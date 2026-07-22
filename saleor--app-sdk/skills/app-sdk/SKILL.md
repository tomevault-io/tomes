---
name: app-bridge-actions
description: > Use when this capability is needed.
metadata:
  author: saleor
---

# App Bridge Actions

Guide for extending the app-to-Dashboard communication layer in `@saleor/app-sdk`. The app (inside
the Dashboard iframe) sends commands through **exactly one** channel: an `actions.*` action sent via
`appBridge.dispatch()`. These rules keep new features on that channel instead of inventing a parallel
`postMessage` protocol.

## Why App Bridge Exists

Apps are third-party web apps embedded in the Dashboard via a cross-origin `<iframe>`. That boundary
blocks shared JS, DOM, and cookies, so the browser's only sanctioned transport is
`window.postMessage`. App Bridge is the typed wrapper over that single link: **app → Dashboard =
actions (`dispatch`)**, **Dashboard → app = events (`subscribe`)**. There is one physical pipe — a
second message protocol isn't a new capability, just an ungoverned use of the same pipe. That is why
every command must be an action.

## When to Apply

- Adding a new app → Dashboard command (redirect, notification, resize, popup close, etc.)
- Reporting iframe size / height / layout to the Dashboard
- Adding or exporting a helper or hook that calls `window.parent.postMessage`
- Reviewing a PR that introduces a new `postMessage` `type` string or message constant
- Touching `src/app-bridge/actions.ts`, `app-bridge.ts`, or `index.ts`

## Rule Categories

| Priority | Category   | Impact   | Prefix       |
| -------- | ---------- | -------- | ------------ |
| 1        | App Bridge | CRITICAL | `appbridge-` |

## Quick Reference

### 1. App Bridge (CRITICAL)

- `appbridge-use-dispatch` — Use `actions.*` + `dispatch()`, never manual `postMessage`; helpers/hooks wrap dispatch; fire-and-forget for frequent actions
- `appbridge-add-action` — Recipe for adding an action in `actions.ts` (ActionType → payload → creator → register → test)
- `appbridge-release-safety` — The action `type`, exported constants, and helper signatures are public API; pre-release/breaking-change checklist

## How to Use

Read individual rule files for explanations and code examples:

```
rules/appbridge-use-dispatch.md
rules/appbridge-add-action.md
rules/appbridge-release-safety.md
```

## Full Compiled Document

For the complete guide with all rules expanded: `AGENTS.md`

---
> Source: [saleor/app-sdk](https://github.com/saleor/app-sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
