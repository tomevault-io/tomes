---
name: nacos-router-weather
description: Opt-in Nacos Router weather PoC; requires a registered weather-mcp server. Use when this capability is needed.
metadata:
  author: clawdotnet
---
This is a static, opt-in contract fixture. Register `weather-mcp` with a
`get_weather(city)` tool before running it. The final output is the tool result;
no model call is needed for this deterministic path. Router prose errors are
not MCP protocol failures: see docs/nacos-mcp-router.md before live use.

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
