---
name: gsd-cleanup
description: Archive accumulated phase directories from completed milestones Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Archive phase directories from completed milestones into `.planning/milestones/v{X.Y}-phases/`.

Use when `.planning/phases/` has accumulated directories from past milestones.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/cleanup.md
</execution_context>

<process>
Follow the cleanup workflow at @.agent/get-shit-done/workflows/cleanup.md.
Identify completed milestones, show a dry-run summary, and archive on confirmation.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
