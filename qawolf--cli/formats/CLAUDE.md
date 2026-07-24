# cli

> Path-scoped rules are in `.claude/rules/` and load automatically when editing matching files.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/cli/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

@AGENTS.md

## Claude Code

Path-scoped rules are in `.claude/rules/` and load automatically when editing matching files.

After editing a file, run:

```bash
bun run lint:fix
bun run format
```

---
> Source: [qawolf/cli](https://github.com/qawolf/cli) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
