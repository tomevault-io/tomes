---
name: test-runner
description: Run and triage Go tests with correct environment handling; produce compact, actionable failure summaries. Use when this capability is needed.
metadata:
  author: pilinux
---

# Test Runner

## When to Use

- Validate changes with unit/integration tests or triage failing test runs.

## Rules

- Use `source setTestEnv.sh` when environment variables are required.
- Focus on the first actionable failure line and include package + test name.
- Prefer targeted test runs (`-run`) over full-suite when iterating.

## Commands

- **Full suite (with test env):** `source setTestEnv.sh && go test -v -cover ./...`
- **Single package:** `source setTestEnv.sh && go test -v -cover ./lib/...`
- **Single test:** `source setTestEnv.sh && go test -v -run TestHashPass ./lib/...`

## Output

- **Result:** pass or fail.
- **Failures:** package, test name, first actionable error lines.
- **Next:** 1-3 focused suggestions (narrow test, inspect file, add mock).

## Related Skills

- `logs-repro-harness`, `linter-runner`, `db-infra-mocks`

---
> Source: [pilinux/gorest](https://github.com/pilinux/gorest) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
