---
name: knowledge
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# knowledge — skill0

Search the internet's knowledge sources from the command line.

## Quick Start

```bash
# Install x-cmd
eval "$(curl https://get.x-cmd.com)"

# Hacker News top posts
x hn top

# Wikipedia search
x wkp "artificial intelligence"

# DuckDuckGo search
x ddg "rust programming language"

# RFC documents
x rfc 2616

# Stack Exchange search
x se "how to exit vim"
```

## What's Available

| Command | Source | Example |
|---------|--------|---------|
| `x hn top` | Hacker News | Top 10 trending posts |
| `x hn new` | Hacker News | Latest submissions |
| `x wkp <query>` | Wikipedia | Search articles |
| `x ddg <query>` | DuckDuckGo | Web search |
| `x rfc <number>` | RFC docs | Read RFC specifications |
| `x se <query>` | Stack Exchange | Search Q&A |

## This skill0 grows

Starting with the essentials. Will add:
- More sources (Project Gutenberg, arxiv)
- Advanced search patterns
- Result filtering and formatting tips

## Full experience

`x knowledge --help` for all options after installing x-cmd.

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
