---
name: lazy-prefetch-pattern
description: Use the ChatJS React Query v5 lazy-prefetch pattern without blocking server rendering. Use when prefetching tRPC queries in Next.js Server Components or changing query dehydration and hydration behavior in apps/chat. Use when this capability is needed.
metadata:
  author: FranciscoMoretti
---

# Lazy prefetch pattern

Start optional server prefetches early without awaiting them so they can stream
through React hydration without blocking rendering.

- Use the exported `prefetch()` helper from `@/trpc/server`:
  `prefetch(trpc.foo.bar.queryOptions(...))`. It handles both paginated and
  non-paginated queries.
- Await only data required before rendering.
- Render through the existing `HydrateClient` or `HydrationBoundary`.

This depends on `trpc/query-client.ts` dehydrating pending queries and using
SuperJSON for serialization and hydration. Preserve those settings when using
this pattern.

---
> Source: [FranciscoMoretti/chat-js](https://github.com/FranciscoMoretti/chat-js) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-09 -->
