---
name: python-repl-skill
description: Demonstrate a persistent Python workspace across multiple calculation steps. Use when this capability is needed.
metadata:
  author: iii-org
---

# Persistent Python Workspace Demo

Use this skill when the user asks for a multi-step Python calculation that reuses intermediate values.

1. In the first Python execution, define values = [2, 4, 6, 8] and total = sum(values).
2. In a separate Python execution, reuse those existing variables to calculate average = total / len(values).
3. Return the resulting average.
4. Do not create or execute a bundled script for this workflow.

---
> Source: [iii-org/akasha](https://github.com/iii-org/akasha) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-23 -->
