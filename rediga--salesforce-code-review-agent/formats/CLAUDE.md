# salesforce-code-review-agent

> This project uses the [Salesforce Code Review Agent](https://github.com/rediga/Salesforce-Code-Review-Agent).

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/salesforce-code-review-agent/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Salesforce DX — code review

This project uses the [Salesforce Code Review Agent](https://github.com/rediga/Salesforce-Code-Review-Agent).

When the user asks to review code, a PR, or a diff that includes Apex, LWC, Aura, Flows, or Salesforce metadata:

1. Follow `.cursor/skills/salesforce-code-review/SKILL.md`
2. Prefer the `salesforce-code-reviewer` subagent (read-only)
3. Return the report template (severity table, file:line, suggested fix)
4. Do not deploy or commit as part of the review

---
> Source: [rediga/Salesforce-Code-Review-Agent](https://github.com/rediga/Salesforce-Code-Review-Agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-10-06 -->
