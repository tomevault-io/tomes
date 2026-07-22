# oss-fuzz

> * Use python3 infra/helper.py to build projects and run fuzzers.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/oss-fuzz/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

* Use python3 infra/helper.py to build projects and run fuzzers.
* If doing development on infra/ you should use a venv and if it doesn't already exist, install deps from infra/ci/requirements.txt build/functions/requirements.txt with pip.
* If doing development on infra/ run python infra/presubmit.py to format, lint and run tests.

---
> Source: [google/oss-fuzz](https://github.com/google/oss-fuzz) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
