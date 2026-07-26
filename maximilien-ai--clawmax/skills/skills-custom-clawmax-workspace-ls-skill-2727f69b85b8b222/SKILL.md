---
name: clawmax-workspace-ls
description: | Use when this capability is needed.
metadata:
  author: Maximilien-ai
---

# ClawMax Workspace Directory Listing

This first-party ClawMax skill lets you inspect the current workspace directory structure.

## Usage

Run `ls -la` or `find` on the workspace directories to see:
- Agent configurations (`AGENTS/`)
- Workflow definitions (`WORKFLOWS/`)
- Organization files (`ORG/`)
- Custom skills (`SKILLS/custom/`)
- System files (`SYSTEM/`)

## Example Commands

```bash
# List workspace root
ls -la "$OPENCLAW_WORKSPACE/"

# List all agents
ls -la "$OPENCLAW_WORKSPACE/AGENTS/"

# List all workflows
ls -la "$OPENCLAW_WORKSPACE/WORKFLOWS/"

# Find all markdown files
find "$OPENCLAW_WORKSPACE" -name "*.md" -maxdepth 3

# Check agent identity
cat "$OPENCLAW_WORKSPACE"/AGENTS/*/IDENTITY.md
```

## When to Use

- After template apply: verify agents and workflows were created
- During debugging: check file permissions and structure
- For system tests: validate workspace state

---
> Source: [Maximilien-ai/clawmax](https://github.com/Maximilien-ai/clawmax) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
