# chrome-devtools-mcp

> This repository contains an MCP server and CLI for Chrome DevTools.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/chrome-devtools-mcp/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

This repository contains an MCP server and CLI for Chrome DevTools.

# Instructions

- Use only scripts from `package.json` to run commands.
- Use `npm run build` to run tsc and test build.
- Use `npm run test` to build and run tests, run all tests to verify correctness.
- Use `npm run test path-to-test.ts` to build and run a single test file, for example, `npm run test tests/McpContext.test.ts`.
- Use `npm run format` to fix formatting and get linting errors.

## Rules for TypeScript

- Do not use `any` type.
- Do not use `as` keyword for type casting.
- Do not use `!` operator for type assertion.
- Do not use `// @ts-ignore` comments.
- Do not use `// @ts-nocheck` comments.
- Do not use `// @ts-expect-error` comments.
- Prefer `for..of` instead of `forEach`.

---
> Source: [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-03 -->
