# nvbench

> When helping with a pull request review, separate context gathering from review comments. Use the repo-local `review-nvbench` skill when available.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/nvbench/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent Guidance

## PR Review Workflow

When helping with a pull request review, separate context gathering from review comments. Use the repo-local `review-nvbench` skill when available.

The default mode is context gathering: use `ci/util/pr_review_context.sh`, explain the issue, PR intent, implementation strategy, and suggested file review order, but do not produce review findings until the user explicitly asks for feedback. If no issue or PR context is discoverable, explicitly flag that the review is missing required context before proceeding.

Follow `docs/pr_review.md` for the full review workflow and NVBench-specific review focus.

---
> Source: [NVIDIA/nvbench](https://github.com/NVIDIA/nvbench) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-16 -->
