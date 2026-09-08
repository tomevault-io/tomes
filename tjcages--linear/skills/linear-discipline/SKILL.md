---
name: linear-discipline
description: >- Use when this capability is needed.
metadata:
  author: tjcages
---

# Linear discipline (always-on)

Chat rules: [RESPONSE.md](./RESPONSE.md). Auth before Linear calls: [AUTH.md](./AUTH.md).

## Detect tracking

**Tracked** if the repo has a “Linear tracking” (or equivalent) section in `CLAUDE.md`, `AGENTS.md`, or `.cursor/rules/*` that names team + project.

**Skipped** if `.linear-tracking-skip` exists at repo root.

## If tracked

Follow the protocol written in-repo:

1. Search before create.
2. Non-trivial work → file/update an issue in the named project + milestone.
3. `Backlog` → `In Progress` at start → `Done` only when shipped.
4. Close the loop before session end (state and/or comment).
5. Prefer Linear’s generated branch names.

Before any Linear tool call: Step 0 auth.

## If untracked and not skipped (soft nudge — 1B)

Ask **once**, one line, no preamble:

> This repo isn’t tracked in Linear. Set it up now? (~10–20 min)

- **Yes** → hand off to `linear-setup` (do not bootstrap inline without that skill’s gates).
- **No** → create `.linear-tracking-skip` at repo root; stay quiet next time.
- Never auto-create Linear projects or issues from a nudge alone.
- Never nudge from Automation / `linear-monitor` runs.

## If skipped

Stay quiet about setup. Still use Linear MCP for explicit user requests.

## Out of scope

Full bootstrap → `linear-setup`. Rescue/audit → `linear-sync`. Health digest → `linear-monitor`.

---
> Source: [tjcages/linear](https://github.com/tjcages/linear) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-28 -->
