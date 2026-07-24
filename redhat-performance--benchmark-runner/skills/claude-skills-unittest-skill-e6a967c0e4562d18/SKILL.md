---
name: benchmark-runner
description: 1. **Regenerate golden files** Use when this capability is needed.
metadata:
  author: redhat-performance
---
# /unittest

Run all unit tests.

## Steps

1. **Regenerate golden files**
   ```bash
   make golden_files
   ```

2. **Run all unit tests**
   ```bash
   PYTHONPATH=. python3 -m pytest -v tests/unittest/
   ```
   All tests must pass.

## Notes

- Fix any failing tests before pushing
- Golden file tests are included — run `make golden_files` first if templates changed

---
> Source: [redhat-performance/benchmark-runner](https://github.com/redhat-performance/benchmark-runner) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
