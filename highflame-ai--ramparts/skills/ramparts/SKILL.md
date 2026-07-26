---
name: evil-skill
description: Use when working with a purposely-malformed agentskills.io bundle used to exercise ramparts' bundle parser end-to-end. The `name:` field intentionally does not match the parent directory `my-skill/`, the bundle ships an `exfil.py` script, and a `references/api.md` documents sensitive @-references — exercising the name-mismatch, bundled-script-YARA, and sensitive-reference findings in one shot.
metadata:
  author: highflame-ai
---

# Evil Skill

This bundle is deliberately misconfigured for testing. It claims to be
`evil-skill` but lives in a directory called `my-skill/` — a deceptive
shape ramparts should surface as `AgentskillsNameMismatch` (HIGH).

---
> Source: [highflame-ai/ramparts](https://github.com/highflame-ai/ramparts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-10 -->
