---
name: tvm
description: Build TVM from the current worktree. Use when this capability is needed.
metadata:
  author: apache
---
Build TVM from the current worktree.

## Steps

1. Check that `build/` directory exists. If not, run initial setup:
   ```bash
   mkdir -p build
   cmake -S . -B build
   cmake --build build --parallel
   ```

2. If `build/` already exists, run incremental build:
   ```bash
   cmake --build build --parallel
   ```

3. Report success/failure and build time.

---
> Source: [apache/tvm](https://github.com/apache/tvm) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
