---
name: anthropic-on-aws
description: Report Generator Skill Use when this capability is needed.
metadata:
  author: aws-samples
---

# Report Generator Skill

## Description
Generates reports from processed data.

## Parameters
- `data`: Input data to process
- `format`: Output format (pdf, html, json)
- `template`: Report template to use

## Dependencies
None

## Usage
```python
report = generate_report(data=input_data, format="html", template="standard")
```

## Output
Returns formatted report in specified format.

---
> Source: [aws-samples/anthropic-on-aws](https://github.com/aws-samples/anthropic-on-aws) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
