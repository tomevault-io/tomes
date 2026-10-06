---
name: history-explorer
description: Inspect recent session conversation turns and meta-run history. Returns structured JSON summaries of turn counts, role distribution, tool usage, meta-skill executions, and co-occurrence patterns. Use this before running meta-skill-creator or when the user asks about recent history, past tool usage, or session activity. Use when this capability is needed.
metadata:
  author: clawdotnet
---

# History Explorer

Read-only helper that inspects OpenClaw.NET session history for downstream
workflows (especially `meta-skill-creator`).

## What It Does

Parses a JSON session snapshot and returns structured analytics:

| Key | Description |
| --- | --- |
| `turns` | Turn count, role distribution (`user` vs `assistant`), time span, recent turn previews |
| `tools` | Tool invocation frequency, top tools, tool co-occurrence in the same turn |
| `meta_runs` | Meta-skill execution history: skill name, status, step counts, failure codes |
| `co_occurrences` | Skill/tool pairs that appear together across turns |
| `placeholder` | Emitted when no session data is available; downstream workflows treat this as a signal to rely on user intent only |

## Input Contract

The script expects JSON session data on **stdin**. The calling agent should pipe a
JSON object matching the `Session` schema — specifically:

```json
{
  "id": "session-guid",
  "history": [
    { "role": "user", "content": "...", "timestamp": "..." },
    { "role": "assistant", "content": "...", "timestamp": "...", "toolCalls": [...] }
  ],
  "metaRunHistory": [
    {
      "runId": "...", "skillName": "...", "status": "completed",
      "startedAtUtc": "...", "completedAtUtc": "...",
      "stepResults": [
        { "id": "...", "kind": "...", "status": "...", "durationMs": 123 }
      ]
    }
  ]
}
```

## Output Contract

Always returns a JSON object. When session data is available, includes the
requested analytics keys. When unavailable or unparseable, returns a single
`placeholder` key so downstream workflows degrade deterministically.

## When to Use

- Before running `meta-skill-creator`: feed co-occurrence and meta-usage data
  into the creator's proposal draft
- When the user asks "what skills did I use recently" or "show my session history"
- When debugging: inspect recent tool failures or meta-run error codes
- When the agent needs to recall conversation context from earlier turns

## Limitations

- Read-only; never mutates session state
- Depends on the agent passing session JSON via stdin; does not access the
  persistence layer directly
- `window_days` filtering is best-effort on the `timestamp` field
- Session snapshots may be truncated by the agent for token budget reasons

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
