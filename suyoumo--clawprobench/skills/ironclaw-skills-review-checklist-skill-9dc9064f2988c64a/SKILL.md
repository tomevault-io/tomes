---
name: review-checklist
description: Pre-merge review checklist based on recurring AI reviewer feedback patterns Use when this capability is needed.
metadata:
  author: suyoumo
---

# Pre-Merge Review Checklist

Before merging, verify these items. They represent the most common issues caught by automated code reviewers (Copilot, Gemini) on IronClaw PRs.

## Database Operations
- [ ] Multi-step DB operations are wrapped in transactions (INSERT+INSERT, UPDATE+DELETE, read-modify-write)
- [ ] Both postgres AND libsql backends updated for any new Database trait methods
- [ ] Migrations are atomic (SQL execution + version recording in same transaction)

## Security & Data Safety
- [ ] Tool parameters are redacted via `redact_params()` before logging or SSE/WebSocket broadcast
- [ ] URL validation resolves DNS before checking for private/loopback IPs (anti-SSRF via DNS rebinding)
- [ ] Destructive tools have `requires_approval()` returning `Always` or `UnlessAutoApproved`
- [ ] Data from worker containers is treated as untrusted (tool domain checks, server-side nesting depth)
- [ ] No secrets or credentials in error messages, logs, or SSE events

## String Safety
- [ ] No byte-index slicing (`&s[..n]`) on external/user strings -- use `is_char_boundary()` or `char_indices()`
- [ ] File extension and media type comparisons are case-insensitive (`.to_ascii_lowercase()` before matching)
- [ ] Path comparisons are case-insensitive where needed (macOS/Windows filesystems)

## Trait Wrappers & Decorator Chain
- [ ] New `LlmProvider` trait methods are delegated in ALL wrapper types (grep `impl LlmProvider for`)
- [ ] New trait methods are tested through the full decorator/provider chain, not just the base impl
- [ ] Default trait method implementations are intentional -- wrappers that silently return defaults are bugs

## Tests
- [ ] Temporary files/dirs use `tempfile` crate, no hardcoded `/tmp/` paths
- [ ] Tests don't mutate global statics without synchronization (use per-test state or `serial_test`)
- [ ] Tests don't make real network requests (use mocks, stubs, or RFC 5737 TEST-NET IPs like 192.0.2.1)
- [ ] Test names and comments match actual test behavior and assertions

## Comments & Documentation
- [ ] Code comments match actual behavior (especially route paths, tool names, function semantics)
- [ ] Spec/README files updated if module behavior changed
- [ ] Error messages are clear and non-redundant (don't nest tool name inside tool error that already contains it)

---
> Source: [suyoumo/ClawProBench](https://github.com/suyoumo/ClawProBench) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
