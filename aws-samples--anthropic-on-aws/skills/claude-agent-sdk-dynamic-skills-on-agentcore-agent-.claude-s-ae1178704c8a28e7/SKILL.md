---
name: anthropic-on-aws
description: Data Analysis Workflow Use when this capability is needed.
metadata:
  author: aws-samples
---

# Data Analysis Workflow

## Description
Orchestrates a complete data analysis workflow using multiple skills.

## Dependencies
- `data-fetcher`: For retrieving source data
- `report-generator`: For creating final reports

## Workflow Steps
1. Fetch data using data-fetcher skill
2. Process and analyze the data
3. Generate report using report-generator skill

## Parameters
- `source`: Data source for fetching
- `query`: Query parameters for data fetching
- `report_format`: Final report format

## Usage
This is a meta-skill that coordinates other skills to complete a full analysis workflow.

## Example
```
Input: source="api", query="sales_2024", report_format="html"
Output: Complete HTML report with analyzed sales data
```

---
> Source: [aws-samples/anthropic-on-aws](https://github.com/aws-samples/anthropic-on-aws) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
