---
name: opentradex-sell
description: Close a paper position by id, booking realized P&L to the ledger. Invoke when the user says "sell", "close", "take profit", "cut it", or references a position id. Price is optional — defaults to the last mark. Use when this capability is needed.
metadata:
  author: deonmenezes
---

# OpenTradex — Close Position

Close an open paper position and book realized P&L.

User arguments: `$ARGUMENTS` — `<position-id> [price]`.

## Flow

1. If no id was given, show the user all open positions so they can pick:
   !`node "${CLAUDE_PLUGIN_ROOT}/bin/tradex.js" positions`
   Then ask which one to close.
2. Close it:
   !`node "${CLAUDE_PLUGIN_ROOT}/bin/tradex.js" sell $ARGUMENTS`
3. Report realized P&L and the new open-position count. If P&L is negative and large (abs > $50), offer a one-line coach note: "Want me to review what went wrong before the next trade?"

## Rules

- Never modify another user's position.
- If the id isn't found, say so clearly and re-show open positions.
- Don't re-enter a position automatically after a close.

---
> Source: [deonmenezes/opentradex](https://github.com/deonmenezes/opentradex) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-11 -->
