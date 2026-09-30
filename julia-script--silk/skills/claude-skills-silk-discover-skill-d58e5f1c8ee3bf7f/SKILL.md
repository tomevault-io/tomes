---
name: silk-discover
description: Verify current remote main, run a deep parallel Silk maintenance sweep, and file every qualifying discovery lead in Linear. Use only when Julia explicitly invokes this skill or asks for a Silk maintenance sweep. Use when this capability is needed.
metadata:
  author: julia-script
---

# Claude entrypoint for Silk discovery

Read `../../../.codex/skills/silk-discover/SKILL.md` completely and follow it as the canonical skill.
Resolve every relative path in that file from its `.codex/skills/silk-discover/` directory, not from
this wrapper. When the canonical workflow requires subagents or a visible plan, use Claude Code's
corresponding agent and task-tracking facilities while preserving the same coordinator boundaries.

---
> Source: [julia-script/silk](https://github.com/julia-script/silk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
