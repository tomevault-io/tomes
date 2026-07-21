# src-cli

> - When adding new commands, use `urfave/cli` instead of the legacy `commander` pattern.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/src-cli/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Command Guidelines

- When adding new commands, use `urfave/cli` instead of the legacy `commander` pattern.
- Register new `urfave/cli` commands in the `migratedCommands` map in `cmd/src/run_migration_compat.go`.

---
> Source: [sourcegraph/src-cli](https://github.com/sourcegraph/src-cli) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
