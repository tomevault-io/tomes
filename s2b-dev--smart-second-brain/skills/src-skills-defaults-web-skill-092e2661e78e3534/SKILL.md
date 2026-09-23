---
name: web
description: Reach the public internet — fetch web pages and run web searches. Prefer the vault first; reach for the web when the user references a link or when the needed information cannot be in the vault. Only the query or URL you pass is sent to the configured web service, never vault contents. Use when this capability is needed.
metadata:
  author: s2b-dev
---

## Web Access
- Prefer the vault first; reach for web tools when the user references a link or when the needed information cannot be in the vault.
- Only the query or URL you pass is sent to the configured web service — never vault contents.
- Use `web_search` for questions about external facts, current events, documentation, or topics the vault is unlikely to contain. When results look promising, follow up with `fetch_url` to read the full page, and cite sources in your response.
- Use `fetch_url` for URLs the user provided or clearly public references.

---
> Source: [s2b-dev/smart-second-brain](https://github.com/s2b-dev/smart-second-brain) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
