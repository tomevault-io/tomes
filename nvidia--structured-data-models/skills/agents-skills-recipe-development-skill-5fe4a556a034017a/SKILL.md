---
name: recipe-development
description: Compose or restructure SDM model recipes. Use when changing a `Recipe` pipeline. Use when this capability is needed.
metadata:
  author: NVIDIA
---

# Compose an SDM Recipe

1. **Follow the processor skill**: Read `AGENTS.md` and `processor-development`. Put only generally reusable operations in `sdm.processing`. Recipe-specific one-offs stay as lambdas.
2. **Stay sequential**: Write the pipeline inline. Introduce a helper or wrapper only when it is required, not to name a group of steps.
3. **No unused wrappers**: Do not wrap steps in `Sequential`, dtype casts, or named helpers unless they change behavior or remove real duplication.

---
> Source: [NVIDIA/structured-data-models](https://github.com/NVIDIA/structured-data-models) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-04 -->
