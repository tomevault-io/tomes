---
name: data-fetching
description: description: Use when implementing data fetching with TanStack Query. Covers query keys, Use when this capability is needed.
metadata:
  author: olijboyd
---
---
  name: data-fetching
  description: Use when implementing data fetching with TanStack Query. Covers query keys,
  mutations, optimistic updates, and cache invalidation.
  ---

  # Data Fetching with TanStack Query

  ## When to Use
  - Adding new API data fetching
  - Implementing mutations with optimistic updates
  - Managing query cache invalidation

  ## Instructions
  1. Query keys follow the pattern: ["resource", id, filters]
  2. All queries use the shared queryClient from src/lib/query-client.ts
  3. Mutations must invalidate related queries on success
  4. Use optimistic updates for user-facing mutations
  5. Set staleTime to 5 minutes for dashboard data, 0 for user-specific data

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/olijboyd)
> Context snippets also available to append to your CLAUDE.md, GEMINI.md, and copilot-instructions.md — [download at TomeVault](https://tomevault.io/claim/olijboyd)
<!-- tomevault:4.0:skill_md:2026-04-07 -->
