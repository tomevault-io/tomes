---
name: docker-logs
description: Tail logs from Docker containers to check for errors and monitor application behavior. Use when the user types /docker-logs. Use when this capability is needed.
metadata:
  author: blockmatic
---

## Purpose

Tail logs from Docker containers to check for errors and monitor application behavior.

## Steps

1. **Discover running containers**: List all running containers to see what's available using `docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Image}}"`
2. **Ask which containers**: Present list and ask which container(s) they want to monitor
3. **Ask for filters**: Ask if they want any filters (errors only, last N lines, since time, etc.)
4. **Execute command**: Run `docker logs` with suitable flags based on their needs

## Completion

Read [completion evidence](../references/completion.md) before reporting completion.

---
> Source: [blockmatic/basilic](https://github.com/blockmatic/basilic) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
