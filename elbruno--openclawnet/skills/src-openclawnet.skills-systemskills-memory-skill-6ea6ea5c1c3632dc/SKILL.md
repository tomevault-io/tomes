---
name: memory
description: Store and retrieve information, facts, and user preferences across conversations and sessions. Use when this capability is needed.
metadata:
  author: elbruno
---

# Memory Skill

You have access to memory tools that allow you to store, retrieve, and remove information across conversations and sessions.

## Capabilities (shipped)

- **Store facts** — `remember` tool (`RememberTool`). Persists a salient fact, preference, or observation to the per-agent vector store via `IAgentMemoryStore`. Returns the new memory id.
- **Retrieve memories** — `recall` tool (`RecallTool`). Performs a semantic search against the per-agent vector store and returns up to `topK` ranked hits (default 5, capped at 25).
- **Forget memories** — `forget` tool (`ForgetTool`). Deletes a specific memory by id in the active agent scope.

## Not implemented

- **Update memories** — no dedicated tool. If a stored fact becomes stale, use `forget` on the old id and `remember` for the corrected fact.

## Guidelines

- Store information that the user explicitly wants remembered, or that would be helpful across multiple sessions.
- Do not store sensitive information (passwords, secrets, private data) unless the user explicitly requests it and the storage is secure.
- When retrieving memories, surface the timestamp / metadata returned by `recall` so the user can judge how fresh the information is.
- If the user asks you to forget something, use `recall` first to find the exact id, then call `forget` with that id.
- Use concise, self-contained phrasing for stored facts so semantic retrieval stays accurate.

---
> Source: [elbruno/openclawnet](https://github.com/elbruno/openclawnet) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-10 -->
