---
name: schema-swapping
description: > Use when this capability is needed.
metadata:
  author: pydiverse
---

# Schema Swapping

Transaction model: each stage has two transaction slots (`__odd`/`__even`). During `init_stage`, the inactive slot is prepared. On `commit_stage`, views in the main schema are redirected.

## Key classes

- `Schema` (in `container/`) — wraps name + prefix + suffix, `.get()` returns the full name
- `Stage` — has `.name` (bare), `.current_name` (set during execution), `.transaction_name`
- `_commit_stage_read_views()` calls `on_clear_schema()` and `on_read_view_alias()` callbacks

## Flow

1. `init_stage()`: determines old/new transaction names, syncs metadata, creates the new transaction schema
2. Tasks run, materializing into the transaction schema
3. `commit_stage()`: swaps the main schema views to point at the new transaction schema
4. `_committed_unchanged()`: if stage is fully cache-valid, discards the transaction schema instead

---
> Source: [pydiverse/pydiverse.pipedag](https://github.com/pydiverse/pydiverse.pipedag) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
