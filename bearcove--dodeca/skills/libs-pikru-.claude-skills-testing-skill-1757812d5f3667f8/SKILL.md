---
name: testing
description: Testing conventions for pikru. Use when running tests to avoid timeouts. DO NOT run the full test suite. Use when this capability is needed.
metadata:
  author: bearcove
---

# Testing

**DO NOT** run the full test suite with `cargo test` - it times out and hangs.

Run specific tests only:

```bash
cargo test test01 -- --nocapture
cargo test test12 -- --nocapture
```

Never try to count/grep test results from the full suite - it will hang.

## Why This Matters

The pikru test suite runs pikchr rendering comparisons which can be slow. Running all tests at once exceeds reasonable timeout limits.

---
> Source: [bearcove/dodeca](https://github.com/bearcove/dodeca) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
