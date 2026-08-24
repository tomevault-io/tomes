---
name: compiler-review
description: Review Rust port code for port fidelity, convention compliance, and error handling. Compares against the original TypeScript source. Use when this capability is needed.
metadata:
  author: react
---

# Compiler Review

Review Rust compiler port code for correctness and convention compliance.

Arguments:
- $ARGUMENTS: Optional commit ref or range (e.g., `HEAD~3..HEAD`, `abc123`). If omitted, reviews uncommitted/staged changes.

## Instructions

1. **Get the diff** based on arguments:
   - No arguments: `git diff HEAD -- compiler/crates/` (uncommitted changes). If empty, also check `git diff --cached -- compiler/crates/` (staged changes).
   - Commit ref (e.g., `abc123`): `git diff abc123~1..abc123 -- compiler/crates/`
   - Commit range (e.g., `HEAD~3..HEAD`): `git diff HEAD~3..HEAD -- compiler/crates/`

2. **If no Rust changes found**, report "No Rust changes to review." and stop.

3. **Identify changed Rust files** from the diff using `git diff --name-only` with the same ref arguments.

4. **Launch the `compiler-review` agent** via the Agent tool, passing it the full diff content. The agent will:
   - Read the architecture guide
   - Find and read the corresponding TypeScript files
   - Review for port fidelity, convention compliance, and error handling
   - Return a numbered issue list

5. **Report the agent's findings** to the user.

---
> Source: [react/react](https://github.com/react/react) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-23 -->
