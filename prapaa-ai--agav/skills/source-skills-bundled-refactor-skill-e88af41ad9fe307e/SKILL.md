---
name: refactor
description: Suggest and apply code refactoring Use when this capability is needed.
metadata:
  author: prapaa-ai
---

# Refactor

Analyze code for refactoring opportunities, apply improvements, and verify correctness.

## Instructions

1. Read the target code and its surrounding context (callers, tests, related modules).
2. Identify refactoring opportunities in these categories:
   - **Duplication**: Repeated logic that can be extracted into shared functions or utilities.
   - **Complexity**: Long functions, deep nesting, or convoluted conditionals that can be flattened or decomposed.
   - **Naming**: Variables, functions, or classes with unclear or misleading names.
   - **Structure**: Misplaced responsibilities, god objects, or tight coupling that can be reorganized.
   - **Modernization**: Outdated patterns that can use newer language features or idioms.
3. Propose each refactoring with:
   - What to change and where
   - Why it improves the code (readability, maintainability, testability)
   - Any risks or trade-offs
4. Apply the refactorings using edit_file, making one logical change at a time.
5. After each change, run the existing test suite to confirm nothing broke.
6. If tests fail, revert the change and try an alternative approach or skip that refactoring.
7. Summarize what was changed, why, and the test results.

---
> Source: [prapaa-ai/agav](https://github.com/prapaa-ai/agav) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
