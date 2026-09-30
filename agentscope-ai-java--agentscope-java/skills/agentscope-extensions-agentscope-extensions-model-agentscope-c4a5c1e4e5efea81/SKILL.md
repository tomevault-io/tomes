---
name: data-transform
description: Use this skill when the task involves converting or reformatting structured data between file formats such as CSV, JSON, XML, or YAML. Suitable for tasks like "convert this CSV to JSON", "reformat my data file", or "change the file format of this dataset". Do NOT use for statistical analysis, aggregation, or report generation.
metadata:
  author: agentscope-ai-java
---
# Data Transform Skill

Converts structured data files between formats (CSV ↔ JSON ↔ XML ↔ YAML).

## Available Scripts

- `scripts/csv_to_json.py` — Convert a CSV file to JSON array format
- `scripts/json_to_csv.py` — Flatten a JSON array into a CSV file

## Usage

```
python3 scripts/csv_to_json.py --input data.csv --output data.json
python3 scripts/json_to_csv.py --input data.json --output data.csv
```

---
> Source: [agentscope-ai-java/agentscope-java](https://github.com/agentscope-ai-java/agentscope-java) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
