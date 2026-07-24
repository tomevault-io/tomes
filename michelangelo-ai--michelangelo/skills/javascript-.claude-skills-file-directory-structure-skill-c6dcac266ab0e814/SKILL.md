---
name: file-and-directory-structuring
description: Trigger when implementing any new feature, hook, or component — decisions about where to put new files and how to import them must follow these rules. Also trigger when adding imports. Use when this capability is needed.
metadata:
  author: michelangelo-ai
---

# File & Import Organization

## Import Strategy

- **Co-locate related code** — types, context, hooks, tests, and utils live alongside the component they belong to
- **Flat over nested** — start flat; introduce a subdirectory only when you have multiple files of the same type (e.g., several hooks → `hooks/`, several utils → `utils/`)

## Directory Structure

- `components/` — feature building blocks
- `__tests__/` — place in the closest directory to the tested code
- `constants.ts`, `types.ts` — single files at the feature root
- `styled-components.ts` — reusable styled components for the feature

## Code Placement Strategy

1. **Start local** — put code in `components/my-component/utils/`
2. **Promote when needed** — move to a shared `utils/` when multiple parts need it
3. **Namespace filenames** — `table/components/table-action-button.tsx`, not `action-button.tsx`

## Hooks/Utils

- Single file: `use-hook-name.ts` directly in the component directory
- Multiple files: extract to a `hooks/` or `utils/` subdirectory

## Naming

- **Variables**: camelCase
- **Constants**: UPPER_SNAKE_CASE

## Anti-Patterns

- ❌ Generic filenames without namespace (`action-button.tsx` vs `table-action-button.tsx`)

---
> Source: [michelangelo-ai/michelangelo](https://github.com/michelangelo-ai/michelangelo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
