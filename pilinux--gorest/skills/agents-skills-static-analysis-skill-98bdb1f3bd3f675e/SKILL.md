---
name: static-analysis
description: Run CI-aligned static analysis (vet, gosec, govulncheck) and convert findings into prioritized remediation steps. Use when this capability is needed.
metadata:
  author: pilinux
---

# Static Analysis

## When to Use

- Security or correctness checks are requested, or to reproduce CI static-analysis failures locally.

## Rules

- Use repository-standard tooling where configured.
- Summarize findings by severity and provide minimal remediation steps.
- Avoid suppressing issues unless instructed.

## Commands

- `go vet -v ./...`
- `gosec ./...`
- `govulncheck ./...`

## Cross-Platform Vet

CI runs vet on six OS/arch combos. Key examples:

- `GOOS=linux GOARCH=amd64 go vet -v ./...`
- `GOOS=darwin GOARCH=arm64 go vet -v ./...`
- `GOOS=windows GOARCH=amd64 go vet -v ./...`

## Output

- Findings grouped by tool and severity.
- For each: `path:line`, plain-language meaning, and a minimal fix suggestion.
- Verification: commands to re-run the specific tool.

## Related Skills

- `linter-runner`, `ci-orchestrator`

---
> Source: [pilinux/gorest](https://github.com/pilinux/gorest) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
