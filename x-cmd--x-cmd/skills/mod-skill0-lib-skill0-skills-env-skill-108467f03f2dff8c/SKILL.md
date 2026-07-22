---
name: env
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# env — skill0

Install any software instantly. No sudo. No system pollution.

## Quick Start

```bash
# Install x-cmd
eval "$(curl https://get.x-cmd.com)"

# Install Python
x env use python

# Install Node.js
x env use node

# Install CLI tools
x env use jq
x env use fzf

# Try without installing permanently
x env try python3 script.py
```

## What's Available

600+ packages including:

| Category | Examples |
|----------|---------|
| Languages | python, node, go, bun, java, rust |
| CLI tools | jq, yq, fzf, himalaya |
| Dev tools | claude-code, code-server |

## Key Features

- **No sudo** — installs to user directory
- **Version management** — install and switch versions
- **Try before install** — `x env try` for temporary use
- **Cleanup** — `x env clean` removes unused packages

## This skill0 grows

Starting with the essentials. Will add:
- Common install patterns
- Version pinning tips
- Multi-language project setup guides

## Full experience

`x env --help` for all options after installing x-cmd.

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
