---
name: tldr
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# tldr — skill0

Quick command reference with real-world examples. Better than man pages for "how do I use this command?"

## Quick Start

```bash
# With x-cmd
x tldr git                    # Git usage examples
x tldr --lang zh python       # Chinese docs
x tldr --fz                   # Interactive search

# Without x-cmd — use curl
curl -s "https://raw.githubusercontent.com/tldr-pages/tldr/main/pages/common/git.md"

# Or install a tldr client
pip install tldr
npm install -g tldr
tldr tar
```

## What's Available

| Command | Description |
|---------|-------------|
| `x tldr <cmd>` | Show examples for a command |
| `x tldr --lang zh <cmd>` | Chinese language |
| `x tldr --fz` | Interactive fzf search |
| `x tldr --cat <cmd>` | Raw markdown display |
| `x tldr --ls` | List all available commands |
| `x tldr --update` | Update page cache |

## Standalone Alternatives

- Online: https://tldr.sh
- Python: `pip install tldr`
- Node: `npm install -g tldr`
- Raw pages: github.com/tldr-pages/tldr

## This skill0 grows

Starting with the essentials. Will add:
- Common command patterns
- Platform-specific notes
- Integration with agent workflows

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
