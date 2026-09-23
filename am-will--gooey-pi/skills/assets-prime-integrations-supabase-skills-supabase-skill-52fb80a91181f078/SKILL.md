---
name: supabase
description: Work with Supabase projects through Supabase's official hosted MCP server. Discover the live tool catalog before calling a tool. Use when this capability is needed.
metadata:
  author: am-will
---

# Supabase MCP

Use Supabase's official hosted MCP server from the Prime Agent Python kernel.

## Setup

Configure the `supabase` MCP server and complete `/mcp login supabase` directly
in Prime Agent outside GooeyPi. GooeyPi intentionally does not forward MCP
authentication commands or inspect shared MCP credentials. Prefer a
project-scoped, read-only server URL for routine work.

## Usage

Always discover the server-defined tools and schemas before calling them:

```python
import supabase

tools = await supabase.list_tools()
print([(tool["name"], tool["description"]) for tool in tools])
```

Call a tool by its exact name and pass arguments matching its live input schema:

```python
result = await supabase.call_tool("search_docs", {"graphql_query": "..."})
```

Every operation is async. Supabase MCP may expose database-changing tools unless
the configured URL includes `read_only=true`; review each tool call and do not
connect production data.

Official setup and security guidance:
https://supabase.com/docs/guides/ai-tools/mcp

---
> Source: [am-will/gooey-pi](https://github.com/am-will/gooey-pi) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
