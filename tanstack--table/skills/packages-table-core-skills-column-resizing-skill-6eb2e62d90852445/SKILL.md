---
name: column-resizing
description: > Use when this capability is needed.
metadata:
  author: TanStack
---

This skill builds on `core`, `table-features`, and `column-sizing`. Resizing supplies gesture APIs and state; the renderer supplies handles and widths.

## Setup

```ts
import {
  columnResizingFeature,
  columnSizingFeature,
  tableFeatures,
} from '@tanstack/table-core'

export const features = tableFeatures({
  columnSizingFeature,
  columnResizingFeature,
})
export const options = {
  columnResizeMode: 'onChange' as const,
  columnResizeDirection: 'ltr' as const,
}
```

## Core Patterns

```ts
const handler = header.getResizeHandler()
handle.addEventListener('mousedown', handler)
handle.addEventListener('touchstart', handler)
```

For large grids, compute all visible sizes once per update and expose them as CSS variables.

## Common Mistakes

### [CRITICAL] Omitting sizing prerequisite

Wrong: `tableFeatures({ columnResizingFeature })`

Correct: `tableFeatures({ columnSizingFeature, columnResizingFeature })`

Resizing modifies the sizing state and requires `columnSizingFeature`.

Source: `packages/table-core/src/types/TableFeatures.ts#FeatureSlotPrereqs`

### [HIGH] Rendering an inert handle

Wrong: `handle.addEventListener('pointerdown', header.getResizeHandler())`

Correct:

```ts
const handler = header.getResizeHandler()
handle.addEventListener('mousedown', handler)
handle.addEventListener('touchstart', handler)
```

The shipped handler distinguishes `touchstart` from the mouse path. A single
`pointerdown` listener does not provide working touch resizing; wire both mouse
and touch start events.

Source: `docs/framework/react/guide/column-resizing.md#connect-column-resizing-apis-to-ui`

### [MEDIUM] Reading sizes in every cell

Wrong: `cells.forEach(cell => cell.style.width = `${cell.column.getSize()}px`)`

Correct: `root.style.setProperty(`--col-${header.id}`, `${header.getSize()}px`)`

Caching sizes or CSS variables avoids repeated work during `onChange` resizing.

Source: `examples/react/column-resizing-performant/src/main.tsx`

## API Discovery

Inspect `node_modules/@tanstack/table-core/dist/features/column-resizing/` and the sizing feature directory for the state it updates.

---
> Source: [TanStack/table](https://github.com/TanStack/table) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
