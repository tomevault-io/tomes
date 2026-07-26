---
name: routine-cookbook
description: Use when working with the single reference for writing Condor routines — fetching Hummingbot data, parallel calls, reports/charts, continuous loops, and candlestick charts. Routes to a companion file per topic.
metadata:
  author: hummingbot
---

# Routine Cookbook

The patterns for building routines, split into **companion files** so you load
only what your task needs. Read this overview, then fetch the relevant file(s):

```
manage_skill(action="read_file", name="routine_cookbook", file="hummingbot_client.md")
```

## Which companion file to read

| Your routine needs to…                                              | Read                    |
|---------------------------------------------------------------------|-------------------------|
| Fetch market data, candles, prices, order book, portfolio, executors| `hummingbot_client.md`  |
| Make 4+ parallel API calls / bulk fetch many pairs / rate-limit     | `async_patterns.md`     |
| Produce a report — KPIs, tables, Plotly charts, rich inline output  | `report_builder.md`     |
| Run a continuous loop (monitor, tracker, alerts) until stopped      | `continuous.md`         |
| Render a candlestick chart, indicator overlay, or volume footprint  | `candles_chart.md`      |

Most routines need `report_builder.md` plus one or two others. A continuous
price monitor with a live dashboard, for example, reads `hummingbot_client.md`
+ `continuous.md`.

## Non-negotiables (apply to every routine)

- **Every routine MUST generate a ReportBuilder report** — see `report_builder.md`.
- All client calls are **async** — always `await`; never `time.sleep`, only `asyncio.sleep`.
- **Parse defensively**: handle `None`/missing keys, return error strings, never raise to the caller.
- Test after writing (`manage_routines(action="run", ...)`) and fix until the output is clean.

These are starting patterns, not a bypass — running a routine still goes through
the normal execution/confirmation controls.

---
> Source: [hummingbot/condor](https://github.com/hummingbot/condor) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
