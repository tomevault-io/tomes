---
name: auto-secure
description: 보안 감사 — OWASP Top 10 관점에서 변경 범위를 점검합니다 Use when this capability is needed.
metadata:
  author: autopus-ai
---

# auto-secure

## OMP Invocation

- `/auto secure ...`
- `/auto-secure ...`
- Load detail skill `auto-secure` for either entrypoint.

## 실행 계약

보안 감사 — OWASP Top 10 관점에서 변경 범위를 점검합니다

1. 대상 디렉터리와 전달된 인자를 확인합니다.
2. 요청 범위를 OWASP 관점으로 감사합니다.
3. 실행 가능한 finding과 검증 공백을 보고합니다.

---
> Source: [autopus-ai/autopus-adk](https://github.com/autopus-ai/autopus-adk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
