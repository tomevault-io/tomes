---
name: mm-bot-report
description: Run the MM bot status report: running bots, open/hold-mode positions, Use when this capability is needed.
metadata:
  author: hummingbot
---

## MM Bot Report

Run the `mm_bot_report` routine — it fetches everything in one shot:

```
manage_routines(action="run", name="mm_bot_report", config={})
```

**What it returns:**
- **Controllers** — active controller count
- **Open positions** — active executors currently placing quotes (`is_trading=True`)
- **Hold-mode** — active executors paused/holding inventory (`is_trading=False`)
- **Recent closes breakdown** — by close type: TP | SL | Early | Hold | Trail | Expired
- **PnL & Volume** — realized + unrealized PnL per controller, total volume
- **Error summary** — error count per active bot from live logs

**Config overrides** (pass as `config={}` keys):
- `trading_pair` — filter to one pair (default: all)
- `connector_name` — filter to one connector (default: all)
- `recent_closes` — how many closed executors to analyze (default: 100)
- `include_errors` — set `false` to skip error log fetch (default: true)

**After reading the output:**
1. Surface the KPIs (open positions, hold-mode count, top close type).
2. Flag any errors — if errors are present, note the bot name and count. For deeper log analysis run `manage_routines(action="run", name="logs_summary")` (global routine).
3. If hold-mode > 0 and user hasn't set it intentionally, flag it — positions holding inventory aren't earning spread.
4. Summarize PnL vs volume to comment on fee efficiency.

---
> Source: [hummingbot/condor](https://github.com/hummingbot/condor) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
