---
name: developer-review
description: Code-review workflow for Developer Studio repositories. Use when this capability is needed.
metadata:
  author: siddsachar
---

# Developer Review

Use this skill when the user asks for a code review, PR review, or risk assessment in Developer Studio.

Prioritize findings over summaries:

1. Inspect workspace identity, branch, dirty state, and changed files.
2. Read relevant diffs and implementation files.
3. Look for correctness bugs, regressions, data loss, security issues, concurrency hazards, and missing tests.
4. Run or recommend focused tests where useful.
5. Report findings first with file paths and line references when possible. If no issues are found, say so clearly and mention residual risk.

Do not rewrite code during a review unless the user asks for fixes.

---
> Source: [siddsachar/Thoth](https://github.com/siddsachar/Thoth) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
