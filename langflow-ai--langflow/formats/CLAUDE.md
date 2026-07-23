# langflow

> This project uses [AGENTS.md](https://agents.md/) as the standard for providing context to AI coding agents. The `@AGENTS.md` import above tells Claude Code to load `AGENTS.md` automatically; other tools that natively support `AGENTS.md` will pick it up directly. The `@.claude/CLAUDE.md` import loads the local hard-rules file (gitignored) that mirrors the PostToolUse hook policy.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/langflow/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

@AGENTS.md
@.claude/CLAUDE.md

This project uses [AGENTS.md](https://agents.md/) as the standard for providing context to AI coding agents. The `@AGENTS.md` import above tells Claude Code to load `AGENTS.md` automatically; other tools that natively support `AGENTS.md` will pick it up directly. The `@.claude/CLAUDE.md` import loads the local hard-rules file (gitignored) that mirrors the PostToolUse hook policy.

---
> Source: [langflow-ai/langflow](https://github.com/langflow-ai/langflow) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-23 -->
