---
name: doubt-driven-development
description: Perform an adversarial, evidence-based challenge of a named high-risk cloakbrowser-mcp product or technical decision only when the user explicitly requests doubt-driven review, red-teaming of a decision, or a go/no-go challenge. Use for public contracts, upstream parity, process and HTTP isolation, unsafe browser capabilities, filesystem or network exposure, Docker sandboxing, dependencies, workflows, publishing, or irreversible migrations; do not use for routine uncertainty or ordinary code review. Use when this capability is needed.
metadata:
  author: swimmwatch
---

# Doubt-Driven Development

1. State the named decision, desired outcome, constraints, alternatives, and
   cost of being wrong.
2. Read `AGENTS.md` and inspect relevant code, tests, docs, dependencies,
   package metadata, images, and workflows. Use CodeGraph before broad source
   search when indexed. Separate evidence from assumptions.
3. Challenge upstream contract ownership, child-process and generated-config
   safety, stdio separation, Streamable HTTP session isolation, browser profile
   ownership, unsafe upstream tools, filesystem/network exposure, Docker
   sandbox assumptions, cross-platform compatibility, supply chain, operator
   burden, rollback, and artifact immutability where applicable.
4. For each material concern, provide a concrete failure scenario, affected
   contract, impact, evidence, detectability, recovery path, and smallest
   resolving experiment.
5. Do not invent measurements, threat actors, provider guarantees, workflow
   protections, or supported environments.
6. Use Prompt MCP only when the user must make a material choice between
   evidenced alternatives. Do not convert a recommendation into approval.

End with a recommendation, evidence confidence, unresolved risks, and explicit
conditions for proceeding, revising, experimenting, or deferring. Do not
implement, publish, or release from this workflow.

---
> Source: [swimmwatch/cloakbrowser-mcp](https://github.com/swimmwatch/cloakbrowser-mcp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
