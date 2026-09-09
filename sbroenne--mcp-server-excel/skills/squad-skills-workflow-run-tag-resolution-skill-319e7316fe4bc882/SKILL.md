---
name: workflow-run-tag-resolution
description: Inspect workflow runs and confirm the failing job/log context. Use when this capability is needed.
metadata:
  author: sbroenne
---

## Context

Use this when a GitHub Actions workflow is triggered by `workflow_run` and needs to recover the release tag or version from the completed source workflow.

## Patterns

1. Check out the source repository with tags before resolving the version.
2. Resolve the tag from the local git graph, not from `git/matching-refs`, when the repo uses annotated tags.
3. Use `git tag --points-at "$HEAD_SHA"` and sort/filter for semver-style release tags.
4. Add a short retry loop to absorb brief tag-visibility delays after the upstream workflow completes.
5. Keep manual replay paths explicit and separately validated.

## Examples

- Good: `actions/checkout@v4` with `fetch-depth: 0`, then `git fetch --force --tags origin` and `git tag --points-at "$HEAD_SHA" --sort=-version:refname`.
- Bad: comparing `workflow_run.head_sha` directly to the REST `matching-refs` `.object.sha` value for annotated tags.

## Anti-Patterns

- Assuming release tags are lightweight tags.
- Resolving the "latest release" instead of the tag that points at the triggering commit.
- Treating an empty tag lookup as proof the release failed before checking whether the lookup method understands annotated tags.

---
> Source: [sbroenne/mcp-server-excel](https://github.com/sbroenne/mcp-server-excel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
