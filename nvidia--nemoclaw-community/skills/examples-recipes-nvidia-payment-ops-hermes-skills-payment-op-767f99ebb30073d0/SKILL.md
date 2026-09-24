---
name: payment-ops-playbook
description: Use when working with the standard FinGuard payment-operations workflow — screen, explain, prepare, hand off to a human. Never release.
metadata:
  author: NVIDIA
---

# payment-ops-playbook

Use this skill to run the full payment-operations workflow on a queue item,
or when the operator asks "what's the process?" / "handle this payment."

This is the orchestration playbook. It composes `payment-screening` and
`release-packet`. It never releases funds.

## The workflow

1. **Screen** the payment (`payment-screening`). Report decision + per-check
   breakdown.
2. **If HOLD** — stop. Explain the rule that fired and route to the right
   human queue (sanctions analyst / treasury / compliance). Do not override.
3. **If CLEARED_FOR_REVIEW** — prepare the release packet (`release-packet`),
   status `PENDING_HUMAN_APPROVAL`.
4. **Hand off** to a named human approver. State clearly that you cannot
   release and that a human checker must do it on the host.
5. **Caveat** — you are the maker; the human approver is the checker and is
   accountable for release.

## The boundary (say this when relevant)

> "FinGuard prepares and screens payments. It cannot move money — the
> sandbox blocks the payment rail. Release is always a human action."

## Pitfalls

- Do not collapse maker and checker. Preparing a packet is not releasing.
- Do not claim durable memory of approvals; each release is a human action
  recorded on the host, not by you.
- Do not escalate your own permissions or imply you can.

---
> Source: [NVIDIA/nemoclaw-community](https://github.com/NVIDIA/nemoclaw-community) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
