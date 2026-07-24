---
name: gsd-health
description: Diagnose planning directory health and optionally repair issues Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Validate `.planning/` directory integrity and report actionable issues. Checks for missing files, invalid configurations, inconsistent state, and orphaned plans.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/health.md
</execution_context>

<process>
Execute the health workflow from @.agent/get-shit-done/workflows/health.md end-to-end.
Parse --repair flag from arguments and pass to workflow.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
