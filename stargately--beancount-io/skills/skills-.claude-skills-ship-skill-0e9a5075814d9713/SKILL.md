---
name: ship
description: Ship pending changes on main by pulling with rebase, committing intentionally, pushing to origin/main, monitoring triggered GitHub Actions and EAS deployment runs, and fixing failures until green. Use only when the user explicitly invokes $ship or asks to ship or publish the current main branch. Do not use for ordinary edits, status checks, pull-request publishing, non-main branches, or requests to commit without pushing. Use when this capability is needed.
metadata:
  author: stargately
---

# Ship

Read and follow the [canonical ship workflow](../../../../.claude/commands/ship.md) completely. Treat any text supplied with the skill invocation as `$ARGUMENTS`.

The linked Claude command is the single source of truth. Do not duplicate or independently amend its workflow here.

---
> Source: [stargately/beancount-io](https://github.com/stargately/beancount-io) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-09 -->
