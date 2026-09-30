---
name: release-validation
description: Look up release verification records and compute release input checksums using the bundled validation script. Use when this capability is needed.
metadata:
  author: zhongkaifu
---

# Release validation fixture

For a release verification record, read `references/record.json` with
`skills_read` and return the requested record field exactly.

For an input checksum, use `skills_run` with path `scripts/check.py` and the
requested input as its single argument. Return the script's stdout exactly.
If execution is refused by the sandbox, state that refusal; do not claim the
script ran and do not calculate a replacement answer.

---
> Source: [zhongkaifu/TensorSharp](https://github.com/zhongkaifu/TensorSharp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
