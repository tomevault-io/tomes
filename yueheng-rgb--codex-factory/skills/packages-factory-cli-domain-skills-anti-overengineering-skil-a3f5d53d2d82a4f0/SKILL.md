---
name: anti-overengineering
description: Keep project architecture proportional to real scope. Use before architecture or implementation when a small project risks unnecessary services, queues, frameworks, or infrastructure. Use when this capability is needed.
metadata:
  author: yueheng-rgb
---

<!-- >>> CODEX_APP_FACTORY:SKILL >>> -->
# Anti-overengineering

- Start with the smallest deployable monolith that completes the approved user path.
- Add microservices, queues, caches, multi-tenancy, payment complexity, or Kubernetes only when a stated requirement or measured limit justifies them.
- For every nonessential component, state the current need, simpler alternative, and removal decision.
- Preserve security, data integrity, error states, and verification; simplicity does not waive correctness.
<!-- <<< CODEX_APP_FACTORY:SKILL <<< -->

---
> Source: [yueheng-rgb/codex-factory](https://github.com/yueheng-rgb/codex-factory) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
