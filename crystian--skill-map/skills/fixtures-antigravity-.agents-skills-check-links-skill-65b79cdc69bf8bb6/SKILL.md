---
name: check-links
description: | Use when this capability is needed.
metadata:
  author: crystian
---

# check-links

The last gate before the site goes out. Link targets resolve per the [WHATWG URL standard](https://url.spec.whatwg.org/).

## Steps
1. List every HTML file under `public/`.
2. For each page, collect its internal links (every `href` to `/` or to a `.html` file).
3. Check the target exists under `public/` (treat `/` as `public/index.html`).
4. Report any link whose target is missing; if none, report "0 broken links".

---
> Source: [crystian/skill-map](https://github.com/crystian/skill-map) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
