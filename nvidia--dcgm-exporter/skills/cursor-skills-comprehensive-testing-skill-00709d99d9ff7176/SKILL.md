---
name: comprehensive-testing
description: Use when adding or selecting tests for DCGM Exporter changes.
metadata:
  author: NVIDIA
---

# Comprehensive Testing

Pick the lowest layer:

- Package tests for pure Go logic.
- `tests/helm` for chart contracts.
- `tests/docker` for image startup and endpoint behavior.
- `tests/integration` for DCGM/GPU executable behavior.
- `tests/e2e` for Kubernetes/Helm deployment behavior.

Document unavailable GPU, Docker, Kubernetes, or DCGM prerequisites.

---
> Source: [NVIDIA/dcgm-exporter](https://github.com/NVIDIA/dcgm-exporter) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-09 -->
