---
name: review-pr
description: Inspect and finish flutter_calendar_carousel pull requests by fixing valid review findings, resolving threads, diagnosing CI, and polling every five minutes until the exact head is clean. Use when this capability is needed.
metadata:
  author: hyochan
---

# Review PR (Claude Code)

Read and follow `.codex/skills/review-pr/SKILL.md` completely. Its authority
rules, current-head evidence, fix/reply/resolve procedure, reviewer fallback,
five-minute polling contract, two-clean-snapshot gate, and no-implicit-merge rule
are canonical for Claude Code too.

Use `.claude/commands/review-pr.md` as the command entry point. For unavailable
reviewers, invoke the local `review-self` skill for exactly one non-polling pass.

---
> Source: [hyochan/flutter_calendar_carousel](https://github.com/hyochan/flutter_calendar_carousel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
