---
name: verification
description: Independent pre-completion verification orchestrator -- Reads upstream superpowers:verification-before-completion as baseline, layers personal rules (pre-claim gate / softening-language self-check). Use when this capability is needed.
metadata:
  author: Oscaner
---

# OS Verification

Pre-completion verification: evidence before assertion.

## Rules

### Rule: Read Upstream

Read upstream `superpowers:verification-before-completion` SKILL.md as the process baseline **when available** (resolution priority + unavailability fallback same as [Rule: Read Upstream](../brainstorming/SKILL.md#rule-read-upstream)). **Read, not Skill-invoke**.

### Rule: Pre-Claim Gate

Before any output that claims "done / fixed / passed", invoke the upstream verification process first (trigger timing = before the model internally decides "can say it's done", not post-output interception).

### Rule: Softening-Language Self-Check

Before output, scan for softening language: status claims ("should pass"/"looks good"/"appears correct"), evasion phrases. Found -> treat as unverified claim, supplement with evidence.

## Red Flags

- "Simple change doesn't need verification" -> pre-claim gate covers all flows (Rule: Pre-Claim Gate)

---
> Source: [Oscaner/skills](https://github.com/Oscaner/skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
