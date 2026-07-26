# snowflake-connector-nodejs

> Standards for writing and modifying test files: TypeScript usage, test naming conventions, and mock server URL rules

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/snowflake-connector-nodejs/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

### Code Rules

When creating new test files, write them in TypeScript.

When writing test names, don't use "should"
❌ `it('should pass the check')`
✅ `it('passes the check')`

When sending API requests to mock servers, always use snowflake.com domains instead of random sites like test.com to prevent accidental data leakage.
❌ `https://test.com/api/endpoint`
❌ `https://example.com/api/endpoint`
✅ `https://snowflake.com/api/endpoint`

---
> Source: [snowflakedb/snowflake-connector-nodejs](https://github.com/snowflakedb/snowflake-connector-nodejs) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-26 -->
