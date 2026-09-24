---
name: ops-rotate
description: OPS on-demand: This skill should be used when the user asks to \"rotate Claude\", \"max seats\", or… Use when this capability is needed.
metadata:
  author: Lifecycle-Innovations-Limited
---

# OPS ► ROTATE (alias → `/ops:accounts`)

Load `ops-rules` before acting. Public repo (no personal data). Outbound: one draft → one approval → one send. If `AskUserQuestion` / `Workflow` are missing, follow Rule 10 in `ops-rules` (Hermes: numbered options / two-turn Telegram card; `delegate_task`).

This skill is a **compat alias**. Route all work through **ops-accounts**:

| Old verb | New |
|----------|-----|
| (none) / status | `ops-accounts status` (Claude section) |
| rotate-now | `ops-accounts switch claude` / `ops-accounts rotate-now` |
| list | `ops-accounts list` |
| add-account | `ops-accounts setup claude` |
| reauth | `ops-accounts reauth claude <email>` |
| pooled seats | CLIProxyAPI — see `/ops:ops-fleet` |

Load **`skills/ops-accounts/SKILL.md`** first, then for Claude-only depth use the
bin:

```bash
"${CLAUDE_PLUGIN_ROOT}/bin/ops-accounts" status
"${CLAUDE_PLUGIN_ROOT}/bin/ops-accounts" rotate-now
"${CLAUDE_PLUGIN_ROOT}/bin/ops-accounts" reauth claude <email>
```

Multi-provider status, Grok, Codex, Factory, Cursor: **`/ops:accounts` only**.

Vision: `docs/ops/OPS-ACCOUNTS-VISION.md`.

---
> Source: [Lifecycle-Innovations-Limited/claude-ops](https://github.com/Lifecycle-Innovations-Limited/claude-ops) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
