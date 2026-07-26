---
name: problem-pattern
description: > Use when this capability is needed.
metadata:
  author: Dynatrace
---

You enable, disable, or verify one of EasyTrade's four problem patterns via the
`feature-flag-service`, and confirm the pattern produces its expected failure and a
Dynatrace problem card.

## Step 1 — Get flag IDs

```bash
curl -sf http://localhost/feature-flag-service/v1/flags/ | jq '.[] | {id, name, enabled}'
```

Pattern names: `DbNotResponding`, `ErgoAggregatorSlowdown`, `FactoryCrisis`, `HighCpuUsage`

## Step 2 — Enable a pattern

```bash
curl -X PUT "http://localhost/feature-flag-service/v1/flags/{flagId}/" \
  -H "accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{"enabled": true}'
```

Confirm: re-run Step 1 and check `"enabled": true` for the target flag.

## Step 3 — Verify expected behavior

| Pattern | What breaks | How to verify |
|---|---|---|
| `DbNotResponding` | No new trades — DB throws errors | POST to `/engine/v2/trades/buy` → expect 500/503 |
| `ErgoAggregatorSlowdown` | 2 aggregators slow; 40% traffic drop after 15–20 min | Watch `/aggregator-service` response times |
| `FactoryCrisis` | Credit card orders stall — third-party blocks | POST credit card order → no factory processing |
| `HighCpuUsage` | Broker-service slow + high CPU; K8s adds CPU limit | `kubectl top pod -n easytrade \| grep broker` |

## Step 4 — Check Dynatrace problem card

Use DQL to confirm Dynatrace detected the problem (run after the expected lag time):

```dql
fetch dt.davis.problems
| filter k8s.namespace.name == array("easytrade")
```

Or check via Dynatrace UI: **Problems** → filter by `easytrade` namespace.

## Step 5 — Disable pattern

```bash
curl -X PUT "http://localhost/feature-flag-service/v1/flags/{flagId}/" \
  -H "accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{"enabled": false}'
```

---
> Source: [Dynatrace/easytrade](https://github.com/Dynatrace/easytrade) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
