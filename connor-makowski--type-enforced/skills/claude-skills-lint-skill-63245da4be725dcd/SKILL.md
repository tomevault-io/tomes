---
name: lint
description: Format type_enforced/ and test/ with autoflake + black. Use when asked to format, lint, clean up style, prettify, or before committing Python changes. Use when this capability is needed.
metadata:
  author: connor-makowski
---

# Formatting

Run:

```
uv run python utils/prettify.py
```

This runs autoflake (strips unused imports) followed by black
(line-length=80, per `pyproject.toml`) over `type_enforced/` and `test/`.
Run it before committing any Python changes in this repo.

Make sure to run tests after formatting to make sure nothing breaks. If you see a test failure after formatting, flag it to the user and stop — wait for further instructions before proceeding.

---
> Source: [connor-makowski/type_enforced](https://github.com/connor-makowski/type_enforced) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
