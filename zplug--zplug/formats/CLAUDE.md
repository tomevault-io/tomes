# zplug

> See @AGENTS.md for project architecture, coding guidelines, and development workflow.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/zplug/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md — zplug

See @AGENTS.md for project architecture, coding guidelines, and development workflow.

## Quick Reference

- **Language**: Zsh (not Bash)
- **Run tests**: `make test`
- **Entry point**: `init.zsh`
- **Core logic**: `base/` directory
- **CLI interface**: `autoload/` directory
- **Function naming**: `__zplug::<module>::<submodule>::<function>`

---
> Source: [zplug/zplug](https://github.com/zplug/zplug) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
