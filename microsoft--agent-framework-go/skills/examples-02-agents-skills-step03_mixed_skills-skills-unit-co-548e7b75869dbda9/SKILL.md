---
name: unit-converter
description: Convert between common units using a multiplication factor. Use when asked to convert miles, kilometers, pounds, or kilograms. Use when this capability is needed.
metadata:
  author: microsoft
---

## Usage

Use this skill when the user asks to convert between units.

1. Read `references/conversion-table.md` to find the factor for the requested conversion.
2. Run `scripts/convert.py` with `--value <number> --factor <factor>`.
3. Present the converted value clearly with both units.

---
> Source: [microsoft/agent-framework-go](https://github.com/microsoft/agent-framework-go) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
