---
name: engineering-principles
description: GPT-RAG architecture and implementation principles. Use for design, review, meaningful refactoring, Azure integration, security, testing, or operational changes. Use when this capability is needed.
metadata:
  author: Azure
---

# GPT-RAG engineering principles

Load only the references needed for the task:

| When the task involves | Read |
| --- | --- |
| Repository purpose, boundaries, components, or Azure architecture | [GPT-RAG architecture](references/gpt-rag-architecture.md) |
| Tests, validation, compatibility, or evidence | [Testing and evidence](references/testing-and-evidence.md) |
| Identity, secrets, networking, retrieval security, or operations | [Security and operations](references/security-and-operations.md) |

Use these principles as design questions rather than dogma. The task
requirements, executable configuration, versioned contracts, and current
implementation remain the sources of truth.

---
> Source: [Azure/agent-landing-zone](https://github.com/Azure/agent-landing-zone) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
