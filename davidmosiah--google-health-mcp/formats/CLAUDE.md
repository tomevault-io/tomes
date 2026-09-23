# google-health-mcp

> This repo is the unofficial Google Health MCP connector for local agent workflows.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/google-health-mcp/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent Development Notes

## Scope

This repo is the unofficial Google Health MCP connector for local agent workflows.

## Commands

- Install: `npm ci`
- Typecheck: `npm run typecheck`
- Build: `npm run build`
- Fast smoke: `npm run smoke`
- HTTP smoke: `npm run smoke:http`
- Full gate: `npm test`

## Rules

- Never commit OAuth client secrets, access tokens, refresh tokens, personal Google Health data, or local config.
- Keep read-only behavior and privacy-safe summaries as the default.
- Preserve agent-ready surfaces: manifest, connection status, privacy audit, CLI UX, Hermes agent manifest, and metadata checks.
- Keep error messages actionable without exposing credentials or raw private payloads.

---
> Source: [davidmosiah/google-health-mcp](https://github.com/davidmosiah/google-health-mcp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-23 -->
