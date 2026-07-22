---
name: freighter-best-practices
description: Freighter is a non-custodial Stellar wallet shipped as a browser extension Use when this capability is needed.
metadata:
  author: stellar
---

# Freighter Best Practices

Freighter is a non-custodial Stellar wallet shipped as a browser extension
(Manifest V3) for Chrome and Firefox. The repository is a Yarn workspaces
monorepo with four main workspaces:

1. **extension/** -- the browser extension itself (popup, background service
   worker, content scripts)
2. **@stellar/freighter-api/** -- the npm SDK that dApps use to interact with
   Freighter
3. **@shared/** -- shared packages (api, constants, helpers) consumed by
   multiple workspaces
4. **docs/** -- documentation and skills

## Reference Guide

| Concern              | File                                | When to Read                                             |
| -------------------- | ----------------------------------- | -------------------------------------------------------- |
| Code Style           | references/code-style.md            | Writing or reviewing any code                            |
| Architecture         | references/architecture.md          | Adding features, understanding the codebase              |
| Security             | references/security.md              | Touching keys, messages, storage, or dApp interactions   |
| Testing              | references/testing.md               | Writing or fixing tests                                  |
| Performance          | references/performance.md           | Optimizing renders, bundle size, or load times           |
| Error Handling       | references/error-handling.md        | Adding error states, catch blocks, or user-facing errors |
| Internationalization | references/i18n.md                  | Adding or modifying user-facing strings                  |
| Messaging            | references/messaging.md             | Adding popup<>background<>content script communication   |
| Git & PR Workflow    | references/git-workflow.md          | Branching, committing, opening PRs, CI                   |
| Dependencies         | references/dependencies.md          | Adding, updating, or auditing packages                   |
| Anti-Patterns        | references/anti-patterns.md         | Code review, avoiding common mistakes                    |
| Troubleshooting      | ../../docs/troubleshooting-guide.md | Build failures, setup issues, known bugs and gotchas     |

---
> Source: [stellar/freighter](https://github.com/stellar/freighter) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
