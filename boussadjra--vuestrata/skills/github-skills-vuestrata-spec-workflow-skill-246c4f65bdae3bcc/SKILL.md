---
name: vuestrata-spec-workflow
description: Use when deciding whether non-trivial work needs a spec and how it should fit the existing backlog.
metadata:
  author: boussadjra
---

# Vuestrata Spec Workflow

Use this skill for work that should not jump straight to code.

## Use When

- the request spans multiple subsystems
- public behavior, docs, env keys, or settings may change
- the issue exposes architecture or contract drift

## Rules

1. Treat `.specify/specs/` as the source of truth for non-trivial work.
2. Reuse or extend an existing spec before creating a new one.
3. New work belongs in `.specify/specs/NNN-name/` with `spec.md`, `plan.md`, and `tasks.md`.
4. Specs stay brownfield-specific and reflect repo reality, not generic templates.
5. Before implementation, read the active spec, then plan, then tasks.

---
> Source: [boussadjra/vuestrata](https://github.com/boussadjra/vuestrata) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
