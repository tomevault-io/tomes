# fakesnow

> When a test compares JSON, `VARIANT`, `ARRAY`, or `OBJECT` results as strings, use the existing helpers in `tests.utils` so DuckDB output is normalised to Snowflake's formatting:

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/fakesnow/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent instructions

## Snowflake-compatible result assertions

When a test compares JSON, `VARIANT`, `ARRAY`, or `OBJECT` results as strings, use the existing helpers in `tests.utils` so DuckDB output is normalised to Snowflake's formatting:

- Use `dindent(rows)` for `DictCursor` results.
- Use `indent(rows)` for tuple results.

Do not compare raw DuckDB JSON strings when the assertion is intended to match real Snowflake output.

## Live behavior in tests

Tests should assert the live Snowflake behavior rather than the fake implementation's current limitation.

---
> Source: [tekumara/fakesnow](https://github.com/tekumara/fakesnow) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-09 -->
