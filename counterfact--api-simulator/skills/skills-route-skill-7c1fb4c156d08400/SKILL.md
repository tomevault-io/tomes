---
name: route
description: > Use when this capability is needed.
metadata:
  author: counterfact
---

# Route Skill

## Purpose

Implement or update route behavior in generated route files.

## Required rules

- Use the `$` API in every handler (`$.path`, `$.query`, `$.body`, `$.response`,
  `$.context`, `$.loadContext`).
- Route handlers must stay thin.
- Business logic must be delegated to a context class in an appropriate
  `_.context.ts` file.
- Do **not** create unit tests in this skill; routes are HTTP adapters and
  behavior should be validated through context tests and black-box/integration
  flows when available.

## Step-by-step

1. Open the target file under `routes/` (e.g. `routes/pet/{petId}.ts`).
2. Read input using `$` (`$.path`, `$.query`, `$.body`).
3. Call a context method for logic/state changes.
4. Return a response using `$.response[status]`.
5. If needed, add new context methods instead of embedding logic in the route.

## Pattern

```ts
export const POST: HTTP_POST = ($) => {
  const created = $.context.createThing($.body);
  return $.response[201].json(created);
};
```

## References

- https://counterfact.dev/docs/features/state.html
- `src/server/dispatcher.ts` for runtime handler behavior

---
> Source: [counterfact/api-simulator](https://github.com/counterfact/api-simulator) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
