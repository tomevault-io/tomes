---
name: csv
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# csv — skill0

Process CSV data: view, filter, convert, merge. Works with any tabular data source.

## Quick Start

```bash
# With x-cmd
x csv tab 1,3,6 < data.csv           # Show specific columns
x csv awk '{print $1, $3}' < data.csv # Process with AWK
x csv tojson < data.csv               # Convert to JSON
x csv merge2 id file2.csv < file1.csv # Merge by key

# Without x-cmd — use Python
python3 -c "
import csv, json, sys
reader = csv.DictReader(sys.stdin)
for row in reader:
    print(row['name'], row['value'])
" < data.csv

# Or use Miller (mlr), xsv, csvkit
```

## What's Available

| Command | Description |
|---------|-------------|
| `x csv tab <cols>` | Display selected columns |
| `x csv awk '{...}'` | AWK-style processing |
| `x csv tojson` | Convert to JSON |
| `x csv tojsonl` | Convert to JSON Lines |
| `x csv totsv` | Convert to TSV |
| `x csv merge2` | Merge two CSVs by key |
| `x csv header` | Operate on headers |
| `x csv app` | Interactive table viewer |

## Standalone Alternatives

- Python: `csv` module, `pandas`
- CLI: `mlr` (Miller), `xsv`, `csvcut`, `csvgrep`
- AWK: `awk -F, '{print $1}'`

## This skill0 grows

Starting with the essentials. Will add:
- Common CSV patterns
- Python/awk recipes
- Data cleaning tips

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
