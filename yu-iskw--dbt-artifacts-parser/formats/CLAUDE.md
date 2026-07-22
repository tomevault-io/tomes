# dbt-artifacts-parser

> See [AGENTS.md](AGENTS.md) for project overview, setup, commands, and parser refresh workflow.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/dbt-artifacts-parser/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

See [AGENTS.md](AGENTS.md) for project overview, setup, commands, and parser refresh workflow.

- When using Claude Code, pre-commit runs as a quality gate on Stop via [.claude/hooks/run-pre-commit.sh](.claude/hooks/run-pre-commit.sh) (configured in [.claude/settings.json](.claude/settings.json)).
- Use the **dbt-parser-refresh** skill when updating parsers: `.claude/skills/dbt-parser-refresh/SKILL.md` or invoke `/dbt-parser-refresh`.

---
> Source: [yu-iskw/dbt-artifacts-parser](https://github.com/yu-iskw/dbt-artifacts-parser) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
