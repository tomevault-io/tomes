# stratus-red-team

> Stratus Red Team is a CLI tool and Go library that allows you to easily detonate granular, real-world cloud attack techniques.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/stratus-red-team/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Stratus Red Team

Stratus Red Team is a CLI tool and Go library that allows you to easily detonate granular, real-world cloud attack techniques.

## Guidelines for creating new attack techniques

When you need to create or update new attack techniques, use the `create-attack-technique` skill.

## Testing and developing locally

To run locally:
- `cd v2/`
- `go run cmd/stratus/*.go COMMAND` (e.g. `go run cmd/stratus/*.go list` or `go run cmd/stratus/*.go detonate aws.persistence.admin-iam-user`)

To run unit tests, run `make test`.

To automatically generate attack technique documentation, use `make docs`.

## DON'T

- Don't directly change auto-generated documentation in `docs/attack-techniques/`.

---
> Source: [DataDog/stratus-red-team](https://github.com/DataDog/stratus-red-team) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-20 -->
