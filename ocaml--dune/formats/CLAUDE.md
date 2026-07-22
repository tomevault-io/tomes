# dune

> - Reuse helpers using setup scripts

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/dune/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Rules for Cram Tests

- Reuse helpers using setup scripts

- Utilities used inside of a test but are otherwise unrelated should be built
  outside of the test suite. See the `utils` directly for examples of such utilities

- To inspect direct output, lean towards using the trace using `$ dune trace cat`.

- Remove non-reproducible trace information using `$ jq`.

- Before adding new tests, search around the existing tests for duplicates and to find the best
  place to put this test.

- Do not use `--display short` unless it is the flag that is being tested.

---
> Source: [ocaml/dune](https://github.com/ocaml/dune) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
