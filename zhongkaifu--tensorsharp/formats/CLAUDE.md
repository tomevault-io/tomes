# tensorsharp

> - Keep ggml upstream sources unchanged. Never add or apply ggml patches, rewrite

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/tensorsharp/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# External dependencies

- Keep ggml upstream sources unchanged. Never add or apply ggml patches, rewrite
  fetched ggml files, or make TensorSharp builds depend on a modified ggml tree.
- Implement behavior that ggml does not provide in TensorSharp-owned code,
  including native kernels and backend integration when necessary.
- Validate native changes against an unchanged upstream checkout. Record the
  dependency revision, actual test coverage, and benchmark limitations; do not
  count skipped or unavailable model/device scenarios as passing validation.

# Validation artifacts

- Keep generated validation logs, reports, and snapshots in ignored `docs/validation/`
  or `artifacts/`; do not force-add them to Git.
- Store reusable validation tools in `eng/` and required test fixtures in the
  relevant test project, outside the generated evidence directories.

---
> Source: [zhongkaifu/TensorSharp](https://github.com/zhongkaifu/TensorSharp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-30 -->
