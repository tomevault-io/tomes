---
name: buildkite-get-results
description: Gets buildkite build results Use when this capability is needed.
metadata:
  author: bazel-contrib
---

Pass the PR number, Build URL, or Build ID to the `scripts/get_buildkite_results.py` script.

The `--jobs` flag can do glob-style filtering of jobs.

The `--download` flag will download job logs.

---
> Source: [bazel-contrib/rules_python](https://github.com/bazel-contrib/rules_python) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
