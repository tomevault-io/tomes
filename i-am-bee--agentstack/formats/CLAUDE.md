# agentstack

> Use `gh` command for GitHub operations.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/agentstack/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent Stack

## GitHub Operations

Use `gh` command for GitHub operations.

Repo: `i-am-bee/agentstack`

All commits must be signed off for DCO compliance (`git commit --signoff`).

## Useful scripts
- `mise run agentstack-server:migrations:run` run migrations

## Development rules

- When working in agentstack-server make sure you always test the behaviour using the agentstack-server debugging approach
- All testing and linting can be done via `mise run check`
- Formatting can be fixed via `mise run fix`
- Breaking API changes must be documented in `docs/development/reference/changelog.mdx`

---
> Source: [i-am-bee/agentstack](https://github.com/i-am-bee/agentstack) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-18 -->
