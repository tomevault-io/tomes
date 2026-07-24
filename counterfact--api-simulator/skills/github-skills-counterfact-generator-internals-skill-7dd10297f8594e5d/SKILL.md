---
name: counterfact-generator-internals
description: > Use when this capability is needed.
metadata:
  author: counterfact
---

# Counterfact Generator Internals Skill

## When to use this skill

Use this skill when changing OpenAPI loading/bundling, schema-to-type generation, operation/type coders, repository/script writing, or generated versions typing.

## Files to inspect first

- `src/typescript-generator/README.md`
- `src/typescript-generator/code-generator.ts`
- `src/typescript-generator/specification.ts`
- `src/typescript-generator/requirement.ts`
- `src/typescript-generator/repository.ts`
- `src/typescript-generator/schema-type-coder.ts`

## Existing conventions to follow

- Keep the generator architecture layered: `Specification/Requirement` -> coders -> `Script` -> `Repository`.
- Preserve regeneration contract: existing route files are not overwritten; generated types are overwritten.
- Support OpenAPI features through typed coders and requirement traversal rather than ad-hoc string logic.
- Keep generated output deterministic and formatted via existing script/repository pipeline.

## Common mistakes to avoid

- Overwriting user-edited route files in `Repository.writeFiles`.
- Implementing new OpenAPI behavior in only one coder path (missing runtime/type parity).
- Skipping fixture/snapshot updates for changed generated output.
- Breaking group/versioned output conventions (`types/versions.ts` per group).

## How to validate the change

- Run: `yarn lint`, `yarn build`, `yarn test`.
- Run focused generator tests first (affected coder + integration/snapshot tests in `test/typescript-generator/`).
- If behavior changes for generated artifacts, verify snapshots and relevant docs (`docs/reference.md`, `docs/faq.md`).

---
> Source: [counterfact/api-simulator](https://github.com/counterfact/api-simulator) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
