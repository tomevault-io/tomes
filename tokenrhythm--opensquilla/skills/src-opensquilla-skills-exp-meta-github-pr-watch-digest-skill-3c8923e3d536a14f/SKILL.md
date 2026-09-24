---
name: meta-github-pr-watch-digest
description: Inspect the user's open GitHub PRs / failing CI / new issues via `gh`, summarize into 3 buckets (to-review / awaiting-me / CI-red), and persist follow-ups to memory. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# GitHub PR Watch & Digest (Meta-Skill)

Daily PR-queue triage: pulls open PRs / failing CI / new comments via
the `github` skill (gh CLI), digests into three actionable buckets, and
records follow-ups to long-term memory.

## Fallback

LLM should manually call `gh pr list`, `gh run list --status failure`,
summarize, and `memory_save`.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
