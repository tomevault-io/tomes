---
name: tool-selection-strategy
description: Use this skill when deciding which tools to call in an agentic workflow. Always choose the minimal, most direct tool for each step and avoid redundant or speculative tool calls.
metadata:
  author: aiming-lab
---

# Tool Selection Strategy

**Principles:**
- **Least tool principle:** Use the most specific, lightweight tool that accomplishes the goal.
- **Read before writing:** Always read a file before editing it to understand current state.
- **Avoid speculative calls:** Don't call a tool "just to see what happens". Have a clear hypothesis.
- **Parallelize independent calls:** If two reads don't depend on each other, fire them simultaneously.

**Decision heuristic:**
1. Can I answer this from memory/context? No tool call needed.
2. Is this a file operation? Use Read/Write/Edit tools.
3. Is this a code search? Use Grep/Glob tools.
4. Is this a system operation? Use Bash (last resort).

**Anti-pattern:** Using a heavy tool (Agent, Bash) when a lightweight dedicated tool suffices.

---
> Source: [aiming-lab/ClawArena](https://github.com/aiming-lab/ClawArena) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
