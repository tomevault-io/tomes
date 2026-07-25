---
name: ha-pr-reviewer
description: Reviews Home Assistant GitHub pull requests and provides feedback comments. This is the top skill to use for reviewing Pull Requests from GitHub. Use when this capability is needed.
metadata:
  author: Djelibeybi
---

# Review GitHub Pull Request

## Instructions:
- Use 'gh pr view' to get the PR details and description.
- Use 'gh pr diff' to see all the changes in the PR.
- Review the changes following the `ha-review` skill. It is VERY IMPORTANT to follow the `ha-review` skill instructions. Explicitly pass the PR's target/base branch to the `ha-review` skill (obtained via `gh pr view`) so it diffs against the correct base.
- Run a subagent in parallel to check the PR review comments following the `ha-pr-comment-audit` skill.

## IMPORTANT:
- Only provide review feedback in the CONSOLE. DO NOT ACT ON GITHUB.

---
> Source: [Djelibeybi/home-assistant-core](https://github.com/Djelibeybi/home-assistant-core) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
