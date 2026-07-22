---
name: rtk
description: Prefix shell commands with rtk to apply the token-optimizing proxy (60–90% savings on Git, pytest, ruff, Fabric CLI, file ops). Use when this capability is needed.
metadata:
  author: scardoso-lu
---

# RTK Token Optimizer

RTK reduces token consumption 60–90% by filtering and compressing shell output before it reaches the AI.

- **Claude Code:** The Bash hook intercepts commands automatically — no manual prefix needed.
- **Codex:** No hook is available — prefix commands manually with `rtk`.

## Golden Rule

Prefix every shell command with `rtk`. RTK applies its filter if one exists; otherwise the command runs unchanged.

## Key Commands for This Project

| Workflow | Command |
|---|---|
| Git | `rtk git status` · `rtk git log` · `rtk git diff` |
| Python / ruff | `rtk pytest` · `rtk ruff check` · `rtk pip` |
| Fabric helpers | `rtk fabric-vibe notebook ...` · `rtk fabric-vibe workspace ...` · `rtk fabric-vibe pipeline manage ...` |
| Files | `rtk ls` · `rtk find` · `rtk grep` |
| Build | `rtk tsc` · `rtk cargo build` |

## Analytics

- `rtk gain` — token savings summary for this session
- `rtk discover` — scan shell history to find new optimization opportunities
- `rtk session` — adoption tracking

---
> Source: [scardoso-lu/fabric-skills-settings](https://github.com/scardoso-lu/fabric-skills-settings) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
