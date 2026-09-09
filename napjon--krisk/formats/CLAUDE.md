# krisk

> - Preserve traditional pandas/Jupyter use without requiring a server, MCP, or database.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/krisk/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Krisk Development

- Preserve traditional pandas/Jupyter use without requiring a server, MCP, or database.
- Keep REST and MCP thin; all behavior belongs in `KriskService` or lower layers.
- Never persist or log connection URLs, credentials, or environment-variable values.
- MCP/REST chart specifications must remain declarative and reject executable JavaScript.
- Use `uv` for Python and `bun` for JavaScript. Do not use pip, npm, or yarn.
- Bind the unauthenticated v1 server to loopback on port 8060.
- Do not add Postgres or Redis containers; local development uses the shared infrastructure.
- Do not modify legacy notebooks merely to normalize their outputs.

---
> Source: [napjon/krisk](https://github.com/napjon/krisk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-09 -->
