---
name: debugging
description: Debugging conventions for pikru. Use when adding debug traces or investigating issues. Important rule - leave debug traces in place. Use when this capability is needed.
metadata:
  author: bearcove
---

# Debugging

When in doubt, add tracing:

- C code: `DBG()` macro
- Rust code: `tracing::debug!()` (not `eprintln!`)

## IMPORTANT: Leave debug traces in place!

- DO NOT remove `DBG()` calls from C code after debugging
- DO NOT remove `tracing::debug!()` calls from Rust code after debugging
- DO NOT run `make clean` in vendor/pikchr-c (it's disabled anyway)

## Rationale

- The C implementation is not used in production - debug traces are helpful for future investigations
- Rust tracing can be turned on/off at compile time via `RUST_LOG` environment variable
- Having traces in place makes future debugging much faster

---
> Source: [bearcove/dodeca](https://github.com/bearcove/dodeca) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
