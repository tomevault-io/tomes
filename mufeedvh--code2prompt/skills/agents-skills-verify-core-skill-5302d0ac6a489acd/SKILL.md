---
name: verify-core
description: Verify changes under crates/code2prompt-core. Use when this capability is needed.
metadata:
  author: mufeedvh
---

# Verify core

Run from the repository root:

```bash
cargo test
cargo clippy --all-targets --all-features
```

If `entity-map` runtime behavior changed, also run:

```bash
cargo test --all-features
```

Check that presentation logic did not leak into core, ordering stays deterministic,
fallbacks and features still work, and changed behavior has a regression test when
practical. Report failed checks explicitly.

---
> Source: [mufeedvh/code2prompt](https://github.com/mufeedvh/code2prompt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
