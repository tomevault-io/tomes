---
name: verify-website
description: Verify changes under website/. Use when this capability is needed.
metadata:
  author: mufeedvh
---

# Verify website

From `website/`, run `pnpm install --frozen-lockfile` only when dependencies are missing
or package metadata changed, then run:

```bash
pnpm build
```

Check changed pages for broken links or routes, incorrect examples, navigation changes,
relevant localized copies, and visual regressions when layout or styling changed.

Do not commit `website/dist/`. Report build or environment failures explicitly.

---
> Source: [mufeedvh/code2prompt](https://github.com/mufeedvh/code2prompt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
