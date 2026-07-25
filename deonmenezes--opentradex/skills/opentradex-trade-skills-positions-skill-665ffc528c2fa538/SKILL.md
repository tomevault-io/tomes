---
name: opentradex-positions
description: Show all open paper positions with entry, mark, and unrealized P&L. Invoke when the user says "positions", "what am I holding", "book", "blotter", or checks in on open trades. Use when this capability is needed.
metadata:
  author: deonmenezes
---

# OpenTradex — Positions

Show the user their open paper book and, if useful, a slim tail of recent realized trades.

## Flow

1. Pull open positions:
   !`node "${CLAUDE_PLUGIN_ROOT}/bin/tradex.js" positions`
2. For each position, display: `id · rail · symbol · side · qty · entry · mark · unrealizedPnl · openedAt`.
3. If the user asked about history ("recent trades", "what did I close"), also pull:
   !`node "${CLAUDE_PLUGIN_ROOT}/bin/tradex.js" trades`
4. Finish with a short summary: "You have N open, total unrealized = $X."

## Rules

- Don't fabricate marks — show what's in the ledger.
- Redact no fields — positions are user-owned data they want to see.
- Keep it skim-friendly: one line per position.

---
> Source: [deonmenezes/opentradex](https://github.com/deonmenezes/opentradex) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-11 -->
