---
name: env-check
description: Detects the current operating system, shell, and available tools to select the best execution strategy. Use when this capability is needed.
metadata:
  author: LowyShin
---

# env-check Skill

This skill allows the agent to precisely identify the host environment to avoid cross-platform command errors.

## 🛠️ Usage

Use this skill before running any OS-specific terminal commands if the environment is unknown.

### Detection Logic

1.  **Check OS**: Use `ADDITIONAL_METADATA` (preferred) or `run_command` with `$PSVersionTable` (Windows) or `uname -a` (POSIX).
2.  **Check Shell**: Identify if the terminal is `PowerShell`, `cmd`, `bash`, `zsh`, etc.
3.  **Check Tool Availability**: Verify if specific binaries like `rg`, `grep`, `jq`, or `git` are available in the `PATH`.

## 💻 Platform-Specific Command Mapping

| Task | Windows (PowerShell) | POSIX (Bash/Zsh) | Platform Tool (Best) |
| :--- | :--- | :--- | :--- |
| Search Text | `Select-String -Pattern "query" -Path "file"` | `grep "query" "file"` | `grep_search` |
| List Files | `Get-ChildItem -Recurse` | `ls -R` | `list_dir` |
| Read File | `Get-Content "file"` | `cat "file"` | `view_file` |
| JSON Parse | `ConvertFrom-Json` | `jq` | (N/A) |

## 🛡️ Best Practices

- **Priority**: ALWAYS prefer platform-native tools (`grep_search`, `list_dir`, `view_file`) as they work consistently across all operating systems.
- **Fallback**: If a shell command is necessary, use a conditional block to provide both Windows and POSIX equivalents.
- **Verification**: Never assume a tool exists. Use `Get-Command` (Windows) or `which` (POSIX) to verify before execution.

---
> Source: [LowyShin/giip-dev-agent](https://github.com/LowyShin/giip-dev-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
