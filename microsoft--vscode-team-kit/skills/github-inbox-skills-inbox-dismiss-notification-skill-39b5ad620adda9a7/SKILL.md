---
name: inbox-dismiss-notification
description: Dismiss GitHub notification Use when this capability is needed.
metadata:
  author: microsoft
---

# Available Actions
Replace `{thread_id}` with the notification's `id` field.

## Mark as read
Notification will still render in inbox, but marked as read.
```
gh api --method PATCH /notifications/threads/{thread_id}
```

## Mark as done
Notification will be marked as done and removed from inbox, but doesn't unsubscribe from the thread.
```
gh api --method DELETE /notifications/threads/{thread_id}
```

## Unsubscribe from thread
Will no longer receive notifications from the thread.
```
gh api --method DELETE /notifications/threads/{thread_id}/subscription
```

# Dismiss notification
To fully dismiss a notification, unsubscribe and mark as done.
```
gh api --method DELETE /notifications/threads/{thread_id}/subscription
gh api --method DELETE /notifications/threads/{thread_id}
```


## Dismmiss multiple commands
Chain multiple commands together in a single terminal invocation using `&&` or `;` to avoid multiple confirmations.


# Rules
- **ALWAYS** prepend `GH_PAGER=cat` to `gh api` calls to avoid interactive pagers
- **NEVER** add other environment variable prefixes

---
> Source: [microsoft/vscode-team-kit](https://github.com/microsoft/vscode-team-kit) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
