---
name: ponytail-review
description: >- Use when this capability is needed.
metadata:
  author: uplbtools
---

# Ponytail review

Hunt complexity only. One line per finding: location, what to cut, what replaces it.

## Format

`path:L42: tag: finding. replacement.`

Tags: `delete:` | `stdlib:` | `native:` | `yagni:` | `shrink:`

End with: `net: -N lines possible.` or `Lean already. Ship.`

## Out of scope

Correctness, security, performance — normal review. Do not apply fixes; list only.

## Room TBA

Pair with [agent-contract](../../rules/agent-contract.mdc). Flag drive-by refactors and duplicate UI surfaces.

Upstream: https://github.com/DietrichGebert/ponytail — `skills/ponytail-review/SKILL.md`

---
> Source: [uplbtools/room-tba](https://github.com/uplbtools/room-tba) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
