---
name: felt-construction
description: Use when constructing a `Felt` from a numeric value in Rust — avoid silently truncating values that may exceed the field modulus.
metadata:
  author: 0xMiden
---

# Felt Construction From Untrusted Numeric Inputs

## Rule

Do not call `Felt::new(x)` when `x` could exceed the field modulus. `Felt::new` silently truncates oversized values, which produces a valid-looking `Felt` that no longer equals the original input — a classic source of hard-to-attribute bugs.

Use one of:

- `Felt::from(x)` where `x` is a `u32` or smaller (infallible).
- `Felt::try_from(x)` for `u64`-and-larger inputs, returning `Result`.
- An explicit `assert!(x < Felt::MODULUS)` before `Felt::new(x)` if you have already proven the bound.

## Why

The field modulus sits just below `2^64`, so `Felt::new` truncates only for a narrow band of large values — most tests pass and production hits the bad input as a value mismatch far from the call. `Felt::from(u32)` cannot truncate and `Felt::try_from` forces the bound check.

## Examples

```rust
// Good: u32 input, infallible conversion
let f = Felt::from(slot_index as u32);

// Good: untrusted u64 input, checked conversion
let f = Felt::try_from(user_value).map_err(|_| Error::FeltOverflow)?;

// Bad: silent truncation on any value >= MODULUS
let f = Felt::new(user_value);
```

---
> Source: [0xMiden/protocol](https://github.com/0xMiden/protocol) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
