---
name: spreadsheets
description: Use for spreadsheet, workbook, Excel, CSV, and TSV tasks that require creation, editing, formula verification, data analysis, or visual QA. Use when this capability is needed.
metadata:
  author: OpenDataBox
---

# Spreadsheet workflow

Use this skill for `.xlsx`, `.xls`, `.csv`, and `.tsv` tasks.

## Authoring priority

1. If the Codex environment provides `load_workspace_dependencies` and
   `@oai/artifact-tool`, use that runtime for spreadsheet authoring and do not
   substitute global libraries.
2. Otherwise use `openpyxl` for workbook edits/creation and `pandas`/`numpy`
   for analysis and data transformation.
3. Keep user-visible calculations in workbook formulas whenever appropriate.

## Formula and visual QA

Use LibreOffice Calc to recalculate and render:

```bash
profile="$(mktemp -d)"
mkdir -p recalc pdf
soffice --headless "-env:UserInstallation=file://$profile" \
  --convert-to xlsx --outdir recalc output.xlsx
soffice --headless "-env:UserInstallation=file://$profile" \
  --convert-to pdf --outdir pdf recalc/output.xlsx
pdftoppm -png -r 144 pdf/output.pdf pdf/page
```

Check for formula errors (`#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`), truncated
columns, bad number formats, and broken charts before final delivery.

---
> Source: [OpenDataBox/Workspace-Bench](https://github.com/OpenDataBox/Workspace-Bench) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
