---
name: code-review
description: Review code changes for bugs, security issues, and improvements Use when this capability is needed.
metadata:
  author: prapaa-ai
---

# Code Review

Review the current git diff or specified files for defects and improvements.

## Instructions

1. Run `git diff` (or `git diff --cached` for staged changes) to obtain the changeset. If specific files are provided, scope the review to those files.
2. Read each changed file in full to understand surrounding context, not just the diff hunks.
3. Analyze every change for the following categories:
   - **Bugs**: Logic errors, off-by-one mistakes, null/undefined access, race conditions, missing error handling.
   - **Security**: Injection vulnerabilities, hardcoded secrets, unsafe deserialization, missing auth checks.
   - **Performance**: Unnecessary allocations, O(n^2) patterns, missing caching opportunities, redundant I/O.
   - **Style**: Naming inconsistencies, dead code, overly complex expressions, missing type annotations.
4. For each finding, report:
   - File path and line number
   - Severity: critical, warning, or suggestion
   - A concise description of the issue
   - A recommended fix or improvement
5. Group findings by file. Present critical issues first, then warnings, then suggestions.
6. If no issues are found, confirm the changes look correct and explain why.
7. Keep feedback actionable. Avoid vague commentary; always suggest a concrete fix.

---
> Source: [prapaa-ai/agav](https://github.com/prapaa-ai/agav) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
