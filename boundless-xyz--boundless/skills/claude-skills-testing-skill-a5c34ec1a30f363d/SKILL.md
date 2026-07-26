---
name: boundless
description: After completing non-trivial code changes, verify they are correct. Don't wait to be asked — if you made meaningful changes to Rust or Solidity code, run verification before reporting done. Use when this capability is needed.
metadata:
  author: boundless-xyz
---
# Verify Changes

After completing non-trivial code changes, verify they are correct. Don't wait to be asked — if you made meaningful changes to Rust or Solidity code, run verification before reporting done.

You can narrow test commands to just the crates/modules you changed (e.g. `cargo test -p broker --lib -- config::tests`), but follow the same patterns the justfile uses for flags and environment variables.

## What to run

1. `cargo fmt --all` — format first, always.
2. `just check-clippy-main` — clippy with `-Dwarnings`. This is what CI runs. Don't skip it.
3. Tests — pick based on what changed. Read the `justfile` for the canonical recipes. Common ones:
   - `just test-broker` — broker + boundless-market config tests
   - `just test-cargo` — full Rust test suite
   - `just test-foundry` — Solidity tests
   - Or run targeted: `RISC0_DEV_MODE=1 cargo test -p <crate> --lib -- <filter>`

## Before reading further

Read `testing/gotchas.md` in this skill directory. It lists environment and build pitfalls that cause false failures. If a test fails unexpectedly, check the gotchas before debugging.

---
> Source: [boundless-xyz/boundless](https://github.com/boundless-xyz/boundless) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
