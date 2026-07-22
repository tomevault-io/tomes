---
name: contribute-integration
description: Contribute a new or updated third-party framework integration for NeMo Relay Use when this capability is needed.
metadata:
  author: NVIDIA
---


# Contribute A Framework Integration

## Companion Guidance

Use `karpathy-guidelines` alongside this skill for implementation or review
work. Keep changes scoped, surface assumptions, and define focused validation
before editing.

Use this skill when contributing an integration with a framework or plugin such
as LangChain, LangGraph, Deep Agents, or OpenClaw through its public APIs.

## Default Guidance

- Keep NeMo Relay optional
- Use stable, documented framework or plugin APIs
- Wrap tool and LLM paths at the correct framework boundary
- Preserve the framework's original behavior when NeMo Relay is absent

## Checklist

- [ ] Integration pattern follows `docs/integrate-into-frameworks/adding-scopes.mdx`
- [ ] Integration uses public framework or plugin APIs
- [ ] Relevant integration tests or smoke path pass
- [ ] Docs updated if activation or usage changed

## References

- `docs/integrate-into-frameworks/about.mdx`
- `validate-change`

---
> Source: [NVIDIA/NeMo-Relay](https://github.com/NVIDIA/NeMo-Relay) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
