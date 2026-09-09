---
name: mcp-server-excel
description: Keep cross-repo publish hardening documentation accurate without overloading user-facing install docs. Use when this capability is needed.
metadata:
  author: sbroenne
---
# Publish Hardening Docs

## Purpose

Keep cross-repo publish hardening documentation accurate without overloading user-facing install docs.

## Pattern

1. Put operational details in maintainer docs first:
   - sync gates
   - version/tag guards
   - manual repair/replay entry points
   - auth/setup requirements
2. Keep user-facing docs to one honest sentence:
   - republish is automatic
   - the flow is gated/guarded
   - install UX is still client-specific
3. Preserve surface boundaries:
   - published plugin artifacts are broader than a single client
   - documented install commands should stay limited to verified client flows

## Apply When

- Updating release docs after workflow hardening
- Documenting cross-repo publish automation
- Explaining plugin artifacts versus client-specific install paths

---
> Source: [sbroenne/mcp-server-excel](https://github.com/sbroenne/mcp-server-excel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
