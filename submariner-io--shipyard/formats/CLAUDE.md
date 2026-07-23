# shipyard

> Development guidelines for the shipyard repository.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/shipyard/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# shipyard

Development guidelines for the shipyard repository.

## Commit Messages

@.agents/commit-templates.md

## Workflows

### Testing

#### Markdown

Run after editing any `.md` file, before committing:

```bash
make markdownlint
```

### CVE Fixes

@.agents/workflows/cve-fix.md

### Konflux Builds

On `devel`, `.rpm-lockfiles/` has documentation (`README.md`) and diagnostic scripts (`check-repo-access.sh`, `verify-packages.sh`).

---
> Source: [submariner-io/shipyard](https://github.com/submariner-io/shipyard) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
