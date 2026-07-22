---
name: openspec-feature-workflow
description: Standalone Codex workflow for OpenSpec proposal, design, specs, and tasks. Use when this capability is needed.
metadata:
  author: SYZ-Coder
---

# OpenSpec Feature Workflow

Use this standalone skill when the feature needs OpenSpec artifacts before implementation.

This is an explicit opt-in workflow. Do not use it by default. Only use it when the user explicitly asks for it, names `$openspec-feature-workflow`, or a repository policy explicitly requires it.

## Workflow

1. Derive or confirm a kebab-case change name.
2. Create the change under `openspec/changes/<change-name>/`.
3. Run `openspec status --change "<change-name>" --json`.
4. Before writing each artifact, run `openspec instructions <artifact> --change "<change-name>" --json`.
5. Complete artifacts in dependency order:
   - `proposal.md`
   - `design.md`
   - `specs/.../spec.md`
   - `tasks.md`
6. Re-run `openspec status --change "<change-name>" --json` until all required artifacts are ready.

## Guardrails

- Do not skip dependency order from OpenSpec status.
- Do not copy instruction metadata into artifact files.
- Do not start coding until required artifacts are ready.

---
> Source: [SYZ-Coder/superpowers-openspec-team-skills](https://github.com/SYZ-Coder/superpowers-openspec-team-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
