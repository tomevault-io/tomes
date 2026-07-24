---
name: gsd-validate-phase
description: Retroactively audit and fill Nyquist validation gaps for a completed phase Use when this capability is needed.
metadata:
  author: Truthan49
---

<objective>
Audit Nyquist validation coverage for a completed phase. Three states:
- (A) VALIDATION.md exists — audit and fill gaps
- (B) No VALIDATION.md, SUMMARY.md exists — reconstruct from artifacts
- (C) Phase not executed — exit with guidance

Output: updated VALIDATION.md + generated test files.
</objective>

<execution_context>
@.agent/get-shit-done/workflows/validate-phase.md
</execution_context>

<context>
Phase: $ARGUMENTS — optional, defaults to last completed phase.
</context>

<process>
Execute @.agent/get-shit-done/workflows/validate-phase.md.
Preserve all workflow gates.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
