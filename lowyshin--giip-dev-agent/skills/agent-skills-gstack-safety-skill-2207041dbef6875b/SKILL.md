---
name: gstack-safety
description: | Use when this capability is needed.
metadata:
  author: LowyShin
---

# Gstack Safety Guardrails

> "Maximum safety for production and complex work."

## 1. Careful Mode (Safety Guardrails)

When activated (user says "be careful" or the agent detects a risky command), the agent must:

- **Warn before destructive commands**: `rm -rf`, `DROP TABLE`, `force-push`, `force-delete`, etc.
- **Confirm environment**: Verify if the command is running against production or staging.
- **Explain impact**: Clearly state what will be deleted or changed.
- **Provide override**: Allow the user to proceed explicitly.

## 2. Freeze Mode (Edit Lock)

Restrict file edits to a specific directory or set of files.

- **Locking**: Define the `FREEZE_BOUNDARY` (e.g., `src/app/admin/`).
- **Persistence**: Any edits outside this boundary are blocked until `/unfreeze` or another location is specified.
- **Purpose**: Prevent accidental side-effects in unrelated parts of the codebase while deep in a bug fix.

## 3. Guard Mode (Full Safety)

Combine `/careful` and `/freeze` in one command.

- Enables safety warnings for all commands.
- Locks edits to the current task's scope.

## 4. Usage Table

| Command | Action |
|---------|--------|
| `be careful` | Activate warnings for destructive commands. |
| `freeze {path}` | Lock all subsequent edits to the specified directory. |
| `guard` | Combo: `be careful` + `freeze current_dir`. |
| `unfreeze` | Remove the edit lock. |


## ⚡ Optimization Integration
When using this skill for critical tasks, please run it within a /native-trace context to capture performance data for self-improvement via /aioptimize.


---
> Source: [LowyShin/giip-dev-agent](https://github.com/LowyShin/giip-dev-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
