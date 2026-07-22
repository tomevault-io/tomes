# afterburn

> Run before submitting changes:

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/afterburn/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

@AGENTS.md

## Claude Code Specific Workflows

### Testing

Run before submitting changes:
```
cargo test --all-targets
cargo clippy --all-targets -- -D warnings
cargo fmt -- --check -l
```

### Adding a New Provider

Each provider lives in `src/providers/<name>/` and implements the `MetadataProvider` trait from `src/providers/mod.rs`. See existing providers (e.g., `src/providers/hetzner/`) for the pattern. Register new providers in `src/metadata.rs`.

### CI Files

Do NOT modify `.github/workflows/*.yml` or `.copr/Makefile` -- these are synced from `coreos/repo-templates`.

---
> Source: [coreos/afterburn](https://github.com/coreos/afterburn) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
