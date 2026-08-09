---
name: benchopt-contributor
description: > Use when this capability is needed.
metadata:
  author: benchopt
---

# benchopt contributor skills

Guidelines for working on the **benchopt library** itself. For authoring a
*benchmark* (datasets/solvers/objective), use the `using-benchopt` skill that
ships with benchopt — run `benchopt sync-skills` to install it.

- [Gotchas](./gotchas.md) — the sharp edges that pass local checks but fail CI or silently test nothing. Skim first.
- [General implementation design](./general.md) — where to put code, how to validate changes, minimal-edit discipline, and writing concise comments.
- [Scoping issues & PRs](./issues_and_prs.md) — keeping a PR to one concern, commit/what's-new conventions, and how to write issues and review PRs.
- [Tests](./tests.md) — writing CLI tests in `benchopt/cli/tests/` with `temp_benchmark`, `CaptureCmdOutput`, mocking, and parametrize patterns.
- [Documentation](./docs.md) — Sphinx workflow: editing `doc/*.rst`, rebuilding with `-E`, verifying dropdown/tab content; and keeping the agent skills in sync with the code they describe.

---
> Source: [benchopt/benchopt](https://github.com/benchopt/benchopt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-09 -->
