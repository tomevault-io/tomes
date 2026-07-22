---
name: pr
description: Rules and checklist for preparing PRs, creating changesets, and releasing packages in the monorepo. Use when this capability is needed.
metadata:
  author: kubb-labs
---

# PR Skill

This skill instructs agents on PR preconditions, changeset usage, and reviewer expectations.

## When to Use

- When a user asks how to prepare a PR or what checks are required before merging
- When guiding contributors to create changesets or update the changelog

## What It Does

- Enforces the PR checklist: `format, lint, typecheck, tests`
- Instructs on creating and using changesets for version bumps
- Describes release/merge expectations and documentation updates

## Commands to Suggest

```bash
pnpm format && pnpm lint:fix
pnpm typecheck
pnpm test
pnpm changeset
```

## Checklist

- [ ] CI green (unit tests, linters, typechecks)
- [ ] Documentation updated if public behavior changed
- [ ] No secrets in the PR
- [ ] Appropriate version bump via changeset

## Related Skills

| Skill                                              | Use For                          |
| -------------------------------------------------- | -------------------------------- |
| **[../changelog/SKILL.md](../changelog/SKILL.md)** | Update changelogs and changesets |

---
> Source: [kubb-labs/kubb](https://github.com/kubb-labs/kubb) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
