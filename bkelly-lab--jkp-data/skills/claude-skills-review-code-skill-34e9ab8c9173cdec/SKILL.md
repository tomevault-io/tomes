---
name: review-code
description: Review changed Python files against project conventions. Use when this capability is needed.
metadata:
  author: bkelly-lab
---

Review changed Python files against project conventions.

Gather context, then delegate to the code-critic agent:

1. Run `git diff --name-only HEAD` to find changed files (staged and unstaged)
2. Run `git diff HEAD` to get the full diff
3. Filter to `.py` files only
4. Pass the file list and diff summary to @code-critic for review

If there are no changed Python files, report that there is nothing to review.

---
> Source: [bkelly-lab/jkp-data](https://github.com/bkelly-lab/jkp-data) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
