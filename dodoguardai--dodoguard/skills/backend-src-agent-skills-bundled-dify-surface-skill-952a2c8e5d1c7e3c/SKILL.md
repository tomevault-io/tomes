---
name: dify-surface
description: Dify-specific wording and probe hints for task drafts. Use when this capability is needed.
metadata:
  author: dodoguardai
---

## Dify

When `surface` is Dify or the target is a Dify agent:

- Mention API base URL and app/workflow context only if the user provided them; do not guess endpoints.
- Prefer conversation-style tests when the user asks for multi-turn abuse cases.
- Call out prompt injection, tool misuse, and knowledge-base leakage as typical dimensions.

---
> Source: [dodoguardai/dodoguard](https://github.com/dodoguardai/dodoguard) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
