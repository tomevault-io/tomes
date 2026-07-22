---
name: ast-introspection
description: Use Go AST-aware analysis to enumerate symbols, extract signatures, and propose mechanically safe refactors (read-only by default). Use when this capability is needed.
metadata:
  author: pilinux
---

# AST Introspection

## When to Use

- Need a structure-aware view (functions, methods, types, receivers) or a safe, mechanical refactor proposal that relies on code shape rather than string matches.

## What This Skill Does

- Enumerates package-level declarations (funcs, methods, types, const/var) with `path:line` citations.
- Extracts function/method signatures, receivers, and doc comments.
- Lists imports and flags suspicious patterns (duplicates, likely unused groups).
- Proposes minimal, mechanically-safe refactors (rename, extract, signature change) with verification steps.

## Rules

- Prefer read-only inspection (glob, grep, targeted read) before any edit.
- Always include `path:line` citations for code claims.
- Never perform large automated rewrites without an explicit preview, tests, and verification commands.

## Commands

- Enumerate packages: `go list ./...`
- Quick exported view: `go doc <pkg>`

## Output

- **Inventory:** compact list of declarations with `path:line`.
- **Findings:** 2-8 concise bullets (impact + confidence).
- **Proposal:** minimal patch plan (files/hunks) + exact verification commands.

## Examples

- "List all exported methods on type `Auth` with file locations."
- "Propose a safe rename for method X and verify callers."

## Related Skills

- `source-search` (broad grep), `code-navigation` (impact mapping)

## References

- `llms.txt` (project knowledge base)

---
> Source: [pilinux/gorest](https://github.com/pilinux/gorest) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
