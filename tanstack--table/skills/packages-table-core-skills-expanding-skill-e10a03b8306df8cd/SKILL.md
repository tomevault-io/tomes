---
name: expanding
description: > Use when this capability is needed.
metadata:
  author: TanStack
---

This skill builds on `core`, `table-features`, and `client-vs-server`. Expansion controls row-tree inclusion; the renderer owns disclosure controls and detail panels.

## Setup

```ts
import {
  createExpandedRowModel,
  rowExpandingFeature,
  tableFeatures,
} from '@tanstack/table-core'

type Node = { id: string; children?: Node[] }
export const features = tableFeatures({
  rowExpandingFeature,
  expandedRowModel: createExpandedRowModel(),
})
export const options = { getSubRows: (row: Node) => row.children }
```

## Core Patterns

```ts
const detailOptions = { getRowCanExpand: () => true }
const isDetailOpen = row.getIsExpanded()
```

For custom detail UI, render an additional row/panel when `isDetailOpen` is true.

## Common Mistakes

### [HIGH] Omitting the subrow accessor

Wrong: `const options = { data: nestedRows }`

Correct: `const options = { data: nestedRows, getSubRows: (row: Node) => row.children }`

Nested object structure is not inferred automatically.

Source: `docs/framework/react/guide/expanding.md#table-rows-as-expanded-data`

### [HIGH] Expecting detail markup from state

Wrong: `row.toggleExpanded(true)`

Correct: `if (row.getIsExpanded()) renderDetail(row.original)`

Table is headless and cannot render a custom detail panel.

Source: `docs/framework/react/guide/expanding.md#custom-expanding-ui`

### [HIGH] Misreading pagination placement

Wrong: `const options = { paginateExpandedRows: false }; const leafOnlyPages = true`

Correct: `const options = { paginateExpandedRows: false }; const descendantsStayWithParent = true`

This option controls whether expansion happens before or after pagination; it does not make page size count only leaf rows.

Source: `packages/table-core/src/features/row-expanding/rowExpandingFeature.types.ts`

## API Discovery

Inspect `node_modules/@tanstack/table-core/dist/features/row-expanding/` for expansion state, row APIs, and model placement.

---
> Source: [TanStack/table](https://github.com/TanStack/table) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
