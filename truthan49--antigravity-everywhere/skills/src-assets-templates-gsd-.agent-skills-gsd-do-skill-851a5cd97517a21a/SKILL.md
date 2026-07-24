---
name: gsd-do
description: Route freeform text to the right GSD command automatically Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Analyze freeform natural language input and dispatch to the most appropriate GSD command.

Acts as a smart dispatcher — never does the work itself. Matches intent to the best GSD command using routing rules, confirms the match, then hands off.

Use when you know what you want but don't know which `/gsd-*` command to run.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/do.md
@.agent/get-shit-done/references/ui-brand.md
</execution_context>

<context>
$ARGUMENTS
</context>

<process>
Execute the do workflow from @.agent/get-shit-done/workflows/do.md end-to-end.
Route user intent to the best GSD command and invoke it.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
