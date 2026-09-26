---
name: inspecting-managed-skills
description: Inspect TraceDecay-managed skill proposals, activation, run evidence, or Hermes bridge health. Use when this capability is needed.
metadata:
  author: ScriptedAlchemy
---

# Inspecting managed skills

Managed skills are profile-owned runtime artifacts, distinct from bundled plugin
skills. Inspect the exact skill or run through supported automation surfaces.
Artifact views verify advertised hashes; filesystem guesses and raw database
rows are not equivalent evidence.

Separate proposal, validation, activation, deployment, and observed use. A
successful generation run does not prove that a host loaded the skill or that it
helped a task. Inspect terminal effects and operator overrides before explaining
an activation decision, and preserve failed or skipped states.

Hermes uses its standard home integration; do not invent a second home selector
or bridge authority. Inspect the supported bridge state without modifying host
files as a side effect of diagnosis. Current operation schemas define available
controls; this inspection workflow itself is read-only.

---
> Source: [ScriptedAlchemy/tracedecay](https://github.com/ScriptedAlchemy/tracedecay) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-23 -->
