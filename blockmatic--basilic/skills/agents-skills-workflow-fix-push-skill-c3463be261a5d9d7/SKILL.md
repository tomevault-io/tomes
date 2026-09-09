---
name: fix-push
description: Fix reported issues, validate, then commit and push using the Git playbooks. Use when the user types /fix-push. Use when this capability is needed.
metadata:
  author: blockmatic
---

## Purpose and inputs

Invocation requests fix → validate → commit → push for the named issues. Preserve unrelated work. Never force-push, never `--no-verify`, never `--trailer`. This is not `/exec-push` (no PR) and not a merge or deploy.

## Steps

1. Address the reported errors, warnings, or feedback (lint, types, tests, reviews).
2. Run `pnpm qa` in Basilic (or the consuming repo's documented full gate). Fix failures before publishing.
3. Follow [git-commit](../git-commit/SKILL.md) for intended paths only.
4. Follow [git-push](../git-push/SKILL.md). Do not use a bare `git push` that skips those rules.

## Verification

- [ ] The reported issues and the full gate were addressed.
- [ ] Commit and push used the child playbooks.
- [ ] Unrelated local changes remain intact.

## Handoff

Report commit, branch, and push result. Do not open a PR unless the user asked `/git-create-pr` or `/exec-push`.

---
> Source: [blockmatic/basilic](https://github.com/blockmatic/basilic) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
