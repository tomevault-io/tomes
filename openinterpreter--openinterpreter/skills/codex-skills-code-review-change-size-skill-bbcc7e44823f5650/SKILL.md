---
name: code-review-change-size
description: Change size guidance (800 lines) Use when this capability is needed.
metadata:
  author: openinterpreter
---

Unless the change is mechanical the total number of changed lines should not exceed 800 lines.
For complex logic changes the size should be under 500 lines.

If the change is larger, explain whether it can be split into reviewable stages and identify the smallest coherent stage to land first.
Base the staging suggestion on the actual diff, dependencies, and affected call sites.

---
> Source: [openinterpreter/openinterpreter](https://github.com/openinterpreter/openinterpreter) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
