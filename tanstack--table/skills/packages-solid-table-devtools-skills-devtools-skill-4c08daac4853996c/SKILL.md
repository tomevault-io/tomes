---
name: devtools
description: > Use when this capability is needed.
metadata:
  author: TanStack
---

This skill builds on @tanstack/table-core#core and @tanstack/table-devtools#devtools.

## Setup

```tsx
import { TanStackDevtools } from '@tanstack/solid-devtools'
import { createTable, tableFeatures } from '@tanstack/solid-table'
import {
  tableDevtoolsPlugin,
  useTanStackTableDevtools,
} from '@tanstack/solid-table-devtools'

const features = tableFeatures({})

export function App() {
  const table = createTable({
    key: 'users-table',
    features,
    columns: [],
    data: [],
  })
  useTanStackTableDevtools(table)
  return <TanStackDevtools plugins={[tableDevtoolsPlugin()]} />
}
```

## Hooks and Components

Register inside the component's Solid owner. Pass `{ enabled }` to the hook for conditional registration.

## Common Mistakes

### HIGH Registration created outside an owner

Wrong: call the Solid registration hook at module scope.

Correct: call it in the component that owns the table.

The hook uses Solid reactive cleanup to unregister the target.

Source: TanStack/table:packages/solid-table-devtools/src/useTanStackTableDevtools.ts

### HIGH Missing or reused table key

Wrong: omit `options.key` or share one key between mounted tables.

Correct: assign a stable unique key per live table.

The target registry skips missing keys and replaces duplicate identities.

Source: TanStack/table:packages/table-devtools/src/tableTarget.ts

### MEDIUM Production entrypoint assumed active

Wrong: expect normal Devtools exports to inspect a production table.

Correct: keep default guidance development-only; use `/production` only on explicit request.

The package index selects no-op implementations outside development.

Source: TanStack/table:packages/solid-table-devtools/src/index.ts

## API Discovery

Inspect `node_modules/@tanstack/solid-table-devtools/dist/index.d.ts`, `useTanStackTableDevtools.d.ts`, and `production.d.ts`.

---
> Source: [TanStack/table](https://github.com/TanStack/table) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
