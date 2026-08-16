# vscode-abap-remote-fs

> Refer to [CONTRIBUTING.md](CONTRIBUTING.md) for full details on contributing to this project.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/vscode-abap-remote-fs/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# ABAP FS Development Guidelines

Refer to [CONTRIBUTING.md](CONTRIBUTING.md) for full details on contributing to this project.

## Workflow
1. Use TDD where possible.
2. Maintain project structure (monorepo).
3. Run `npm run format` after any modification.
4. Ensure CI passing (Node 24).

## Constraints
- No dynamic imports.
- No external network calls (SAP systems only).
- Keep functions short and early returns preferred.

---
> Source: [marcellourbani/vscode_abap_remote_fs](https://github.com/marcellourbani/vscode_abap_remote_fs) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-16 -->
