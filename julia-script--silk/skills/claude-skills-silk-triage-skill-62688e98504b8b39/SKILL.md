---
name: silk-triage
description: Validate, deduplicate, specify, size, and prioritize Silk maintenance issues from Linear. Use only when Julia explicitly invokes this skill or asks to triage Silk issues. Use when this capability is needed.
metadata:
  author: julia-script
---

# Claude entrypoint for Silk triage

Read `../../../.codex/skills/silk-triage/SKILL.md` completely and follow it as the canonical skill.
Resolve every relative path in that file from its `.codex/skills/silk-triage/` directory, not from
this wrapper. When the canonical workflow requires subagents or a visible plan, use Claude Code's
corresponding agent and task-tracking facilities while preserving the same coordinator boundaries.

---
> Source: [julia-script/silk](https://github.com/julia-script/silk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
