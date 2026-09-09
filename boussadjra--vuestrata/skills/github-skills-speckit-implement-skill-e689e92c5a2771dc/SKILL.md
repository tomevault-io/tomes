---
name: vuestrata
description: Use to execute the next ready task from a feature task list. Use when this capability is needed.
metadata:
  author: boussadjra
---
# speckit-implement Skill

Use to execute the next ready task from a feature task list.

## Rules

1. Read `.specify/specs/NNN-feature/tasks.md`.
2. Pick the first incomplete task whose dependencies are complete.
3. Read the linked plan context.
4. Implement exactly one task.
5. Run required quality gates before marking it complete.
6. If blocked, report the blocker instead of skipping ahead.

---
> Source: [boussadjra/vuestrata](https://github.com/boussadjra/vuestrata) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
