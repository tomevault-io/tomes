---
name: nacos-router-weather-retry
description: Opt-in Nacos Router weather PoC: dynamic capability slot with step retry. Use when this capability is needed.
metadata:
  author: clawdotnet
---
Opt-in contract fixture for #233: the capability step permits up to three attempts
(100 ms backoff) only when the host marks weather-mcp/get_weather retry-safe.
The test harness opts in for its read-only fixture. Default Nacos composition
does not assume retry safety and takes the fallback after the first failure.
No model call is needed.

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
