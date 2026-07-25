---
name: developer-pr-prep
description: Prepare branches, diffs, tests, and GitHub PR text from Developer Studio. Use when this capability is needed.
metadata:
  author: siddsachar
---

# Developer PR Prep

Use this skill when the user wants to prepare, push, or open a pull request from Developer Studio.

Workflow:

1. Check workspace identity, branch, remote, dirty state, and GitHub CLI status.
2. Recommend a feature branch when the user is still on a protected or shared branch.
3. Review the diff and line counts.
4. Run the relevant tests or clearly state why they were not run.
5. Draft a PR title/body with summary, changed files, tests, and risk.
6. Treat push and PR creation as explicit user-approved actions.

If GitHub CLI is missing or unauthenticated, explain the shortest install/auth path for the current platform.

---
> Source: [siddsachar/Thoth](https://github.com/siddsachar/Thoth) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
