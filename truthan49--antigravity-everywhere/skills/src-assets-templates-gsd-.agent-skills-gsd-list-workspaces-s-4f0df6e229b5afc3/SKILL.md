---
name: gsd-list-workspaces
description: List active GSD workspaces and their status Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Scan `~/gsd-workspaces/` for workspace directories containing `WORKSPACE.md` manifests. Display a summary table with name, path, repo count, strategy, and GSD project status.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/list-workspaces.md
@.agent/get-shit-done/references/ui-brand.md
</execution_context>

<process>
Execute the list-workspaces workflow from @.agent/get-shit-done/workflows/list-workspaces.md end-to-end.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
