---
name: amethyst-intro
description: > Use when this capability is needed.
metadata:
  author: Wayn-Git
---

# Introducing AMETHYST

Use this skill when the user wants to know what the system can do, or when
something appears misconfigured and you need to diagnose it.

## Establishing the current state

Run `amethyst doctor` with `run_shell_command` (read-only, so it will not prompt).
It reports the AMETHYST home directory, whether the database exists, which model
providers are configured, how many tools are registered, how many skills loaded
and which failed validation, and whether an OS sandbox is available.

Read the output before answering. Do not describe capabilities the doctor output
contradicts — if no providers are configured, say so rather than listing what
AMETHYST could do once one is.

## Explaining the system

AMETHYST reaches the user's world through four kinds of thing, and the distinction
matters when explaining what is possible:

- **Tools** are single actions AMETHYST performs directly: reading and writing
  files, searching them, running shell commands, opening applications, creating
  tasks and calendar events.
- **Skills** — like this one — are procedures written in markdown that combine
  existing tools. They add no new capability; they encode how to use what is
  already there.
- **MCP servers** are external processes providing tools AMETHYST did not write.
- **Integrations** connect an external account such as Gmail or Calendar, and
  own its credentials and sync.

## Explaining the permission model

If the user asks why they are being prompted:

Every tool has a fixed risk level. Low-risk reads run without asking. Writes and
anything outward-facing ask first. Anything touching credential directories asks
regardless of prior approval, and cannot be silenced. Choosing "always" for an
operation records that preference; `amethyst logs` shows every tool call with the
decision that allowed it.

## Diagnosing a failure

1. `amethyst doctor` first, always.
2. If a tool failed, check `amethyst logs --limit 10` for the recorded error.
3. If the sandbox is unavailable, that is expected on Windows and on Linux
   without bubblewrap installed — shell commands then run in direct mode and
   always ask for confirmation. Say this plainly rather than treating it as a
   fault.

---
> Source: [Wayn-Git/Amethyst](https://github.com/Wayn-Git/Amethyst) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
