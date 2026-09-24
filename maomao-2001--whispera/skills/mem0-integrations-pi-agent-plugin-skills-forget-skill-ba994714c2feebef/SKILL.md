---
name: forget
description: Deletes memories by search query or memory ID with confirmation before removal. Use when removing outdated information, incorrect memories, sensitive data, or cleaning up after experiments. Use when this capability is needed.
metadata:
  author: maomao-2001
---

# Forget

Delete specific memories from Mem0.

## Execution

### Step 1: Parse input

The user provides either:
- A search query: `/mem0-forget travel plans`
- A memory ID: `/mem0-forget <memory_id>`

If no argument, ask: "What should I forget? Provide a search query or memory ID."

### Step 2: Find memories

**If memory ID provided** (looks like a UUID or hex string):
- Use `mem0_memory` tool with `action="search"` and the ID as query, or look it up directly.
- Show: `Found: "<memory content first 120 chars>" (created <date>)`

**If search query provided:**
- Use `mem0_memory` tool with `action="search"`, `query=<user's query>`.
- Show numbered list:
  ```
  Found <N> memories matching "<query>":
  1. <content, 120 chars> [<category>] [ID: <short_id>]
  2. ...
  ```

### Step 3: Confirm

Ask: "Delete which memories? Enter numbers (e.g., 1,3,5), 'all', or 'cancel'."

For a single memory ID, ask: "Delete this memory? [y/N]"

**Never delete without confirmation.** This is destructive.

### Step 4: Delete

For each confirmed memory, use `mem0_memory` tool with `action="delete"` and the memory ID.

### Step 5: Report

```
Deleted <N> memories.
```

If any deletions failed, report which ones and why.

---
> Source: [maomao-2001/Whispera](https://github.com/maomao-2001/Whispera) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
