---
name: officecli
description: iOfficeAI/OfficeCLI executable on the MateClaw server Use when this capability is needed.
metadata:
  author: mateaix
---

# OfficeCLI advanced Office operations

This skill supplements MateClaw's native Office renderers. It never replaces them.

## Routing

| User intent | Use |
|---|---|
| Create a simple new document from Markdown | `renderDocx`, `renderXlsx`, or `renderPptx` |
| Inspect an existing Office file | `office_document(action="inspect")` |
| Validate OpenXML structure | `office_document(action="validate")` |
| Apply several structured changes | `office_document(action="batch")` |
| Fill an existing template's placeholders | `office_document(action="merge")` |
| Render for visual QA | `office_document(action="render")` |

## Safety contract

- `batch` and `merge` operate on a private copy and never overwrite the source.
- The tool only accepts `.docx`, `.xlsx`, and `.pptx` inputs inside the active workspace or current chat uploads.
- Do not install OfficeCLI from inside a chat. If the dependency is missing, explain that an administrator must install it on the MateClaw server.
- Do not fall back to arbitrary shell commands when `office_document` rejects an action.
- Return the generated markdown link verbatim so the user can download and preview the result.

## Operations

### Inspect

Use one of `outline`, `stats`, `issues`, `text`, or `annotated`:

```text
office_document(action="inspect", filePath="report.docx", mode="issues")
```

### Validate

```text
office_document(action="validate", filePath="workbook.xlsx")
```

### Batch edit

`payload` must be a non-empty OfficeCLI batch JSON array. Prefer stable element IDs returned by inspection over positional paths when available.

```text
office_document(
  action="batch",
  filePath="deck.pptx",
  payload="[{\"command\":\"set\",\"path\":\"/slide[1]/shape[@id=42]\",\"props\":{\"text\":\"Updated\"}}]",
  outputFilename="deck-updated.pptx"
)
```

### Template merge

`payload` must be a non-empty JSON object:

```text
office_document(
  action="merge",
  filePath="invoice-template.docx",
  payload="{\"client\":\"Acme\",\"total\":\"$5,200\"}",
  outputFilename="invoice-acme.docx"
)
```

### Render

Use `html`, `screenshot`, `svg`, or `pdf`. Prefer `screenshot` for visual QA.

```text
office_document(action="render", filePath="deck.pptx", mode="screenshot")
```

After rendering, inspect the returned preview before claiming that layout or formatting is correct.

---
> Source: [mateaix/mateclaw](https://github.com/mateaix/mateclaw) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
