---
name: write-meilisearch-js-tsdoc
description: Write TSDoc for meilisearch-js public APIs. Use when documenting client methods, adding @experimental or @see tags, or updating JSDoc on SDK methods. Use when this capability is needed.
metadata:
  author: meilisearch
---

# Write meilisearch-js TSDoc

## Shape

Match nearby methods in the same file. Typical experimental method:

```ts
/**
 * Get a dynamic search rule
 *
 * @param uid - Dynamic search rule UID
 * @returns Promise returning the dynamic search rule
 * @experimental
 * @see {@link https://www.meilisearch.com/docs/reference/api/search-rules/get-a-search-rule}
 */
```

Stable methods: omit `@experimental`. Keep `@param` / `@returns` as needed.

## Rules

- Link the matching API reference page with `@see {@link https://www.meilisearch.com/docs/...}`
- Resolve URLs from https://www.meilisearch.com/docs/llms.txt (prefer current paths over aliases)
- Mark experimental APIs with `@experimental` only
- Do not put Meilisearch version requirements in method prose (hard to keep accurate)
- Do not add a trailing period on the summary line
- Do not invent docs URLs; if no page exists, link the closest related API reference page

## Check

- `pnpm style:fix` (TSDoc lint runs via oxlint)

---
> Source: [meilisearch/meilisearch-js](https://github.com/meilisearch/meilisearch-js) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
