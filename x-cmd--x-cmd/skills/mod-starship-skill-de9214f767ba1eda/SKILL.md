---
name: x-cmd
description: Starship.rs cross-shell prompt with theme management. Use when this capability is needed.
metadata:
  author: x-cmd
---
---
name: x-starship
description: |
  Starship.rs cross-shell prompt with theme management.
  Minimal, blazing-fast, and infinitely customizable prompt.
  Auto-downloads starship binary if not available.
  
  **Dependency**: This is an x-cmd module. Install x-cmd first (see x-cmd skill for installation options).
  see x-cmd skill for installation.

## Prerequisites

| Tool | Purpose | Notes |
|------|---------|-------|
| x-cmd | Required module runtime | `brew install x-cmd` |
| starship | Prompt engine | Optional - x-cmd auto-downloads from GitHub if not present |

**Auto-download Security**: When starship is not found locally, x-cmd downloads the official binary from GitHub (https://github.com/starship/starship/releases). All downloads are verified with SHA256 checksums before execution.


license: Apache-2.0
compatibility: POSIX Shell

metadata:
  author: Li Junhao
  version: "1.0.0"
  category: x-cmd-extension
  tags: [x-cmd, starship, prompt, theme, shell]

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
