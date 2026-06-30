# node-libcurl

> Node.js bindings for libcurl - a powerful HTTP/HTTPS client library.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/node-libcurl/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Project: node-libcurl

## Overview
Node.js bindings for libcurl - a powerful HTTP/HTTPS client library.

## Development Commands

### Install Dependencies
```bash
pnpm install
```

### Build
```bash
npm run build
```

### Test
```bash
npm test
```

### Lint
```bash
npm run lint
```

### Type Check
```bash
npm run typecheck
```

## Project Structure
- Native C++ bindings for libcurl
- TypeScript/JavaScript interface
- Cross-platform support (Windows, macOS, Linux)

## Important Notes
- Uses Node.js native addons
- Requires libcurl to be installed on the system
- Main branch for PRs: `develop`
- Always use pnpm pregyp build to build the addon, do not use pnpm run build.

---
> Source: [JCMais/node-libcurl](https://github.com/JCMais/node-libcurl) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-06-29 -->
