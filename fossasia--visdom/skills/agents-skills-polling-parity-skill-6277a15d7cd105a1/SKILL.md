---
name: polling-parity
description: Keep feature behavior identical across WebSocket and polling transport modes. Use when adding socket commands, event flows, or transport-sensitive UI updates. Use when this capability is needed.
metadata:
  author: fossasia
---

# Skill: Polling and WebSocket Parity

## When to Use

Use this skill for any real-time feature that touches transport behavior.

## Core Workflow

1. Implement feature changes in the primary socket path.
2. Mirror equivalent behavior in polling wrappers/fallback logic.
3. Confirm command names and payload shapes are transport-neutral.
4. Validate environment switch, pane update, and callback routing in both modes.
5. Ensure no mode-specific regressions in reconnect/reload behavior.

## Guardrails

- Do not ship socket-only features.
- Keep command contracts stable across both modes.
- Avoid mode-specific payload forks unless explicitly versioned.

## Documentation

- [Skill reference](references/REFERENCE.md)
- `py/visdom/server/handlers/socket_handlers.py`
- `js/api/ApiProvider.js`
- `js/api/Legacy.js`
- `AGENTS.md`
- `CONTRIBUTING.md`

## Assets

- See `assets/README.md` and store templates/resources in `assets/`.

## Tests

- Follow the default flow in `references/TESTS.md`.

---
> Source: [fossasia/visdom](https://github.com/fossasia/visdom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
