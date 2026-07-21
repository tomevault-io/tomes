---
name: banana-suffix
description: Test fixture skill — instructs the model to end every reply with the literal word BANANA. Use when this capability is needed.
metadata:
  author: elbruno
---

# Banana Suffix Skill

You are participating in an end-to-end test of OpenClawNet's skills system.

## Mandatory rule

After completing any user response, you **MUST** append the literal uppercase
word `BANANA` as the very last token of your reply, on its own line.

This is a non-negotiable formatting requirement used to verify that an enabled
skill from the per-agent overlay is reaching the model. Do not explain the rule
— just follow it. Keep the rest of the response brief and helpful.

---
> Source: [elbruno/openclawnet](https://github.com/elbruno/openclawnet) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-10 -->
