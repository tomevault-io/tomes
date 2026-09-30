---
name: adk-kotlin-agent-builder
description: >- Use when this capability is needed.
metadata:
  author: google
---

# ADK Kotlin Agent Builder

Checked against `main` after release 1.1.0 (September 2026).

The references teach patterns and the rules behind most failures; they are not an API listing. The API is close to adk-python but not identical. If a symbol does not resolve, read `core/src/*/kotlin/com/google/adk/kt/` (JVM- and Android-only APIs such as MCP and the persistent session services live outside `commonMain`) rather than guessing a neighbouring name. When a reference and the code disagree, the code is right.

## References

| Task | Reference |
| --- | --- |
| First agent, running it, reading events, streaming | [getting-started.md](references/getting-started.md) |
| The rules that cause most runtime failures | [best-practices.md](references/best-practices.md) |
| `@Tool`, hand-written tools, agent-as-tool, MCP, long-running and confirmation-gated tools | [tools.md](references/tools.md) |
| Sequential, parallel and loop agents, LLM transfer | [workflow-agents.md](references/workflow-agents.md) |
| Callbacks and plugins | [callbacks-and-plugins.md](references/callbacks-and-plugins.md) |
| State, sessions, artifacts, memory | [state-sessions-artifacts.md](references/state-sessions-artifacts.md) |
| Tests with a fake model | [testing.md](references/testing.md) |

For Java callers, copy the patterns in `examples/java/`, a javac-only module that keeps the Java surface working.

## Coming from adk-python

| Python | Kotlin |
| --- | --- |
| `LlmAgent(instruction="...")` | `LlmAgent(instruction = Instruction("..."))` |
| `FunctionTool(func)` | `@Tool` on the function (KSP generates the tool), or subclass `FunctionTool` |
| `tool_context.state[k] = v` | `context.updateState(k, v)`; read with `context.state[k]` |
| `ToolContext`, `CallbackContext` | `Context` |
| `BaseToolset` | `Toolset` |
| `LongRunningFunctionTool` | `isLongRunning = true`, or `@Tool(isLongRunning = true)` |
| `output_schema=MyModel` | `outputSchema = Schema(...)`, built by hand |
| `runner.run_async(...)` | `runner.runAsync(...)`, a `Flow<Event>` |
| `event.is_final_response()` | `event.isFinalResponse` |

---
> Source: [google/adk-kotlin](https://github.com/google/adk-kotlin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
