---
name: remove-old-logs
description: Remove log files older than 1 day from logs directory Use when this capability is needed.
metadata:
  author: leshchenko1979
---

Remove log files from /logs that are more than a day old. Use only shell commands:
find logs -name "*.log" -mtime +1 -delete

---
> Source: [leshchenko1979/fast-mcp-telegram](https://github.com/leshchenko1979/fast-mcp-telegram) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-30 -->
