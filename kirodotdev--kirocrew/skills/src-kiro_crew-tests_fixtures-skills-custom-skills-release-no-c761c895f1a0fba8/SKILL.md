---
name: release-notes
description: Draft a release note section from a commit range, grouped by what the reader gets. Use when this capability is needed.
metadata:
  author: kirodotdev
---

# release-notes

## When to use
Asked to draft the changelog section for a version bump.

## Steps
1. Read the commit range and partition it -- account for every commit.
2. Group by what the reader gets, most interesting first. Never by commit type.
3. Lead with breaking changes when the release has any.

## Gotchas
- A list of commit subjects is not a changelog section.
- Never restate a count of commits.

---
> Source: [kirodotdev/KiroCrew](https://github.com/kirodotdev/KiroCrew) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
