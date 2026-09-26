---
name: code-health
description: Assess project or directory architecture, coupling, and structural test risk using TraceDecay evidence. Use when this capability is needed.
metadata:
  author: ScriptedAlchemy
---

# Code health

Start with the requested project's health dimensions, then investigate the weak
ones: cycles and depth for architecture, modularity and coupling for boundaries,
and test risk for poorly covered hubs. A score is a lead, not a finding; inspect
the implicated code and its callers.

Check indexed coverage before comparing scores. Unmounted files may look healthy
in the graph while no build root reaches them; inspect the real build or runtime
mount before calling them live or deleting them. Structural test links do not
prove execution coverage.

For before/after analysis, retain the generation- and path-bound `health_delta`
cursor. Compare the same scope and explain changed coverage rather than treating
a score increase alone as proof of better architecture.

---
> Source: [ScriptedAlchemy/tracedecay](https://github.com/ScriptedAlchemy/tracedecay) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-23 -->
