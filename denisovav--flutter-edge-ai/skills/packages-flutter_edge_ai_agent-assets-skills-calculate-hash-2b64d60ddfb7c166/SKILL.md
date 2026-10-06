---
name: calculate-hash
description: Calculate the hash of a given text. Use when this capability is needed.
metadata:
  author: DenisovAV
---

# Calculate hash

This skill calculates the hash of a given text.

## Examples

* "Calculate hash of..."
* "What is the hash of..."

## Instructions

Call the `run_js` tool with the following exact parameters:

- skillName: `calculate-hash`
- data: A JSON string with the following field
  - text: the text to calculate hash for

---
> Source: [DenisovAV/flutter_edge_ai](https://github.com/DenisovAV/flutter_edge_ai) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
