---
name: wp-ci-cd-and-release-engineering
description: WordPress CI/CD and release engineering review for Codex. Use when reviewing GitHub Actions, deployment scripts, artifact packaging, WordPress.org release flows, or rollback and environment promotion safety. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress CI/CD and Release Engineering Review

## Purpose

Use this skill when Codex should review how a WordPress plugin, theme, or related app is built, packaged, validated, and deployed.

## Focus Areas

- GitHub Actions and deploy gating
- Packaging and artifact reproducibility
- Secrets, environments, and promotion safety
- WordPress.org release mechanics and rollback readiness

## Workflow

1. Identify workflow files, release scripts, and artifact assembly logic.
2. Check artifact boundaries and production deploy protections first.
3. Review validation gates, secret exposure, and rollback readiness.
4. Load only the shared references needed from `../../claude-skills/wp-ci-cd-and-release-engineering/references/`.
5. Report findings with severity, file references, impact, and safer patterns.

## References

- `../../claude-skills/wp-ci-cd-and-release-engineering/references/github-actions-and-gating.md`
- `../../claude-skills/wp-ci-cd-and-release-engineering/references/packaging-and-artifacts.md`
- `../../claude-skills/wp-ci-cd-and-release-engineering/references/wordpress-org-and-rollbacks.md`

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
