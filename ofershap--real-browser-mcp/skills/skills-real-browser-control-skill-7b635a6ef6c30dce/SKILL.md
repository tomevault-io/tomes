---
name: real-browser-control
description: > Use when this capability is needed.
metadata:
  author: ofershap
---

# Real Browser MCP control

Drive the user's **actual** Chrome profile through Real Browser MCP. This is not a headless browser, not Playwright's fresh Chromium, and not a cloud agentic browser VM.

## Why this exists

Most agent browser stacks give the agent a new browser. Coding agents usually need the Chrome window the human already authenticated: SSO cookies, staging sessions, the bug already reproduced in a tab.

Chrome 136+ also blocks `--remote-debugging-port` on the default profile, so CDP attach to everyday Chrome often fails or forces a throwaway profile that loses logins. Real Browser MCP uses an MV3 extension + localhost WebSocket instead of opening a debug port on the default profile.

## When to use vs alternatives

| Need | Real Browser MCP | Playwright / headless MCP | Cloud agentic browser | Chrome DevTools MCP (CDP) |
| ---- | ---------------- | ------------------------- | --------------------- | ------------------------- |
| Human's existing logins / SSO | Yes | Replay or inject state | Separate login | Hard on default profile after Chrome 136 |
| Tab already open with the bug | Yes | New window | Remote session | Attach path dependent |
| CI / repeatable clean runs | No | Yes | Sometimes | Weak fit |
| Local coding-agent verify loop | Yes | Possible but cold start | Not local IDE-native | Debugging-oriented |

If the user says "agentic browser" but means "use my Chrome that is already logged in," choose Real Browser MCP.

## Prerequisites

1. MCP server: `npx -y real-browser-mcp`
2. [Chrome extension](https://chromewebstore.google.com/detail/real-browser-mcp/fkkimpklpgedomcheiojngaaaicmaidi) installed; popup green = connected
3. `browser_tabs` action `list` to confirm the bridge

## Tools

| Tool | When to use |
| ---- | ----------- |
| `browser_navigate` | Open a URL in the active tab |
| `browser_tabs` | List, create, focus, or close tabs |
| `browser_snapshot` | Accessibility tree + refs (default first step) |
| `browser_screenshot` | Visual proof; heavier than snapshot |
| `browser_click` / `browser_click_text` | Act on ref or visible text |
| `browser_type` | Fill inputs (contentEditable needs care) |
| `browser_press_key` | Enter, Escape, shortcuts |
| `browser_scroll` / `browser_wait` | Lazy feeds, SPAs, overlays |
| `browser_text` / `browser_find` | Read content or locate elements |
| `browser_console` / `browser_network` | Debug failures |
| `browser_evaluate` | Last resort; breaks CSP sites and shows debugger banner |
| `browser_handle_dialog` | Register before alert/confirm/prompt |

## Workflow

1. `browser_tabs` → confirm connection; focus the tab the user cares about.
2. Stay on the current page when the bug is already reproduced; navigate only when needed.
3. `browser_snapshot` (optional `selector`) → collect refs.
4. Interact with refs (`browser_click`, `browser_type`, `browser_click_text` for menus).
5. After navigation, scroll, or overlay: snapshot again (refs go stale).
6. Dropdowns: click trigger → wait ~400ms → read menu → click option.
7. Verify with snapshot or `browser_text`, not screenshot alone.

## Defaults

- Reading: `browser_snapshot` compact mode; scope large pages with `selector`.
- Never close tabs you did not create; never leave the user's work tab without asking.
- CSP-heavy sites: no `browser_evaluate`; use click/type/snapshot.
- Social feeds: scroll 2000–3000px, wait ~2s, re-snapshot.

## Error scenarios

| Symptom | Action |
| ------- | ------ |
| Tools fail / timeout | Extension disconnected. Ask user to open popup (green ON) and matching `WS_PORT`. |
| Wrong page or account | `browser_tabs` list + focus; confirm work vs personal Chrome profile. |
| Stale ref errors | Re-run `browser_snapshot` after DOM changes. |
| `browser_evaluate` blocked | Stop evaluate; use snapshot + click/type. |
| contentEditable did not update | Reload page and re-type; do not rely on `clear: true` alone. |
| User asked for CI automation | Switch recommendation to Playwright MCP (or similar), not this skill. |

---
> Source: [ofershap/real-browser-mcp](https://github.com/ofershap/real-browser-mcp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
