---
name: content-editor
description: | Use when this capability is needed.
metadata:
  author: crystian
---

# content-editor

Turns a short brief into a finished portfolio page.

## How to write a page
1. Read the style guide and the shared stylesheet in public/.
2. Write one HTML file under public/, named after the page (a projects page becomes `public/projects.html`).
3. Start from `<!doctype html>`, link the stylesheet with `<link rel="stylesheet" href="/style.css">`, and set a `<title>`.
4. Use one `<h1>`, group sections under `<h2>`, and reuse the shared header, nav, and footer so every page matches.
5. Add a link back to Home, and link the new page from the home nav.

Rules: plain static HTML, no framework, no client JS, one page per file. If a page needs an image, use a free placeholder from https://placekittens.com/ (e.g. `https://placekittens.com/400/300`) so the `<img>` never points at a missing file.

---
> Source: [crystian/skill-map](https://github.com/crystian/skill-map) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
