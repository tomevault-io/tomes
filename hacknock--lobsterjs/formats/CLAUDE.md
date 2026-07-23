# lobsterjs

> This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/lobsterjs/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

lobster.js is an extended Markdown parser library. It parses Markdown (including lobster-specific syntax) into an AST, then renders rich HTML. The design principle is that the library provides document structure only — visual styling is entirely left to CSS.

Spec: `markdowns/spec.md` (English), `markdowns/spec-ja.md` (Japanese)

## Commands

This project uses **npm** (declared via `devEngines`; requires npm `>=11.10.0` for the `min-release-age` setting in `.npmrc`).

```bash
npm test           # Run all tests once (Vitest)
npm run test:watch # Run tests in watch mode
npm run build      # Build ESM bundle + emit .d.ts declarations
npm run build:docs # Build and copy dist/lobster.js → docs/lobster.js
```

To run a single test file:
```bash
npx vitest run tests/block-parser.test.ts
```

## Architecture

**Pipeline:** `parseDocument(markdown)` → `Document` AST → `renderDocument(doc)` → HTML string

The convenience function `toHTML(markdown)` combines both steps.

### Source layout

```
src/
├── core/
│   ├── types.ts          # All AST node type definitions (union types)
│   ├── block-parser.ts   # Block-level parser (entry: parseDocument, parseBlocks)
│   ├── inline-parser.ts  # Inline-level parser (entry: parseInline)
│   └── index.ts
├── renderer/html/
│   ├── renderer.ts       # AST → HTML string (entry: renderDocument)
│   └── dom.ts            # Browser API: renderToDOM, loadMarkdown, autoInit
└── index.ts              # Public API surface
tests/                    # Vitest tests (mirrors src/core/ and src/renderer/)
markdowns/                # Spec docs and test-case Markdown files
docs/                     # GitHub Pages demo site (lobster.js loads its own content)
```

### Parsing pipeline (block-parser.ts)

`parseDocument` runs in three passes:

1. **Pre-scan** (`collectDefinitions`): Extracts link definitions `[id]: url` and footnote definitions `[^id]: text` from all lines.
2. **Custom block extraction** (`extractCustomBlocks`): Pulls out `:::header`, `:::footer`, `:::warp id`, and `:::details Title` blocks before main parsing. Details blocks use a placeholder string mechanism to preserve position.
3. **Block parsing** (`parseBlocks`): Processes remaining lines via `tryParse*` functions in priority order: heading → horizontal_rule → code_block → blockquote → list → table → paragraph (fallback).

### Evaluation order (per spec)

```
header / footer / details (extracted before block parse)
  blockquote → list → heading → horizontal_rule → code_block → silent_table → table
    image → inline_footnote → footnote_ref → warp_ref → link → inline_link
      code_span → emphasis → strong → strikethrough
```

### Key types (types.ts)

- `Document`: `{ header?, footer?, body, linkDefs, footnoteDefs, footnoteRefs, warpDefs }`
- `BlockNode`: union of all block node types, discriminated by `type` field
- `InlineNode`: union of all inline node types, discriminated by `type` field
- `ParseContext`: shared mutable state during parsing (linkDefs, footnoteDefs, warpDefs, footnoteRefs, inlineFootnoteCount)

### HTML output conventions

All rendered elements carry `lbs-*` CSS class names (e.g. `lbs-heading-1`, `lbs-paragraph`, `lbs-code-block`, `lbs-table`, `lbs-table-silent`). No inline styles except for table cell alignment (`style="text-align:..."`).

Headings are rendered as `<hN class="lbs-heading-N">` (e.g. `<h1 class="lbs-heading-1">`).

### Browser API (dom.ts)

- `renderToDOM(doc, element)` — renders into a container element
- `loadMarkdown(src, element?)` — fetches a `.md` file and renders it
- `autoInit()` — auto-loads from `<script src="lobster.js" data-src="content.md">`

## Lobster-specific syntax

| Syntax | Description |
|--------|-------------|
| `:::header` ... `:::` | Page header region → `<header class="lbs-header">` |
| `:::footer` ... `:::` | Page footer region → `<footer class="lbs-footer">` |
| `:::details Title` ... `:::` | Collapsible block → `<details><summary>` |
| `:::warp id` ... `:::` | Named content block; referenced via `[~id]` |
| `~ \| ... \|` | Silent table (no border) → adds `lbs-table-silent` class |
| `\|` in table cell | Horizontal cell merge (colspan) |
| `\---` in table cell | Vertical cell merge (rowspan) |
| `![alt](url =WxH)` | Image with explicit width/height |

## Coding rules

- `src/core/` must be pure functions with no DOM/browser API dependencies.
- AST nodes use union types discriminated by `type` field.
- Comments should map implementation to the corresponding spec section.
- Each parser function should have corresponding Vitest tests.

---
> Source: [Hacknock/lobsterjs](https://github.com/Hacknock/lobsterjs) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
