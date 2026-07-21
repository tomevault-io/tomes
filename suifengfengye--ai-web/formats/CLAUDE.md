# ai-web

> - If releasing from floating dependency ranges, then run tests in a fresh env with latest resolved deps before tagging.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ai-web/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Project Prevention Notes

## CI Parity
- If releasing from floating dependency ranges, then run tests in a fresh env with latest resolved deps before tagging.
- If FastMCP internals are used in tests, then use helpers that support both 2.x (`get_tools`) and 3.x (`list_tools`) APIs.
- If release CI runs `black --check`, then run `black` on touched files before pushing the release tag.

---
> Source: [suifengfengye/ai-web](https://github.com/suifengfengye/ai-web) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
