---
name: email-triage
description: Triage inbox into “needs reply”, “FYI”, “urgent”, and “safe to archive”, with a short plan for each. Use when this capability is needed.
metadata:
  author: clawdotnet
---

When asked to triage email:

1) Default to read-only / dry-run behavior unless explicitly asked to modify mailboxes.
2) If available, use `inbox_zero`:
   - Start with `analyze` (or `categorize`) to summarize categories and urgency.
   - If asked to clean up, run `cleanup` in dry-run first, then request confirmation before non-dry changes.
3) Produce a concise report:
   - Urgent (why + suggested reply)
   - Needs reply (draft 1–3 sentence reply)
   - Receipts/confirmations (extract key numbers/dates)
   - Newsletters/promotions (safe to archive)
4) If asked to email the report, send it via the `email` tool with a clear subject line.

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
