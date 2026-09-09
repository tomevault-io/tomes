---
name: vuestrata-quality-gates
description: Use when deciding the smallest correct verification set for a change in this repo.
metadata:
  author: boussadjra
---

# Vuestrata Quality Gates

Use this skill to choose validation fast.

## Rules

- Use the `vp` CLI only; do not use `pnpm`, `npm`, `yarn`, or `bun` directly.
- Start with `vp check` (runs format, lint, and typecheck).
- Add focused unit tests when logic, stores, composables, auth, validation, or modules change.
- Add `vpr build` when routes, layouts, config, providers, or runtime wiring change.
- Add `vpr test:e2e` only for user-visible flow or routing changes.
- Validate changed tooling paths directly for dependencies, CI, or containers.
- Do not finish non-trivial work with known diagnostics in touched files.

---
> Source: [boussadjra/vuestrata](https://github.com/boussadjra/vuestrata) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
