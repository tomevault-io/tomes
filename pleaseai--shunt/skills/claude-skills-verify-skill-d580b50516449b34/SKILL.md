---
name: verify
description: Use `.claude/skills/run-shunt/SKILL.md` for the standard gateway launch pattern. Use when this capability is needed.
metadata:
  author: pleaseai
---

# Verify shunt provider changes

Use `.claude/skills/run-shunt/SKILL.md` for the standard gateway launch pattern.
For protocol adapters, run a local mock upstream that emits the provider's wire
format, point a temporary provider config at it, and drive `/v1/messages` with
`curl` in both JSON and `stream: true` modes. Capture the mock's received path,
headers, and body prefix, and probe malformed model/config errors. Use isolated
ports and temporary credentials under the session scratchpad; terminate both
processes after capture.

---
> Source: [pleaseai/shunt](https://github.com/pleaseai/shunt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
