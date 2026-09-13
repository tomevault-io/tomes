---
name: documentation
description: Update code2prompt documentation when public behavior or architecture changes. Use when this capability is needed.
metadata:
  author: mufeedvh
---

# Documentation

Update docs when a change affects public APIs, CLI flags/defaults/output, configuration,
template variables, feature flags, installation, or user workflows.

- Use `//!` for module purpose and boundaries.
- Use `///` for useful public API semantics, errors, or examples.
- Use inline comments only for non-obvious intent, constraints, or tradeoffs.
- Keep the root README, Python README, and website examples consistent with their surface.
- Update localized pages when in scope; otherwise report which copies may be stale.

Do not add comments that merely restate the code.

For changed CLI documentation, compare against:

```bash
cargo run --quiet -- --help
```

Run the relevant verification skill after documentation-sensitive changes.

---
> Source: [mufeedvh/code2prompt](https://github.com/mufeedvh/code2prompt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
