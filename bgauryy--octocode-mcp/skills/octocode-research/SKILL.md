---
name: octocode-research
description: > HTTP API server wrapping `octocode-mcp` tools for code research at `localhost:1987` by default (configurable via `OCTOCODE_RESEARCH_HOST` / `OCTOCODE_RESEARCH_PORT`) Use when this capability is needed.
metadata:
  author: bgauryy
---
# Octocode Research Skill - Agent Development Guide

> HTTP API server wrapping `octocode-mcp` tools for code research at `localhost:1987` by default (configurable via `OCTOCODE_RESEARCH_HOST` / `OCTOCODE_RESEARCH_PORT`)

## Project Overview

| Attribute | Value |
|-----------|-------|
| **Type** | Express.js HTTP Server |
| **Host** | localhost (default) |
| **Port** | 1987 (default) |
| **Package** | `octocode-research` |
| **Version** | 2.0.0 |
| **Main Dependency** | `octocode-mcp` |

---

## Quick Commands

```bash
# Development
npm run build       # Bundle with tsdown
npm start           # Run bundled server
npm run dev         # Run with tsx watch mode
npm test            # Run tests with Vitest
npm run test:watch  # Watch mode testing
npm run lint        # ESLint check
npm run lint:fix    # Auto-fix lint issues

# Server Health Check
curl http://localhost:1987/health
```

---

## Project Structure

```
octocode-research/
├── src/
│   ├── server.ts              # Express server entry point
│   ├── index.ts               # Re-exports from octocode-mcp
│   ├── mcpCache.ts            # MCP client caching
│   ├── routes/
│   │   ├── local.ts           # Local tool handlers (used in tests)
│   │   ├── lsp.ts             # LSP tool handlers (used in tests)
│   │   ├── github.ts          # GitHub tool handlers (used in tests)
│   │   ├── package.ts         # Package tool handlers (used in tests)
│   │   ├── tools.ts           # /tools/* - MAIN tool API (mounted)
│   │   └── prompts.ts         # /prompts/* - prompt discovery (mounted)
│   ├── middleware/
│   │   ├── errorHandler.ts    # Error response formatting
│   │   ├── logger.ts          # Request/response logging
│   │   ├── queryParser.ts     # Zod validation
│   │   └── readiness.ts       # Server readiness check
│   ├── validation/
│   │   ├── index.ts           # Schema exports
│   │   ├── schemas.ts         # HTTP schemas (import from octocode-mcp)
│   │   └── httpPreprocess.ts  # HTTP query string preprocessing
│   ├── utils/
│   │   ├── colors.ts          # Console color functions
│   │   ├── logger.ts          # File-based logging
│   │   ├── responseBuilder.ts # Role-based response formatting
│   │   ├── responseFactory.ts # Response creation helpers
│   │   ├── responseParser.ts  # MCP response parsing
│   │   ├── resilience.ts      # Resilience utilities
│   │   ├── retry.ts           # Retry with backoff
│   │   ├── circuitBreaker.ts  # Circuit breaker pattern
│   │   └── routeFactory.ts    # Route handler factory
│   ├── types/
│   │   ├── express.d.ts       # Express type extensions
│   │   ├── guards.ts          # Type guard functions
│   │   ├── mcp.ts             # MCP protocol types
│   │   ├── responses.ts       # Response types
│   │   └── toolTypes.ts       # Tool parameter types
│   └── __tests__/
│       ├── integration/       # Integration tests
│       │   ├── circuitBreaker.test.ts
│       │   └── routes.test.ts
│       └── unit/              # Unit tests
│           ├── circuitBreaker.test.ts
│           ├── logger.test.ts
│           ├── responseBuilder.test.ts
│           └── retry.test.ts
├── docs/
│   ├── API_REFERENCE.md       # Complete HTTP API reference
│   ├── ARCHITECTURE.md        # Architecture documentation
│   └── FLOWS.md               # Main flows & connections
├── references/
│   └── GUARDRAILS.md          # Safety guardrails
├── scripts/                   # Bundled output
│   ├── server.js              # Bundled server
│   └── server.d.ts            # Type declarations
├── SKILL.md                   # Skill definition for AI agents
├── AGENTS.md                  # This file
├── tsdown.config.ts           # tsdown bundler configuration
├── package.json
├── tsconfig.json
├── eslint.config.mjs
└── vitest.config.ts           # Test configuration
```

---

## API Endpoints

### Available Routes

| Endpoint | Description |
|----------|-------------|
| `GET /health` | Server health check |
| `GET /tools/list` | List all tools (concise) |
| `GET /tools/info` | List all tools with details |
| `GET /tools/info/:toolName` | Get specific tool schema (call BEFORE using!) |
| `GET /tools/system` | Get system prompt (load FIRST) |
| `GET /tools/initContext` | Combined system prompt + all tool schemas (recommended for init) |
| `POST /tools/call/:toolName` | **Execute any tool** |
| `GET /prompts/list` | List all prompts |
| `GET /prompts/info/:promptName` | Get specific prompt content |

### Tool Execution (Unified API)

**All tools are called via `POST /tools/call/:toolName`** with JSON body:

```bash
curl -X POST http://localhost:1987/tools/call/localSearchCode \
  -H "Content-Type: application/json" \
  -d '{"queries":[{
    "pattern":"useState",
    "path":"/project",
    "mainResearchGoal":"Find React hooks",
    "researchGoal":"Locate useState",
    "reasoning":"Need source location"
  }]}'
```

### Available Tools (via `/tools/call/:toolName`)

