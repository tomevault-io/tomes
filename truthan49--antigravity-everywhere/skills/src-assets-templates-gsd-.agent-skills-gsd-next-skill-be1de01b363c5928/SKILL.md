---
name: gsd-next
description: Automatically advance to the next logical step in the GSD workflow Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Detect the current project state and automatically invoke the next logical GSD workflow step.
No arguments needed — reads STATE.md, ROADMAP.md, and phase directories to determine what comes next.

Designed for rapid multi-project workflows where remembering which phase/step you're on is overhead.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/next.md
</execution_context>

<process>
Execute the next workflow from @.agent/get-shit-done/workflows/next.md end-to-end.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
