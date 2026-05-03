# lsap

> - Lint & format: `ruff check --fix && ruff format`

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/lsap/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# AGENTS.md

## Development Commands

- Lint & format: `ruff check --fix && ruff format`
- Type checking: `ty check <dir_or_file>`
- Run tests: `uv run pytest`
- Python commands: always use `uv`

## Code Style Guidelines

- Python: 3.12+ required
- Imports & Formatting: use ruff
- Async: Use async/await, `asyncer.TaskGroup` for concurrency

## Implementation Guidelines

- Path Handling: `client.from_uri()` returns relative paths by default. Use `relative=False` explicitly when absolute paths are required (e.g., for path comparisons in exclusion sets).

## API Design

- **Skill**: MUST use `lsap-api-design` skill first before designing new APIs

## Testing

- Run `uv sync --upgrade` before testing and fixing type errors

---
> Source: [lsp-client/LSAP](https://github.com/lsp-client/LSAP) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-03 -->
