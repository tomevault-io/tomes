---
name: gsd-fast
description: Execute a trivial task inline — no subagents, no planning overhead Use when this capability is needed.
metadata:
  author: Truthan49
---


<objective>
Execute a trivial task directly in the current context without spawning subagents
or generating PLAN.md files. For tasks too small to justify planning overhead:
typo fixes, config changes, small refactors, forgotten commits, simple additions.

This is NOT a replacement for /gsd-quick — use /gsd-quick for anything that
needs research, multi-step planning, or verification. /gsd-fast is for tasks
you could describe in one sentence and execute in under 2 minutes.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/fast.md
</execution_context>

<process>
Execute the fast workflow from @.agent/get-shit-done/workflows/fast.md end-to-end.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
