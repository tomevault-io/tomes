---
name: anthropic-on-aws
description: Data Fetcher Skill Use when this capability is needed.
metadata:
  author: aws-samples
---

# Data Fetcher Skill

## Description
Fetches data from various sources for analysis.

## Parameters
- `source`: Data source (api, database, file)
- `query`: Query parameters

## Dependencies
None

## Usage
```python
result = fetch_data(source="api", query="sales_data")
```

## Output
Returns structured data ready for processing.

---
> Source: [aws-samples/anthropic-on-aws](https://github.com/aws-samples/anthropic-on-aws) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
