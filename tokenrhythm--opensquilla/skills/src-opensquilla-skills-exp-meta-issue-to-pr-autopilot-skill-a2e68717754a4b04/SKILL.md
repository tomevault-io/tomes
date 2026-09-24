---
name: meta-issue-to-pr-autopilot
description: [DEPRECATED] Issue-to-PR autopilot — opens a PR via `gh`, runs a sub-agent fix loop, and writes to git. Disabled pending the E5 bounded sub-agent contract + side-effect ledger (plan §3.1 A8 / §5.3 E4): no risk metadata enforcement, no per-step budget, no rollback path. Do not re-enable without `metadata.opensquilla.risk: high` + capabilities {vcs, filesystem-write, network-write, subprocess} and a saga-style compensation step. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Issue-to-PR Autopilot (Meta-Skill)

Triages an issue, delegates the fix to `sub-agent`, drafts a PR
description with `summarize`, and opens the PR via `gh`. Best used on
small, well-scoped issues with clear acceptance criteria.

## Fallback

Manually call `gh issue view`, code the fix, write the PR body, then
`gh pr create`.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
