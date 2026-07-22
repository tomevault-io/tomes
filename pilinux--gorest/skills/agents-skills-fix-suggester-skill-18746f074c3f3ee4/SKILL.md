---
name: fix-suggester
description: Diagnose failures and propose minimal, test-backed fixes with verification and rollback instructions. Use when this capability is needed.
metadata:
  author: pilinux
---

# Fix Suggester

## When to Use

- A test or runtime error is reported and you need a safe, auditable fix plan.

## Rules

- Prefer the smallest atomic change that fixes the problem.
- Include: rationale, exact patch plan (files + hunks), verification commands, and a one-line rollback.
- Highlight security/auth or data-migration risks explicitly.

## Output

- **Diagnosis:** concise bullets (root cause + confidence).
- **Fix plan:** files + short hunk descriptions.
- **Verify:** specific commands and expected outputs.
- **Rollback:** single command/step.

## Examples

- "Failing test X shows nil pointer in Y" - propose fix, tests to run, rollback.
- "Login returns 500 instead of 401" - trace handler logic, propose fix.

## Related Skills

- `safe-edit-simulator`, `patch-applier`, `test-runner`

---
> Source: [pilinux/gorest](https://github.com/pilinux/gorest) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
