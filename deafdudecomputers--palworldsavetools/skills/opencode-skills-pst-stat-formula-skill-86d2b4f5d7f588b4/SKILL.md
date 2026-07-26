---
name: pst-stat-formula
description: Game-verified Palworld pal stat calculation formulas (HP/ATK/DEF/WS) in src/palworld_aio/utils.py. Verified against in-game breakdowns on maxed test pals. Load when touching stat calculation, tooltips, or IV/rank/condenser math. Use when this capability is needed.
metadata:
  author: deafdudecomputers
---

# PST Stat Formula (Game-Verified)

Location: `src/palworld_aio/utils.py` — 5 `calculate_*` functions.

## Formula Structure
```
base        = additive_const + floor(scaling × K × level × (1+IV) × (1+condenser))
subtotal    = base + trust_bonus + awakening_bonus     # additive
final       = floor(subtotal × (1+soul) × (1+passive)) # multiplicative
```

## Per-Stat Formulas

| Stat | AD(K) | base | trust | awake |
|------|-------|------|-------|-------|
| **HP** | `500+5L`(0.5) | `floor(AD + hs×0.5×L×(1+IV))` | `int(L×FR×fh×0.65×(1+cb)+0.5)` | `floor(hs×L×0.065×(1+cb))` |
| **ATK** | `1.5L`(0.075) | `floor(AD + shot×0.075×L×(1+IV)×(1+cb))` | `floor(L×FR×f_shot÷10.2) + floor(L×FR×f_shot×cb÷10.2)` | `floor(shot×L×(1+IV)×0.009)` |
| **DEF** | `0.75L`(0.075) | `floor(AD + def×0.075×L×(1+IV)×(1+cb))` | `floor(L×FR×f_def÷10.2×(1+cb))` | `floor(def×L×(1+IV)×0.009)` |
| **WS** | — | `70+floor(cs×cb×L÷57)` if cond>1 else 70 | — | — |

Key: hs=hp_scaling, shot=shot_attack, def=defense, cs=craft_speed, L=level, IV=individual value 0-1, cb=condenser_bonus, FR=friendship_rank multiplier, fh=friendship_hp factor, f_shot/f_def=friendship attack/defense factors.

## What Changed (verified Jun 26 session)
- **HP trust:** `int(800×2.5×0.65+0.5) = 1300`
- **HP awake:** `floor(hs×L×0.065×(1+cb))` (was `floor(base_wc×0.089)`)
- **HP base:** removed `lucky_alpha` — boss multiplier already in BOSS_ data's hs
- **ATK/DEF trust:** divisor 8.6/8.5 -> 10.2, split `floor(x)+floor(x×cb)` to avoid float boundary
- **ATK/DEF awake:** scaling-based `floor(stat×L×(1+IV)×0.009)` (was base-based)
- **WS:** `70+floor(cs×condenser_bonus×L÷57)` (was always `cs×L//280`)

## Known ±1-2 Tolerance
- Trust formula: ±1 boundary cases at some friendship/level/condenser combos
- DEF awake Jetragon: 112 (game 111) — boundary float issue
- Anubis ATK: 2524 (game 2526) — pre-existing

## Stat Tooltip Feature
Custom QLabel popup (`Qt.Tool | Qt.FramelessWindowHint`) on HP/ATK/DEF/WS hover. Shows full breakdown: base, condenser, trust, awake, subtotal, souls, passives, final. Dark bg `rgba(18,20,24,0.98)`, blue border, rounded. Avoids QToolTip stylesheet inheritance issues on Windows.

## Display Rule
Always recalc from formula; `int()`->`round()` for soul/passive percentage display.

---
> Source: [deafdudecomputers/PalWorldSaveTools](https://github.com/deafdudecomputers/PalWorldSaveTools) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
