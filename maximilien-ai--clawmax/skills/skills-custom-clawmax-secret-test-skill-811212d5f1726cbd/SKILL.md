---
name: clawmax-secret-test
description: Verify that an explicitly authorized agent skill can use a brokered workspace secret without revealing the raw value. Use when this capability is needed.
metadata:
  author: Maximilien-ai
---

# ClawMax Secret Broker Test

Use this skill only when the user asks to verify brokered secret access.

Run:

```bash
clawmax-skill-run clawmax-secret-test check
```

Report `secretAvailable` and the returned one-way fingerprint. Never run environment-inspection commands, request the raw value, or claim the secret is available unless the command succeeds.

---
> Source: [Maximilien-ai/clawmax](https://github.com/Maximilien-ai/clawmax) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
