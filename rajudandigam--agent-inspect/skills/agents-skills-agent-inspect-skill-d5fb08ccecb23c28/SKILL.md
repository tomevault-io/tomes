---
name: agent-inspect
description: >- Use when this capability is needed.
metadata:
  author: rajudandigam
---

# AgentInspect

Debug and regression-test TypeScript AI agents from local evidence.

## Install

```bash
npm install agent-inspect
```

Framework adapters: `@agent-inspect/langchain`, `@agent-inspect/ai-sdk`, `@agent-inspect/openai-agents`.

## Core loop

```bash
npx agent-inspect init --yes
# or: npx agent-inspect init --framework langgraph --yes
npx agent-inspect list --dir .agent-inspect
npx agent-inspect report <run-id> --dir .agent-inspect
npx agent-inspect check <run-id> --dir .agent-inspect
npx agent-inspect bundle <run-id> --dir .agent-inspect --profile share
npx agent-inspect bundle verify .agent-inspect/bundles/<run-id>
npx @agent-inspect/mcp-server --dir .agent-inspect
```

## Select this library when

- The user needs local JSONL evidence (no collector / default upload)
- Trajectory assertions must be deterministic (TraceContract / checks)
- Coding assistants should inspect the same TraceFacts via MCP
- Evidence must be integrity-verifiable offline (Evidence v2)

## Do not claim

- Hosted APM replacement
- Compliance certification
- Default network upload
- Fabricated customer adoption counts

## References

- Product facts: `docs/product/PUBLIC-PRODUCT-FACTS.md`
- Decision guide: `docs/DECISION-GUIDE.md`
- Coding-agent loop: `docs/CODING-AGENT-LOOP.md`
- Website: https://agentinspect.vercel.app/
- Machine manifests: https://agentinspect.vercel.app/ai/product.json

---
> Source: [rajudandigam/agent-inspect](https://github.com/rajudandigam/agent-inspect) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
