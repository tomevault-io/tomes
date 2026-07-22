# weaverse

> Shopify Hydrogen integration layer for Weaverse visual page builder. Depends on `@weaverse/react` and `@weaverse/schema`.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/weaverse/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# @weaverse/hydrogen — Shopify Hydrogen Integration

Shopify Hydrogen integration layer for Weaverse visual page builder. Depends on `@weaverse/react` and `@weaverse/schema`.

## Structure

```
src/
├── weaverse-client.ts      # WeaverseClient class (909L)
├── WeaverseHydrogenRoot.tsx # Root React component (332L)
├── types.ts                # All type definitions (714L)
├── components/main.tsx     # Default wrapper component
├── hooks/                  # useWeaverseDataContext
└── utils/                  # getRequestQueries, getWeaverseConfigs, generateDataFromSchema
```

## Where to Look

| Task | Location |
|------|----------|
| Page data fetching | `weaverse-client.ts` → `loadPage()` |
| Theme settings | `weaverse-client.ts` → `loadThemeSettings()` |
| Component registration | `WeaverseHydrogenRoot.tsx` → `registerComponent()` |
| Props type | `types.ts` → `HydrogenComponentProps<L>` |
| Schema type | `types.ts` → `HydrogenComponentSchema` (alias for `SchemaType`) |
| Utility functions | `utils/index.ts` |
| Theme settings hook | `WeaverseHydrogenRoot.tsx` → `useThemeSettings()` |

## Key Classes

### WeaverseClient

Main client for fetching Weaverse data in Hydrogen routes.

```typescript
// In server.ts getLoadContext:
weaverse: createWeaverseClient({ storefront, request, env, cache, waitUntil })

// In route loader:
const weaverseData = await context.weaverse.loadPage()
```

**Multi-Project Support (v5.7.2+):**
```typescript
// Static (backward compatible)
projectId: 'my-project-id'

// Dynamic function
projectId: () => getProjectIdFromDomain(request.headers.get('host'))

// Priority chain: URL param > Function result > String value > Env var
```

**Caching:** Uses Hydrogen's `createWithCache`. Default: 10s short, 23hr stale-while-revalidate.

### WeaverseHydrogenRoot

Root component that renders the Weaverse content tree.

```typescript
// In app/root.tsx
<WeaverseHydrogenRoot components={components} errorComponent={ErrorComponent} />
```

**Props:**
- `components: HydrogenComponent[]` — Registered components
- `errorComponent?: React.FC` — Custom error UI

## Component Pattern

```typescript
import { createSchema, type HydrogenComponentProps } from '@weaverse/hydrogen'

export let MySection = forwardRef<HTMLDivElement, HydrogenComponentProps>((props, ref) => {
  let { children, loaderData, ...rest } = props
  return <div ref={ref} {...rest}>{children}</div>
})

export let schema = createSchema({
  type: 'my-section',
  title: 'My Section',
  settings: [
    { type: 'text', name: 'heading', label: 'Heading', defaultValue: 'Hello' },
  ],
})

export default MySection
```

## Types

| Type | Purpose |
|------|---------|
| `HydrogenComponentProps<L>` | Props passed to components (extends `WeaverseElement`, adds `children`, `loaderData`) |
| `HydrogenComponent` | Component definition: `{ default, schema, loader? }` |
| `WeaverseLoaderData` | Data from `loadPage()`: `{ configs, page, project, pageAssignment }` |
| `HydrogenPageData` | Page structure: `{ id, items, name, rootId }` |
| `RouteLoaderArgs` | Remix loader args with `weaverse` in context |
| `LoadPageParams` | Parameters for `loadPage()`: `{ type?, handle?, locale?, projectId?, strategy? }` |

## Utilities

| Function | Purpose |
|----------|---------|
| `getRequestQueries<T>(request)` | Parse URL query params with boolean coercion |
| `getWeaverseConfigs(request, env)` | Extract Weaverse config from env/URL |
| `generateDataFromSchema(schema)` | Extract default values from schema (memoized) |
| `getSelectedProductOptions(request)` | Filter Weaverse params from product options |

## Conventions (Package-Specific)

- **Route data key**: Must be `weaverseData` in loader return
- **Component registration**: Use `registerComponent()` from `WeaverseHydrogenRoot.tsx`
- **HOC pattern**: Wrap app with `withWeaverse()` for theme settings context
- **Cache isolation**: Multi-tenant apps must use unique `projectId` — included in cache keys

## Anti-Patterns

- **Don't** use `inspector` in schema → use `settings`
- **Don't** pass async `projectId` function directly → await first, then pass
- **Don't** forget to register components in `WeaverseHydrogenRoot`
- **Don't** mutate `loaderData` — it's shared across components

---
> Source: [Weaverse/weaverse](https://github.com/Weaverse/weaverse) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
