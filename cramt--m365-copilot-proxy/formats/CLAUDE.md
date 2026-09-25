# m365-copilot-proxy

> Working guidance for this repo lives in **[AGENTS.md](AGENTS.md)** — read it first.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/m365-copilot-proxy/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

Working guidance for this repo lives in **[AGENTS.md](AGENTS.md)** — read it first.

Start with the **Operating principles (read first)** and **How we work —
hypothesis-driven** sections. In short:

1. Always run sequentially — one thread at a time; the rate limit tracks
   threads-started, not messages, and masquerades as `Disengaged`.
2. Chase all hunches — tangents to test any idea are encouraged; test, don't guess.
3. The end goal is always a usable agent in **pi or openclaw**.
4. Be scientific: hypothesize → predict → test → conclude (log it in
   `docs/hypotheses.md`).
5. Prompt tinkering: try **N wildly different** strategies at once, A/B them in one
   bench sweep, and let the data pick the direction — never iterate on the first idea.

Protocol source of truth: [`docs/m365-copilot-api.md`](docs/m365-copilot-api.md).
Open-questions notebook: [`docs/hypotheses.md`](docs/hypotheses.md).

---
> Source: [cramt/m365-copilot-proxy](https://github.com/cramt/m365-copilot-proxy) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-24 -->
