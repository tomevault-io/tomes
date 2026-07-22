---
name: make-check
description: Run full pre-commit validation (fmt, lint, test, security) and report results Use when this capability is needed.
metadata:
  author: openfga
---

Run `make check` in the project root and report the results.

If any step fails, diagnose the first failure and suggest a fix. Do not proceed to later steps if an earlier one fails — focus on resolving the first issue.

The steps run by `make check` are:
1. `make fmt` — gofmt formatting
2. `make lint` — go vet + golangci-lint
3. `make test` — all tests with race detector
4. `make security` — gosec + govulncheck

---
> Source: [openfga/go-sdk](https://github.com/openfga/go-sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
