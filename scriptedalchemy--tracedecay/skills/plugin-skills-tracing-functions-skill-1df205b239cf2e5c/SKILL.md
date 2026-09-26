---
name: tracing-functions
description: Trace callers, callees, or a call path between symbols, accounting for ambiguous names and indexed coverage. Use when this capability is needed.
metadata:
  author: ScriptedAlchemy
---

# Tracing functions

Resolve ambiguous names to exact symbols before following edges. Caller/callee
queries answer relationships; a text occurrence is not a call edge. Begin with
one direction and bounded depth, widening only when the question needs a longer
chain. Batch independent known nodes when the operation supports it.

Inspect trait-dispatch attribution and implementation bodies when the call passes
through an interface. Indexed resolution is not universal runtime coverage:
macros, dynamic dispatch, string-keyed calls, and public users outside the index
may need source or runtime evidence. Report the coverage gap instead of claiming
an empty graph proves no callers.

Call chains connect specified endpoints; rename preview provides broader
reference evidence for a proposed rename without applying it. Hand actual
mutations to `editing-safely`, and test/blast-radius questions to
`assessing-impact`. Keep returned node identities for scoped follow-up.

---
> Source: [ScriptedAlchemy/tracedecay](https://github.com/ScriptedAlchemy/tracedecay) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-23 -->
