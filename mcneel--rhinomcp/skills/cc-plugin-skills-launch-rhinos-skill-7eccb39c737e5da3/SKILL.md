---
name: launch-rhinos
description: Spin up N Rhino MCP sessions in parallel and fan out one agent per Rhino. Use when the user wants multiple Rhinos running simultaneously with each agent driving its own — e.g. "spawn 3 agents and have each launch Rhino", "run 5 Rhino tasks in parallel". For a single Rhino, use `/launch-rhino` instead. Use when this capability is needed.
metadata:
  author: mcneel
---

# Launching N parallel Rhino MCP sessions

Follow the procedure in the [`/launch-rhinos`](../../commands/launch-rhinos.md) slash command. It owns the full flow — slot probing, OS-specific launch (sequential on macOS, parallel on Windows), listener wait, and the agent fan-out. Pass through the count and the version argument; default version to `8`. Use only the pre-declared slots in `.mcp.json` (`rhino`, `rhino-2` … `rhino-8`).

---
> Source: [mcneel/RhinoMCP](https://github.com/mcneel/RhinoMCP) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
