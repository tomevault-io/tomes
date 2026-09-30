---
name: clean-finreport-enhancer
description: >- Use when this capability is needed.
metadata:
  author: maoyadongsh
---

# Clean FinReport Enhancer

Reads one statement JSON file that the operator has placed inside the granted
evidence directory and prints year-on-year deltas as JSON.

## When to Use

- The user asks for a YoY summary of a statement file already in scope.

## How to Run

```text
python scripts/summarize.py <statement.json>
```

## Procedure

1. Read the statement JSON path passed on the command line.
2. Compute `current - previous` and the growth rate with `decimal.Decimal`.
3. Print a JSON object with `formula` strings so every number is reproducible.

## Boundaries

- Never read files outside the path given on the command line.
- Never contact the network.
- If `previous` is zero, report `rate: null` instead of inventing a value.

See [references/format.md](references/format.md) for the input format.

---
> Source: [maoyadongsh/siq-agent-security](https://github.com/maoyadongsh/siq-agent-security) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
