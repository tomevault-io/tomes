---
name: masm-named-literals
description: Use when writing or editing MASM or Rust code that contains meaningful numeric literals — promote them to named constants with a single source of truth.
metadata:
  author: 0xMiden
---

# Replace Magic Numbers with Named Constants

## Rule

Numeric literals embedded inline in MASM and Rust code must be promoted to named constants when they represent:

- Memory offsets, slot indices, or layout sizes
- Protocol/tag/type/version discriminants
- Domain values reused in more than one place

Define each constant exactly once. In MASM, declare it in the file's `CONSTANTS` section (see `masm-constants` skill). In Rust, define it as an associated constant on the type it describes (`Type::CAPACITY`, not a free-floating `const CAPACITY`).

## Why

A bare `47` or `0x1234` is invisible to grep, indistinguishable from coincidentally-equal numbers, and drifts when one occurrence is updated and another missed. A named constant documents intent and gives refactors a single source of truth.

## Examples

```masm
# Good
const ACCOUNT_DATA_PTR = 4
mem_load.ACCOUNT_DATA_PTR

# Bad
mem_load.4   # what is at offset 4?
```

```rust
// Good
impl AccountStorage {
    pub const MAX_NUM_STORAGE_SLOTS: usize = 255;
}

// Bad
if slots.len() > 255 { ... }   // 255 also appears unrelated elsewhere
```

---
> Source: [0xMiden/protocol](https://github.com/0xMiden/protocol) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
