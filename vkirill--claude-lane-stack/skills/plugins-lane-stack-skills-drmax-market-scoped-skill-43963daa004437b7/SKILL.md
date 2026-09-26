---
name: drmax-market-scoped
description: DrMax Ultimate Market-Scoped Differentiation — split locales by market value, not translation. Use when: мультилокаль, hreflang, ru_RU vs ru_KZ, локали схлопываются, дифференциация рынков. SKIP: single-market RU site; cocoon IA (→drmax-cocoon-engine-x4); BrandCore facts (→drmax-brandcore). Use when this capability is needed.
metadata:
  author: VKirill
---

# Market-Scoped Differentiation

Only when there are **two or more locales** that must not collapse into a translation.

## Protocol

1. Open and apply **1:1**: [ORIGINAL.md](ORIGINAL.md)
2. Require topic/page type + locale list. Do not invent market facts — mark `[ТРЕБУЕТСЯ ПОИСК: …]` / legal/commercial checks from the original.
3. Brand-legal facts come from filled BrandCore, not from this prompt.

## Place in pipeline

```
BrandCore (if claims differ by market)
→ this skill (locale value map)
→ X4 per locale or locale-specific pages
```

---
> Source: [VKirill/claude-lane-stack](https://github.com/VKirill/claude-lane-stack) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
