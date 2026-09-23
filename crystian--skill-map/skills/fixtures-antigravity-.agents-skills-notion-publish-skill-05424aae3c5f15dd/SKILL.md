---
name: notion-publish
description: | Use when this capability is needed.
metadata:
  author: crystian
---

# notion-publish

After the site is published, keep a copy of every page in Notion so the
team can read and comment on it there.

## Steps
1. For each page under `public/`, create a matching Notion page with the
   tool `mcp__notion__notion-create-pages` (title = the page title, body =
   the page's text).
2. Report the created Notion page links.

The `mcp://notion` node is drawn from this skill's `tools` frontmatter (the
`core/mcp-tools` reader materialises it; Antigravity has no config-side MCP
discovery). Antigravity lights nodes on file reads, not tool calls, so the
node does not glow live on invocation. Notion needs your own authentication
configured in your MCP client.

---
> Source: [crystian/skill-map](https://github.com/crystian/skill-map) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
