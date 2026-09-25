---
name: wp-security-review
description: WordPress security code review for Codex. Use when reviewing themes, plugins, or custom WordPress code for XSS, SQL injection, CSRF, auth gaps, unsafe uploads, dangerous functions, or insecure REST and AJAX handlers. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress Security Review

## Purpose

Use this skill when Codex should audit WordPress code for exploitable security issues and produce findings with file references, severity, and direct remediation guidance.

## Focus Areas

- XSS from missing output escaping
- SQL injection from unprepared database access
- CSRF gaps in forms, AJAX handlers, and state-changing flows
- Missing capability checks and authorization mistakes
- Unsafe file uploads and dangerous PHP functions
- REST and AJAX endpoints with weak permission controls

## Workflow

1. Identify public-facing, admin-only, AJAX, REST, and upload surfaces.
2. Check critical exploit paths first: SQL injection, public XSS, missing nonces on state-changing actions, and unsafe uploads.
3. Validate WordPress-specific security patterns such as nonce checks, capability checks, sanitization, and late escaping.
4. Load only the relevant reference docs from the shared security references.
5. Report findings with severity, file references, exploit impact, and a safe fix pattern.

## Reference Files

Load only the references you need from:

- `../../claude-skills/wp-security-review/references/vulnerability-patterns.md`
- `../../claude-skills/wp-security-review/references/nonce-csrf-guide.md`
- `../../claude-skills/wp-security-review/references/auth-patterns.md`
- `../../claude-skills/wp-security-review/references/escaping-guide.md`
- `../../claude-skills/wp-security-review/references/sanitization-guide.md`

## Output

- Use `CRITICAL`, `WARNING`, and `INFO`
- Include file references and affected surface area
- Name the WordPress security control that is missing or misused
- Recommend a secure replacement pattern

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
