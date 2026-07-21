# Cargo Readme

Read ./README.md for project background.

## Important: Test Fixtures Are Not Project Code

Subdirectories under `tests/` look like cargo projects but are **test input only**. Code, comments,
and Cargo.toml files in e.g. `tests/project-with-version/` do not apply to this project. Do not
treat them as project source.

## Project Index

- `src/config/` — Cargo.toml parsing, badge definitions, project metadata
- `src/readme/` — Doc comment extraction, processing, template rendering
- `src/helper.rs` — CLI helpers for file I/O, entrypoint resolution, template loading
- `tests/` — Integration tests (assert_cli) with fixture projects

## Debugging: Compiler Warnings Can Break Tests

Tests assert on exact stdout/stderr. New compiler warnings contaminate that output and cause
assertion failures. Fix the warning in source code — don't update test expectations to include
warning text. See commits a7d1d18 and 2d64b24 for prior examples.

## Policies

### Do Not Edit README.md Directly

README.md is generated output — this project *is* a readme generator. Edit the doc comments in
source files or `README.tpl` instead. Any direct edits to README.md will be overwritten.

### Dependencies

Use the least specific version possible in Cargo.toml — e.g. `0.4` not `0.4.23`, `1` not `1.2.3`.
Cargo resolves to the latest compatible version automatically, so patches and fixes flow in without
manual bumps. Cargo.lock still pins the exact build.

## Architecture: Layered Separation of Concerns

The codebase is organized as concentric layers. **Inner layers must not know outer layers exist.**

```text
┌─ CLI / helper.rs ───────────────────────────────────┐
│  Owns: file I/O, flags, stdin/stdout, entrypoint    │
│  May call: readme, config                           │
│                                                     │
│  ┌─ readme::generate_readme (mod.rs) ────────────┐  │
│  │  Owns: wiring the pipeline stages together    │  │
│  │  May call: extract, process, template, config │  │
│  │                                               │  │
│  │  ┌─ extract / process / template ──────────┐  │  │
│  │  │  Each owns exactly one transformation   │  │  │
│  │  │  May call: nothing outside itself       │  │  │
│  │  └─────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────┘  │
│                                                     │
│  ┌─ config/ ────────────────────────────────────┐   │
│  │  Owns: Cargo.toml → Manifest struct          │   │
│  │  May call: nothing outside itself            │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

**Rules to preserve:**

- Data flows downward only: `helper.rs` > `readme::generate_readme()` > `config::get_manifest()`
- Pipeline stages are pure functions:
  - `extract` takes a `Read`
  - `process` takes `Vec<String>`
  - `template` takes a processed string plus a `Manifest`
- `config/` is self-contained
- Only `helper.rs` does real I/O

---
> Source: [webern/cargo-readme](https://github.com/webern/cargo-readme) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:agents_md:2026-07-21 -->
