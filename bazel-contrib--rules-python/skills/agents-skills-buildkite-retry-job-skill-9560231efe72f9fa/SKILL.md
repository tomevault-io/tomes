---
name: buildkite-retry-job
description: Retry a failed build kite job Use when this capability is needed.
metadata:
  author: bazel-contrib
---

Use `scripts/retry_buildkite_jobs.py` to retry a job. This is best used
when there are network failures.


example:

```
retry_buildkite_jobs.py org pipeline build
```
You can also simply pass a PR number or a direct Buildkite build URL.

The `--jobs` flag can be used to retry specific jobs.

---
> Source: [bazel-contrib/rules_python](https://github.com/bazel-contrib/rules_python) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