| Tool Name | Category | Description |
|-----------|----------|-------------|
| `localSearchCode` | Local | Code search via ripgrep |
| `localGetFileContent` | Local | Read file content |
| `localFindFiles` | Local | Find files by pattern/metadata |
| `localViewStructure` | Local | View directory tree |
| `lspGotoDefinition` | LSP | Go to symbol definition |
| `lspFindReferences` | LSP | Find all references |
| `lspCallHierarchy` | LSP | Call hierarchy (incoming/outgoing) |
| `githubSearchCode` | GitHub | Search GitHub code |
| `githubGetFileContent` | GitHub | Read GitHub files |
| `githubSearchRepositories` | GitHub | Search repositories |
| `githubViewRepoStructure` | GitHub | View repo structure |
| `githubSearchPullRequests` | GitHub | Search pull requests |
| `packageSearch` | Package | Search npm/PyPI packages |

---

## Key Files & Responsibilities

### Entry Points

| File | Purpose |
|------|---------|
| `src/server.ts` | Express app creation, route mounting, graceful shutdown |
| `src/index.ts` | Re-exports octocode-mcp functions with cleaner names |
| `src/mcpCache.ts` | MCP client instance caching and management |

### Routes

Each route file follows the pattern:
1. Import tool function from `../index.js`
2. Define Express Router
3. Apply validation middleware
4. Execute tool and format response

### Middleware

| File | Purpose |
|------|---------|
| `queryParser.ts` | Validates query params against Zod schemas |
| `errorHandler.ts` | Catches errors, formats consistent responses |
| `logger.ts` | Logs requests to console and file |
| `readiness.ts` | Server readiness check middleware |

### Validation

Schemas are imported from `octocode-mcp/public` (source of truth) and wrapped with HTTP preprocessing.

| File | Purpose |
|------|---------|
| `schemas.ts` | HTTP-wrapped schemas importing from `octocode-mcp/public` |
| `httpPreprocess.ts` | Query string conversion (string→number/boolean/array) |

When adding/modifying endpoints:
1. Check if schema exists in `octocode-mcp/public`
2. Create HTTP wrapper in `validation/schemas.ts` with preprocessing
3. Apply schema validation in route handler

---

## Development Guidelines

### Adding a New Endpoint

1. **Add schema** in `src/validation/schemas.ts`
2. **Create route handler** in appropriate `src/routes/*.ts`
3. **Add route to server.ts** if new route group
4. **Update types** if needed
5. **Add tests** in `src/__tests__/`
6. **Document** in docs/ARCHITECTURE.md

### Code Style

- **TypeScript strict mode** enabled
- **Zod** for runtime validation
- **Express async handlers** - wrap with try/catch or error middleware
- **Consistent logging** - use `agentLog`, `successLog`, `errorLog` from colors.ts

### Testing

```bash
yarn test                 # Run all tests
yarn test:watch          # Watch mode
yarn test -- --coverage  # With coverage report
```

---

## Response Format

### Single Query Response (`POST /tools/call/:toolName`)

```typescript
{
  tool: "localSearchCode",
  success: true,
  data: { files: [...], totalMatches: 10 },
  hints: ["Use lineHint for LSP tools", ...],
  research: {
    mainResearchGoal: "...",
    researchGoal: "...",
    reasoning: "..."
  }
}
```

### Bulk Query Response (2-3 queries)

```typescript
{
  tool: "localSearchCode",
  bulk: true,
  success: true,
  instructions: "...",
  results: [
    { id: 1, status: "hasResults", data: {...}, research: {...} },
    { id: 2, status: "empty", data: {...}, research: {...} }
  ],
  hints: { hasResults: [...], empty: [...], error: [...] },
  counts: { total: 2, hasResults: 1, empty: 1, error: 0 }
}
```

### Error Response

```typescript
{
  tool: "localSearchCode",
  success: false,
  data: {},
  hints: ["Error recovery hint..."],
  research: {...}
}
```

---

## Key Dependencies

| Package | Purpose |
|---------|---------|
| `octocode-mcp` | Core tool implementations |
| `express` | HTTP server framework |
| `zod` | Schema validation |
| `@modelcontextprotocol/sdk` | MCP format types |

---

## Documentation References

| Doc | Purpose |
|-----|---------|
| [SKILL.md](./SKILL.md) | How AI agents should USE this skill |
| [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md) | Detailed architecture |
| [docs/FLOWS.md](./docs/FLOWS.md) | Main flows & component connections |

---

## Console Output Colors

| Category | Color | Function |
|----------|-------|----------|
| Agent messages | 🟣 Purple | `agentLog()` |
| Tool results | 🔵 Blue | `resultLog()` |
| Success | 🟢 Green | `successLog()` |
| Errors | 🔴 Red | `errorLog()` |
| Warnings | 🟡 Yellow | `warnLog()` |
| Secondary info | Gray | `dimLog()` |

---

## Troubleshooting

### Server won't start
```bash
# Check if port 1987 is in use
lsof -i :1987

# Kill existing process
kill -9 $(lsof -ti :1987)
```

### Build errors
```bash
# Clean and rebuild
rm -rf scripts/
npm run build
```

### Missing dependencies
```bash
# Reinstall
rm -rf node_modules/
yarn install
```

---

## Access Control

| Path | Access |
|------|--------|
| `src/`, `src/__tests__/` | ✅ Auto |
| `docs/`, `references/` | ✅ Auto |
| `*.json`, `*.config.*` | ⚠️ Ask first |
| `.env*`, `node_modules/`, `scripts/` | ❌ Never modify |

---

*This skill wraps `octocode-mcp` tools as HTTP endpoints. For tool-specific documentation, see the [octocode-mcp package](https://github.com/bgauryy/octocode-mcp/blob/main/packages/octocode-mcp/AGENTS.md).*

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/bgauryy) — claim your Tome and manage your conversions.
<!-- tomevault:4.0:skill_md:2026-04-11 -->
