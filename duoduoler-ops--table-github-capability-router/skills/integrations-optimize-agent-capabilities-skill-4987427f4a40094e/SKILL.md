---
name: optimize-agent-capabilities
description: >- Use when this capability is needed.
metadata:
  author: duoduoler-ops
---

# Optimize Agent Capabilities

Treat the repository's L0-L4 documents and templates as the source of truth. This Skill is an
optional execution entry, not a second routing specification.

## Workflow

1. Run the read-only inventory:

   ```bash
   node <skill-dir>/scripts/audit.mjs --json
   ```

2. Read only the matching profile in `profiles/`.
3. Classify every detected client:
   - `audit-only`: report findings and a client-specific plan; do not edit client configuration.
   - `unknown`: use the generic profile and do not infer configuration keys or paths.
4. Compare findings with the shared L0-L4 model and propose the smallest useful routing plan.
5. Report detected roots, counts, support boundaries, unsupported assumptions, and next steps.

## Safety

- This integration is read-only. Do not install, uninstall, enable, disable, or rewrite anything.
- Do not edit extension caches directly.
- Do not claim support from format similarity alone; client discovery and invocation controls differ.
- Preserve explicit invocation wherever the client supports it.
- Unknown clients receive a plan, not guessed mutations.

## Extending Clients

Add a profile first. A future PR may propose a write-capable adapter only when all five operations
are deterministic and tested: `detect`, `inventory`, `plan`, `apply`, and `verify`. See
`references/client-adapters.md`.

---
> Source: [duoduoler-ops/Table-GitHub-Capability-Router](https://github.com/duoduoler-ops/Table-GitHub-Capability-Router) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
