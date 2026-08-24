# promptwright

> - ESM only: always use `.js` extension in imports

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/promptwright/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Source of truth: CLAUDE.md
# See CLAUDE.md and packages/*/CLAUDE.md for detailed coding instructions.
# This file exists for Cursor IDE compatibility.

# Promptwright — QA Assistant powered by GitHub Copilot SDK
# TypeScript, pnpm monorepo, Electron + React, Playwright MCP, CDP

## Key Rules
- ESM only: always use `.js` extension in imports
- Module resolution: NodeNext, no path aliases
- Node.js 22+ required
- Never log full MCP configs or Copilot SDK payloads (contain secrets)
- Desktop app must run in Electron, not browser
- Renderer accesses backend only through `window.jarvis`
- After UI changes: `pnpm build && pnpm test:e2e:smoke`

---
> Source: [testronai/promptwright](https://github.com/testronai/promptwright) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-23 -->
