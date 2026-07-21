# agentdb

> **This tool coordinates Claude Code's actions. It does NOT write code or create content.**

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/agentdb/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# List Active Patterns

## 🎯 Key Principle
**This tool coordinates Claude Code's actions. It does NOT write code or create content.**

## MCP Tool Usage in Claude Code

**Tool:** `mcp__claude-flow__agent_list`

## Parameters
```json
{
  "swarmId": "current"
}
```

## Description
View all active cognitive patterns and their current focus areas

## Details
Filters:
- **all**: Show all defined patterns
- **active**: Currently engaged patterns
- **idle**: Available but unused patterns
- **busy**: Patterns actively coordinating tasks

## Example Usage

**In Claude Code:**
1. List all agents: Use tool `mcp__claude-flow__agent_list`
2. Get specific agent metrics: Use tool `mcp__claude-flow__agent_metrics` with parameters `{"agentId": "coder-123"}`
3. Monitor agent performance: Use tool `mcp__claude-flow__swarm_monitor` with parameters `{"interval": 2000}`

## Important Reminders
- ✅ This tool provides coordination and structure
- ✅ Claude Code performs all actual implementation
- ❌ The tool does NOT write code
- ❌ The tool does NOT access files directly
- ❌ The tool does NOT execute commands

## See Also
- Main documentation: /CLAUDE.md
- Other commands in this category
- Workflow examples in /workflows/

---
> Source: [ruvnet/agentdb](https://github.com/ruvnet/agentdb) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
