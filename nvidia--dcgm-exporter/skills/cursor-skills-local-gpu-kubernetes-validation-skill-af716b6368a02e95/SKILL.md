---
name: local-gpu-kubernetes-validation
description: Use when validating DCGM Exporter in a local GPU-backed k3d/Kubernetes environment.
metadata:
  author: NVIDIA
---

# Local GPU Kubernetes Validation

Prerequisites: Linux, NVIDIA driver, Docker, k3d, kubectl, Helm, NVIDIA
Container Toolkit, and a usable GPU.

Typical workflow:

```bash
make e2e-local-check
make e2e-local-up
make e2e-local-deploy
make test-e2e
```

Use `make e2e-local-logs` and `make e2e-local-status` for triage.

---
> Source: [NVIDIA/dcgm-exporter](https://github.com/NVIDIA/dcgm-exporter) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-09 -->
