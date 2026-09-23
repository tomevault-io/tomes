---
name: publish
description: | Use when this capability is needed.
metadata:
  author: crystian
---

# publish

The one skill you run when the site is ready to go out.

## Steps
1. Run $check-links on the pages in public/. If it reports broken links, stop and fix them first.
2. If a page needs a content fix, brief [content-editor](../../../.codex/agents/content-editor.toml) with the change.
3. Follow the [deploy runbook](../../../docs/DEPLOY.md): regenerate pages, run the link check, start the server.

---
> Source: [crystian/skill-map](https://github.com/crystian/skill-map) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
