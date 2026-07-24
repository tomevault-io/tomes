---
name: acceptance-tests
description: >- Use when this capability is needed.
metadata:
  author: Activiti
---

# Acceptance Tests (Playwright API)

**Before making any change**, read the full canonical guidelines:

> [`.github/instructions/acceptance-tests.instructions.md`](../../.github/instructions/acceptance-tests.instructions.md)

These are **API-level** tests — no browser UI, page objects, or locators. Tests call REST APIs via the `activiti` fixture and GraphQL WebSocket subscriptions via `services/notifications/`.

## Non-negotiable rules

1. **Never create `tests/**/helpers/`** — API calls in `services/`, shared flows in `flows/`, assertions in specs.
2. **Never define functions inside spec files** — only hooks and test blocks (except `for...of` at describe scope).
3. **Keep API calls in service classes** — wire new methods into existing services.
4. **Keep static test data in `resources/modeling-projects/`** — no inline BPMN/JSON templates.
5. **No comments or JSDoc** in generated code.
6. **No `try/catch` in spec files** — use `afterEach`/`afterAll` for cleanup; use `helpers/query-sync.ts` for tolerant polling.
7. **Cleanup in hooks only** — last statement in every test body must be `expect`.
8. **Import `activiti`/`expect` from `fixtures/services.fixture`** — never from `@playwright/test`.
9. **Never wrap `expect` in `try/catch`, `if`, `switch`, loops, or ternary** — separate tests per scenario.
10. **Use `activiti.step()` for multi-phase tests** — mandatory when a test has 2+ API calls or distinct phases.
11. **Register skips via `pickScenarioTest` + Jira ticket** — not bare inline `activiti.skip()`.

## Architecture (this repo)

```
activiti fixture → services → BaseService → ContextFactory
flows/ — shared process start patterns
services/notifications/ — GraphQL WebSocket engine events
```

Typical spec import:

```typescript
import { activiti, expect } from "../../fixtures/services.fixture";
```

Playwright projects: `acceptance` → `notifications` (serial) → `destructive-last` (`@destructive`).

After edits from `activiti-cloud-acceptance-tests-playwright/`:

```bash
npm run typecheck
npm run lint:fix
```

---
> Source: [Activiti/activiti-cloud](https://github.com/Activiti/activiti-cloud) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
