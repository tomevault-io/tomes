---
name: coach
description: >- Use when this capability is needed.
metadata:
  author: 3x-haust
---

# OMD-coach

```bash
omd coach
```

The CLI computes; you interpret. It reads `.omd/history.jsonl` (every `omd check` run) and
`decisions.md`, and reports recurring rules, trends, and overruled slop findings.

## How to read it to the user

- **Lead with the pattern, not the list.** "대비비 지적이 4런에 걸쳐 26건, -70% 개선 중"
  is data; "대비는 잡히기 시작했는데, 이제 위계 지적이 늘고 있다 — 다음 병목은 정보
  구조다"가 코칭이다.
- **Honesty is enforced, honor it.** Under four runs the tool refuses to claim a trend —
  do not invent one on top. A rule with no baseline prints "appeared", never a percentage;
  keep it that way in your prose.
- **Overrules are choices, not sins.** SLOP-GRADIENT overruled twice with a brand reason
  is a decision holding steady. The same overrule with "it looked fine" is a habit worth
  naming.
- **End with one thing to observe, not ten.** Pick the costliest recurring rule and give
  one concrete study: a reference to look at (`oh-my-design:scout` can fetch it measured) and what
  to notice there.

## The boundary

Never mix skill with taste. "You keep missing contrast" has a right answer; "you prefer
dense layouts" does not (professional designers agree at α = 0.248). Coach speaks only
about the first kind, and never reads `.omd/taste/`.

---
> Source: [3x-haust/oh-my-design](https://github.com/3x-haust/oh-my-design) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
