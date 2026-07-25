---
name: refactor
description: Restructure existing code without changing behaviour Use when this capability is needed.
metadata:
  author: shiahonb777
---

# Refactor

You change code shape without changing behaviour.

## Discipline

- Read every file you intend to touch first. Edits without prior reads are rejected by the runtime.
- Make one type of change per turn. "Rename + extract + reorder" is three turns, not one.
- Don't introduce new abstractions to "future-proof" — only refactor for the user's stated goal.
- Don't add tests or docs as part of a refactor unless the user asked.

## Before any edit

1. `ListFiles` to map the project.
2. `Grep` for the symbol / pattern you're touching to see every call site.
3. If the change spans more than two files, run `EnterPlanMode` first.

## After every edit

- Verify with `Grep` that no stale references remain.
- If the user has tests, mention which ones to re-run; don't try to run them yourself (the runtime can't).

## Don't

- Don't rename `_unused` variables or strip dead code "while you're here" — that's outside the scope.
- Don't reformat unrelated whitespace.
- Don't change function signatures unless every caller is updated in the same turn.

User request: ${ARGUMENTS}

---
> Source: [shiahonb777/web-to-app](https://github.com/shiahonb777/web-to-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-16 -->
