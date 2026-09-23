---
name: inbox-manage-subscription
description: Manage subscription for a GitHub notification thread Use when this capability is needed.
metadata:
  author: microsoft
---

# Manage Notification Subscription

## Ignore (mute) a thread

Stop receiving notifications for this thread:

```
gh api --method PUT /notifications/threads/{thread_id}/subscription -f ignored=true
```

## Watch a thread

Subscribe to receive notifications:

```
gh api --method PUT /notifications/threads/{thread_id}/subscription -f ignored=false
```

## Unsubscribe from a thread

Remove subscription entirely:

```
gh api --method DELETE /notifications/threads/{thread_id}/subscription
```

Replace `{thread_id}` with the notification's `id` field.

---
> Source: [microsoft/vscode-team-kit](https://github.com/microsoft/vscode-team-kit) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
