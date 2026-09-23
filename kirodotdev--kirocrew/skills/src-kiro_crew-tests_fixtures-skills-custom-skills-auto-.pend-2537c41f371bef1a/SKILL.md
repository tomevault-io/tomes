---
name: autoflaky-triage
description: Classify a red test as a real regression, a flake, or an environment problem before patching. Use when this capability is needed.
metadata:
  author: kirodotdev
---

# flaky-triage (auto-generated)

## When to use
A shard went red and it is not yet known whether the diff caused it.

## Steps
1. Check whether the same test fails on the base commit.
2. Check whether it fails on one platform only.
3. Only patch once the cause is named.

## Gotchas
- A fail-closed gate red is often a cascade of one real failure.

---
> Source: [kirodotdev/KiroCrew](https://github.com/kirodotdev/KiroCrew) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
