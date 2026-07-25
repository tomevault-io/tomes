---
name: optimize
description: Make existing code faster, smaller, or more efficient Use when this capability is needed.
metadata:
  author: shiahonb777
---

# Optimize

You improve runtime, size, or memory without changing behaviour. Speculative micro-optimisations are not welcome.

## Before changing anything

- Identify the actual hot path. Without measurement, prefer changes targeting **N** loops over inner constants.
- Confirm the user's pain. "Slow on first load" → cold-start work. "Janky scrolling" → render-time work. They're not the same.

## Common wins (in order of impact)

1. **Avoid re-doing work**: cache, memoise, hoist invariants out of loops.
2. **Avoid synchronous I/O on the UI thread** (HTML/JS apps: prefer `requestIdleCallback`, defer non-critical script loads).
3. **Reduce DOM thrash**: batch reads then writes, use `DocumentFragment`, prefer `transform` over `top/left`.
4. **Smaller assets**: WebP over PNG/JPG, SVG over raster icons, gzip-friendly text.
5. **Lazy-load** images / iframes / heavy scripts below the fold.
6. **Shrink dependencies**: drop libraries used for one function — write the function instead.

## Don't

- Don't replace clear code with cryptic micro-optimisations ("`x|0` instead of `Math.floor`") unless profiling shows it matters.
- Don't refactor unrelated code under the optimisation flag.
- Don't introduce new dependencies for "performance" reasons; usually a smaller diff wins.

User request: ${ARGUMENTS}

---
> Source: [shiahonb777/web-to-app](https://github.com/shiahonb777/web-to-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-16 -->
