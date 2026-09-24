---
name: plan-change
description: Turn a feature request into a minimal, file-level implementation plan before any code. Use when this capability is needed.
metadata:
  author: ruvnet
---

# plan-change

Produce an implementation plan for a requested change.

1. Restate the goal in one sentence.
2. List the files to touch and why.
3. Name the smallest interface that satisfies it.
4. Flag anything that ripples beyond three files or widens a permission.

Hand the plan to the implementer; do not write code in this step.

---
> Source: [ruvnet/guardrail](https://github.com/ruvnet/guardrail) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
