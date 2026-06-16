---
name: skill-npmpublish
description: Publish npm packages with private access and patch version bumps by default. Use when this capability is needed.
metadata:
  author: hasna
---
# skill-npmpublish

Publish npm packages with private access and patch version bumps by default.

## Quick Reference

```bash
# Default: private, patch bump (0.0.1)
bun run src/index.ts

# Options
--bump <patch|minor|major>  # Version bump type (default: patch)
--public                    # Publish as public (default: private)
--dry-run                   # Preview without publishing
--dir <path>                # Package directory
```

## Project Structure

- `src/index.ts` - CLI entry point
- `SKILL.md` - Claude Code / Codex skill definition

## Skill Installation

For Claude Code:
```bash
ln -s $(pwd) ~/.claude/skills/npmpublish
```

For Codex:
```bash
ln -s $(pwd) ~/.codex/skills/npmpublish
```

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/hasna) — claim your Tome and manage your conversions.
<!-- tomevault:4.0:skill_md:2026-04-15 -->
