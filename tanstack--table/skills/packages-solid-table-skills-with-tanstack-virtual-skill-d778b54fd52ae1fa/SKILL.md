---
name: with-tanstack-virtual
description: > Use when this capability is needed.
metadata:
  author: TanStack
---

This skill builds on `@tanstack/table-core#core`, `getting-started`, and `table-state`. Virtualize the final Table model in the renderer; Virtual is not a Table feature.

## Setup

```tsx
import { createVirtualizer } from '@tanstack/solid-virtual'

let scrollElement: HTMLDivElement | undefined
const rows = () => table.getRowModel().rows
const virtualizer = createVirtualizer({
  get count() {
    return rows().length
  },
  getScrollElement: () => scrollElement ?? null,
  estimateSize: () => 36,
  getItemKey: (index) => rows()[index].id,
  overscan: 5,
})
```

## Core Patterns

### Keep count reactive

```tsx
const virtualizer = createVirtualizer({
  get count() {
    return rows().length
  },
  getScrollElement,
  estimateSize,
})
```

### Apply measurement and geometry together

```tsx
<tr
  data-index={item.index}
  ref={(node) => virtualizer.measureElement(node)}
  style={{ position: 'absolute', transform: `translateY(${item.start}px)` }}
/>
```

## Common Mistakes

### HIGH Snapshotting row count

Wrong:

```tsx
createVirtualizer({ count: rows().length, getScrollElement, estimateSize })
```

Correct:

```tsx
createVirtualizer({
  get count() {
    return rows().length
  },
  getScrollElement,
  estimateSize,
})
```

The getter lets Solid Virtual track changes to the final row model.

Source: `examples/solid/virtualized-rows`

### HIGH Virtualizing raw data

Wrong:

```tsx
const rows = () => data()
```

Correct:

```tsx
const rows = () => table.getRowModel().rows
```

Raw data excludes Table's current sorting, filtering, grouping, expansion, and pagination.

Source: `docs/framework/solid/guide/virtualization.md`

### HIGH Separating ref lifecycle from virtualizer

Wrong:

```tsx
const scrollElement = document.querySelector('#rows')
const virtualizer = createVirtualizer({
  getScrollElement: () => scrollElement,
  count: 100,
  estimateSize,
})
```

Correct:

```tsx
let scrollElement: HTMLDivElement | undefined
const virtualizer = createVirtualizer({
  getScrollElement: () => scrollElement ?? null,
  get count() {
    return rows().length
  },
  estimateSize,
})
```

Keep the ref and virtualizer in the same owner so observers attach after JSX assigns the element.

Source: `examples/solid/virtualized-rows`

### HIGH Omitting renderer geometry

Wrong:

```tsx
<For each={virtualizer.getVirtualItems()}>
  {(item) => <tr>{rows()[item.index].id}</tr>}
</For>
```

Correct:

```tsx
<tbody
  style={{ height: `${virtualizer.getTotalSize()}px`, position: 'relative' }}
>
  <For each={virtualizer.getVirtualItems()}>
    {(item) => (
      <tr
        style={{
          position: 'absolute',
          transform: `translateY(${item.start}px)`,
        }}
      >
        {rows()[item.index].id}
      </tr>
    )}
  </For>
</tbody>
```

Virtual computes positions; the renderer must apply spacer size, transforms, widths, and sticky CSS.

Source: `examples/solid/virtualized-rows`

## API Discovery

Inspect `node_modules/@tanstack/solid-table/dist/index.d.ts` and installed `node_modules/@tanstack/solid-virtual/dist/`; use the maintained row, column, or infinite example for the matching CSS geometry contract.

---
> Source: [TanStack/table](https://github.com/TanStack/table) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
