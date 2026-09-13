---
name: upscale
description: >- Use when this capability is needed.
metadata:
  author: guaardvark
---

# Upscaling with Guaardvark

Read `setup` first; needs the `upscaling` plugin (`POST /api/plugins/upscaling/start`).
`B=${GUAARDVARK_URL:-http://localhost:5000}`. Models: `GET $B/api/upscaling/models` (default `HAT-L_SRx4`);
install one with `POST $B/api/upscaling/models/download {"model": "<id>"}` only after the user says so.

## One image (synchronous, seconds)

```bash
curl -s -X POST $B/api/upscaling/upscale/image \
  -F file=@/abs/path/in.png -F model=HAT-L_SRx4 -F scale=4 -F sharpen=0.2 -F denoise_strength=0.1
```
Returns the finished file (`output_path`, served under `GET $B/api/upscaling/output/image/<filename>`).
Form options: `model`, `scale`, `sharpen`, `denoise_strength`.

## Many images (queued)

```bash
curl -s -X POST $B/api/upscaling/upscale/images -F files=@a.png -F files=@b.png -F model=HAT-L_SRx4 -F scale=2
```
Returns a job id; poll `GET $B/api/upscaling/jobs/<job_id>`; `GET $B/api/upscaling/jobs` lists all.

## Video (queued, frame by frame)

```bash
curl -s -X POST $B/api/upscaling/upscale/video -H 'Content-Type: application/json' -d '{
  "input_path": "/abs/path/clip.mp4", "model": "realesrgan-x2", "scale": 2, "two_pass": false, "suffix": "_4k"
}'
```
`output_path` is optional. Same job polling. Video upscaling is slow: minutes per hundred frames
at 1080p on a 16 GB card. Say so before queuing.

## Rules

- Preview first when in doubt: `POST $B/api/upscaling/preview` (multipart, same form fields) runs a crop.
- Pick the model for the content: HAT-L for photos, Real-ESRGAN x2 for video, anime models for
  line art. The models list carries descriptions.
- The GPU is exclusive; a running video upscale blocks image and video generation until it finishes.

---
> Source: [guaardvark/guaardvark](https://github.com/guaardvark/guaardvark) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
