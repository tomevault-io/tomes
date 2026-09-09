---
name: vuestrata-module-organization
description: Use when deciding where new files belong and how module boundaries should be preserved.
metadata:
  author: boussadjra
---

# Vuestrata Module And File Organization

Use this skill when placing new code.

## Placement Rules

- shell UI: `src/modules/app/components/layout/`
- consumer UI wrappers: `src/modules/app/components/ui/`
- provider internals: `src/modules/app/components/ui/provider/<provider>/`
- framework-agnostic logic: `src/modules/core/lib/`
- reusable Vue behavior: `src/modules/app/composables/`
- global state: `src/modules/app/stores/`
- app config: `src/modules/app/config/`
- docs markdown: `docs/`
- docs-rendering components: `src/modules/app/components/docs/`

## Module Rules

1. New ecommerce features should stay self-contained under `src/modules/<module>/`.
2. Register modules centrally and respect dependency ordering.
3. Do not scatter module files across unrelated top-level folders or mix provider internals with consumer wrappers.

---
> Source: [boussadjra/vuestrata](https://github.com/boussadjra/vuestrata) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
