---
name: borzoi-pytorch-port
description: > Use when this capability is needed.
metadata:
  author: aipoch
---

# Borzoi — DNA → Functional Track Prediction

## Prerequisites

| Requirement | Minimum | Recommended |
| ----------- | ------- | ----------- |
| Python      | 3.10+   | 3.11        |
| CUDA        | 12.1+   | 12.4+       |
| GPU VRAM    | 16 GB   | 24 GB+      |

## How to run

```python
from borzoi_pytorch import Borzoi

model = Borzoi.from_pretrained("johahi/borzoi-replicate-0").cuda().eval()
# input: (batch, 4, 524288) one-hot DNA  → output: (batch, tracks, 6144) bins
```

Borzoi consumes ~524 kb one-hot windows and emits binned predictions across
7,611 human tracks (the separate 2,608-track mouse head is off by default;
enable via `enable_mouse_head=True` and select with
`forward(..., is_human=False)`). For variant scoring, run ref/alt windows
centred on the variant and compare per-track output.

## Output format

`(B, T, L)` tensor — `T` tracks × `L` 32-bp bins. Track metadata (assay,
biosample) is in `borzoi_pytorch.pytorch_borzoi_model.TRACKS_DF` (or `model.tracks_df` when using the `AnnotatedBorzoi` subclass) — the base `Borzoi` model has no `targets` attribute.

## Remote compute

Needs ≥24 GB VRAM and either pre-cached HF weights or egress to
`huggingface.co`. Read `compute_details({provider, mode:'read'})` for an
environment with `borzoi-pytorch`, then:

```python
c = host.compute.create(provider)
job = c.submitJob(
    intent="Borzoi track prediction for 1 locus — 1×GPU, ~2 min",
    inputs=[{"src": "borzoi_run.py", "dstFilename": "borzoi_run.py"}],
    command="python3 borzoi_run.py",   # env selection is host-specific — see compute_details for your provider
    outputs=["tracks.npz"],
    timeoutSeconds=1800,
)
print(job.job_id)   # cell ends here — kernel never blocks on compute
```

Retain the exact returned `job_id`. Query that saved ID with the non-blocking
`c.attachJob(job_id).status()` or `.result()` when its state or result is relevant; do not scan Job
history. A final `.result()` read reports whether its follow-up was `suppressed` or had already been
`committed`; otherwise the app starts the later analysis turn for an unread final result. See the
`remote-compute-ssh` skill for details.

If the provider exposes a weight-cache mount, point `HF_HOME` at it inside
`borzoi_run.py` (path is in `compute_details`).

## Troubleshooting

| Symptom                     | Cause                   | Fix                                                             |
| --------------------------- | ----------------------- | --------------------------------------------------------------- |
| `module has no __version__` | Package exposes no attr | Use `importlib.metadata.version("borzoi-pytorch")`              |
| Shape mismatch on input     | Wrong window length     | Pad/crop to 524288 bp (fixed; not exposed as a model attribute) |

---

**Next**: combine track deltas with `evo2` likelihood deltas for a
two-axis variant prioritisation.

---
> Source: [aipoch/open-science](https://github.com/aipoch/open-science) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
