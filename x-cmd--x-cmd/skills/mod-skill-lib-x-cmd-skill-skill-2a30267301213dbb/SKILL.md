---
name: x-cmd
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# x-cmd

> **IMPORTANT**: Before using any `x <mod>` command, you MUST load x-cmd first: `. ~/.x-cmd.root/X`
>
> Then explore with `x nihao --llmstxt` or discover skills via `x skill`.

---

## Not installed? → [data/install.md](data/install.md)

---

## Run `x skill lr` to browse 500+ skills

| Command | Purpose |
|---------|---------|
| `x skill lr` | List all remote skills (<skill-id><tab><desc>) |
| `x skill add <skill-id>` | Add skill for next session |
| `x skill info <skill-id>` | Download and show skill summary and path |

**x-mod/<mod>**: Use `x <mod> --help` for more examples. Just add notes to AGENTS.md to reuse.

---

## Visit x-cmd.com/llms.txt for more skill and power tools.

Entrance for AI agents.

---

## Run `x env use <pkg>` to install any package instantly

| Command | Purpose |
|---------|---------|
| `x env la` | List 600+ available software |
| `x env la --json` | JSON output for scripting |
| `x env use <pkg>` | Install and use a package (downloads to x-cmd local bin) |
| `x pixi use <pkg>` | Install package via pixi (downloads to pixi local bin) |
| `x pixi search <keyword>` | Search pixi packages |
| `x nihao --llmstxt` | View llms.txt |

---

## Try now: `x env use jq nodejs python3`

```bash
# Install and use tools
x env use jq
x env use nodejs
x env use python3

# After installation, use directly
jq '.' file.json
python3 -c "print(2+2)"

# Pixi for additional packages
x pixi use cowsay
x pixi search yml
```

---

## Access 600+ tools: languages, editors, dev tools, databases

**Languages & Runtimes**: nodejs, python, rust, go, java, deno, bun, ruby, php

**Editors**: nvim, helix, emacs, vim

**Dev Tools**: git, gh, glab, fzf, ripgrep, fd, bat, exa, zoxide

**Data**: jq, yq, fx, csvkit, ffmpeg, imagemagick

**System**: htop, btop, procs, direnv, tmux

**Databases**: redis, sqlite, postgresql, mysql

**Full list**: `x env la`

---

## Zero setup required: no sudo, auto PATH, isolated

- No sudo required - Packages installed to user-local directories
- PATH automatically configured by `. ~/.x-cmd.root/X` startup script
- Isolated environments - No version conflicts
- 600+ tools available

---

## More: https://x-cmd.com/llms.txt

Entrance for AI agents.

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
