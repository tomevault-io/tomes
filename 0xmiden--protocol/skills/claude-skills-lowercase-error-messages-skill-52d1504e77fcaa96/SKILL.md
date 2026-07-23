---
name: lowercase-error-messages
description: Use when writing or editing a Rust error message, panic/assert string, or MASM `ERR_*` constant — follow the Rust convention for error-message casing and punctuation.
metadata:
  author: 0xMiden
---

# Lowercase Error Messages, No Trailing Punctuation

## Rule

Error messages (in `Error` enum `#[error("...")]` attributes, `panic!`, `assert!` messages, MASM `ERR_*` constant strings) follow Rust's convention:

- Start with a lowercase letter (unless beginning with a proper noun or acronym).
- No trailing period, exclamation, or other punctuation.
- Imperative or descriptive, not "ERROR: ..." or "Failed to ...".

Examples of correct shape: `"invalid account id length"`, `"note not found"`, `"failed to deserialize storage"`.

## Why

Error messages get composed into chains and contexts, where a capital letter or trailing period mid-chain makes them read like disconnected sentences. Lowercase-with-no-punctuation is the convention `std`, `thiserror`, and most crates already follow.

## Examples

```rust
// Good
#[derive(Debug, thiserror::Error)]
pub enum AccountError {
    #[error("invalid account id length, expected {expected} bytes, got {got}")]
    InvalidLength { expected: usize, got: usize },
    #[error("account not found")]
    NotFound,
}

// Bad
#[derive(Debug, thiserror::Error)]
pub enum AccountError {
    #[error("Invalid account id length: expected {expected} bytes, got {got}.")]
    InvalidLength { ... },
    #[error("Account not found!")]
    NotFound,
}
```

```masm
# Good
const ERR_NOTE_NOT_FOUND = "note not found"

# Bad
const ERR_NOTE_NOT_FOUND = "Note not found!"
```

---
> Source: [0xMiden/protocol](https://github.com/0xMiden/protocol) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
