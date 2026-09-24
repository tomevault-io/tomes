---
name: meta-long-running-build-watchdog
description: [DEPRECATED] Build watchdog — launches arbitrary commands from the user message in tmux and lets sub-agent auto-apply a fix. Disabled pending the E5 bounded sub-agent contract + Jinja sandbox + side-effect ledger (plan §3.1 A1/A8 / §5.3 E4): the launch task interpolates raw user_message into a shell-bound tmux session and the heal step lets sub-agent mutate state with no rollback. Do not re-enable without `metadata.opensquilla.risk: high` + capabilities {shell, tmux, filesystem-write, subprocess} and a saga-style compensation step. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Long-Running Build Watchdog (Meta-Skill)

Watches a long-running command via tmux, lets `sub-agent` diagnose
failures and propose a fix, and records the diagnosis to memory.
Designed for overnight model fine-tunes, CI image builds, or repeated
regression suites that may fail intermittently.

## Fallback

Manually start a tmux session, scrape output, ask the LLM to diagnose,
record the resolution.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
