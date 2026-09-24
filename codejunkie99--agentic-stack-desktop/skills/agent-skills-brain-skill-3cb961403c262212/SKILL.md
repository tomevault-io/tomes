---
name: brain
description: Recall and store durable cross-tool memory through the external Brain CLI. Use when this capability is needed.
metadata:
  author: codejunkie99
---

# Brain Integration

Use this skill when the task needs durable memory shared across coding-agent
harnesses through the external `brain` CLI and MCP server.

## Check Availability

```bash
python3 .agent/tools/brain_bridge.py status
```

If Brain is missing, tell the user to install it:

```bash
brew install codejunkie99/tap/brain
```

## Recall

Before non-trivial work that could depend on prior cross-tool decisions:

```bash
python3 .agent/tools/brain_bridge.py ask "<intent or topic>"
```

Use returned notes as context, but keep project-local `.agent/memory/semantic`
as the source for agentic-stack lessons until the user explicitly asks to
promote or migrate them.

## Save

Save one concise observation when the user gives a durable preference,
cross-project convention, or decision that should survive across harnesses:

```bash
python3 .agent/tools/brain_bridge.py note "<one durable observation>"
```

Do not save secrets, credentials, or ephemeral task details.

## MCP

To wire Brain as an MCP stdio server, inspect:

```bash
python3 .agent/tools/brain_bridge.py mcp-command
```

The expected command is `brain serve --mcp`.

---
> Source: [codejunkie99/agentic-stack-desktop](https://github.com/codejunkie99/agentic-stack-desktop) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
