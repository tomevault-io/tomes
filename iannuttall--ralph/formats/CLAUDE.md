# ralph

> Keep this file short. It is always loaded into context.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ralph/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# AGENTS

Keep this file short. It is always loaded into context.

## Build & test
- No build step.
- Tests (dry-run): `npm test`
- Fast real agent check: `npm run test:ping`
- Full real loop: `npm run test:real`

## CLI shape
- CLI entry: `bin/ralph`
- Templates: `.agents/ralph/` (copied to repos on install)
- State/logs: `.ralph/` (local only)
- Skills: `skills/`
- Tests: `tests/`
- Docs/examples: `README.md`, `examples/`

## Quirks / Guardrails
**Add any common quirks guiderails here as needed**

---
> Source: [iannuttall/ralph](https://github.com/iannuttall/ralph) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-04-20 -->
