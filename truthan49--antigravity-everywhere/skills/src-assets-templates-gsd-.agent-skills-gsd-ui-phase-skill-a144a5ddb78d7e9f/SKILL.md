---
name: gsd-ui-phase
description: Generate UI design contract (UI-SPEC.md) for frontend phases Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Create a UI design contract (UI-SPEC.md) for a frontend phase.
Orchestrates gsd-ui-researcher and gsd-ui-checker.
Flow: Validate → Research UI → Verify UI-SPEC → Done
</objective>

<execution_context>
@.agent/get-shit-done/workflows/ui-phase.md
@.agent/get-shit-done/references/ui-brand.md
</execution_context>

<context>
Phase number: $ARGUMENTS — optional, auto-detects next unplanned phase if omitted.
</context>

<process>
Execute @.agent/get-shit-done/workflows/ui-phase.md end-to-end.
Preserve all workflow gates.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
