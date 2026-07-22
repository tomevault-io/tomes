# r3bl-open-core

> Files in this directory are **conformance test definitions** for the VT-100 PTY output parser.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/r3bl-open-core/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Test Data - Do Not Modify Code

Files in this directory are **conformance test definitions** for the VT-100 PTY output parser.
They contain precise ANSI escape sequence definitions that the test suite validates against.

**Do not** refactor, reformat, rename, or rewrite **code** in any file here. Changes to code
will break the conformance tests.

**Doc comments** (`///` and `//!`) may be updated to follow codebase documentation conventions
(e.g., escape sequence notation, link style, prose style) since they do not affect test behavior.

If you need to update a definition, do so intentionally as part of a test change - never as a
side effect of a codebase-wide refactor.

---
> Source: [r3bl-org/r3bl-open-core](https://github.com/r3bl-org/r3bl-open-core) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
