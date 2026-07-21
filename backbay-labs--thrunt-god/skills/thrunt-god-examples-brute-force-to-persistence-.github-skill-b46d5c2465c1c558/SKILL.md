---
name: thrunt-list-workspaces
description: List active THRUNT workspaces and their status Use when this capability is needed.
metadata:
  author: backbay-labs
---

<objective>
Scan `~/thrunt-workspaces/` for workspace directories containing `WORKSPACE.md` manifests. Display a summary table with name, path, repo count, strategy, and THRUNT project status.
</objective>

<execution_context>
@.github/thrunt-god/workflows/list-workspaces.md
@.github/thrunt-god/references/ui-brand.md
</execution_context>

<process>
Execute the list-workspaces workflow from @.github/thrunt-god/workflows/list-workspaces.md end-to-end.
</process>

---
> Source: [backbay-labs/thrunt-god](https://github.com/backbay-labs/thrunt-god) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
