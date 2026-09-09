---
name: cloc
description: Get the number of lines of code for specific languages while excluding certain directories. Use when this capability is needed.
metadata:
  author: open-guji
---
To get the number of lines of code for Lua, TeX, and Python, excluding `.git`, `tests`, and `build` directories, use the following command:

// turbo
cloc . --exclude-dir=.git,tests,build --include-lang=Lua,TeX,Python

---
> Source: [open-guji/luatex-cn](https://github.com/open-guji/luatex-cn) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
