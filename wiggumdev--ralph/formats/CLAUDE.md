# ralph

> This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ralph/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bun install       # install deps
bun dev           # run with watch mode
bun run --watch src/index.tsx  # explicit dev command
```

## Architecture

Terminal UI app using OpenTUI + SolidJS + Bun runtime.

**Stack:**
- OpenTUI (`@opentui/core`, `@opentui/solid`) - terminal UI framework
- SolidJS - reactive UI library
- Bun - runtime & bundler
- TypeScript with strict mode

**Entry:** `src/index.tsx` - renders TUI components via `render()` from `@opentui/solid`

**Key config:**
- `bunfig.toml` - preloads `@opentui/solid/preload` for JSX transform
- `tsconfig.json` - JSX import source set to `@opentui/solid`

## OpenTUI Components

Available primitives: `<box>`, `<text>`, `<ascii_font>`

Layout uses flexbox props: `alignItems`, `justifyContent`, `flexGrow`

Text styling via `TextAttributes` enum from `@opentui/core`

---
> Source: [wiggumdev/ralph](https://github.com/wiggumdev/ralph) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-04 -->
