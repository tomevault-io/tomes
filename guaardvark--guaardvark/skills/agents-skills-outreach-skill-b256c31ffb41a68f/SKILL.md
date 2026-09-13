---
name: outreach
description: >- Use when this capability is needed.
metadata:
  author: guaardvark
---

# Outreach with Guaardvark (MCP tools, supervised)

Nothing here posts. Approval happens in the Studio's Outreach page, by design.

| tool | use |
|---|---|
| `outreach_status` | enabled / supervised / cadence / last run |
| `outreach_list_queue` | drafts, default `status='drafted'` (pending review) |
| `outreach_draft_post` | draft a comment or share post for a platform and thread URL; grounded in the user's indexed knowledge, graded, then queued |
| `outreach_reject_draft` | mark a draft rejected so it will not post |
| `request_publish` | ask to post the user's own announcement to one of their social connections; it waits on the Approvals page |

## Pattern

1. `outreach_status` to confirm the loop is on and supervised.
2. `outreach_draft_post` with the platform and the thread. Show the draft and its grade.
3. The user edits or approves in the Studio. You can reject on their word; you cannot approve.

## Rules

- Do not bulk-draft across many threads. The system is for keeping up with engagement on the
  user's own products and topics, not for volume.
- Say clearly that a draft is queued, not posted.

---
> Source: [guaardvark/guaardvark](https://github.com/guaardvark/guaardvark) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
