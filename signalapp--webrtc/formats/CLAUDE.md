# webrtc

> @agents/prompts/common.md

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/webrtc/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# General workflow

@agents/prompts/common.md
@agents/README.md

# Searching Downstream

When auditing symbol usage or finding references in downstream projects, always
prefer high-precision CodeSearch filters over raw text searches:

- **Semantic References:** Use `usage:webrtc::SymbolName` to find actual
  call-sites.
- **Virtual Overrides:** Use `func:MethodName` to find overrides in downstream
  implementations.
- **Exclude WebRTC Mirrors:** Always append `-file:stable/webrtc` to focus on
  true downstream consumers.

# Codebase knowledge

@./g3doc/abseil-in-webrtc.md

@./g3doc/how_to_write_documentation.md

@./g3doc/implementation_basics.md

@./g3doc/style-guide.md

@./g3doc/testing.md

---
> Source: [signalapp/webrtc](https://github.com/signalapp/webrtc) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
