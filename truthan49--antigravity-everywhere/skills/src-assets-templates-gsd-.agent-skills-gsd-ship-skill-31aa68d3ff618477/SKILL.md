---
name: gsd-ship
description: Create PR, run review, and prepare for merge after verification passes Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Bridge local completion → merged PR. After /gsd-verify-work passes, ship the work: push branch, create PR with auto-generated body, optionally trigger review, and track the merge.

Closes the plan → execute → verify → ship loop.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/ship.md
</execution_context>

Execute the ship workflow from @.agent/get-shit-done/workflows/ship.md end-to-end.

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
