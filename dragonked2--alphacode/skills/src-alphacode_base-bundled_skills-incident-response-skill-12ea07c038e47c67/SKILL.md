---
name: incident-response
description: Structured incident response: root cause analysis, rollback strategies, post-mortem templates, and prevention patterns. Use when this capability is needed.
metadata:
  author: dragonked2
---

# Incident Response Skill

Structured approach to handling production incidents.

## Response Process

1. **Detect** — identify the incident (alerts, user reports, anomalies)
2. **Triage** — assess severity and impact scope
3. **Mitigate** — stop the bleeding (rollback, feature flag, hotfix)
4. **Diagnose** — root cause analysis
5. **Remediate** — fix the underlying issue
6. **Review** — blameless post-mortem

## Rollback Strategy

- Feature flags for instant feature disable
- Database migration rollback scripts
- Blue-green deployment switch
- Traffic rerouting to healthy instances
- Cache invalidation if stale data is the issue

## Post-Mortem Template

- **Summary**: What happened, when, impact
- **Timeline**: Key events in chronological order
- **Root Cause**: Technical root cause analysis
- **Impact**: Users affected, duration, revenue impact
- **What Went Well**: Things that helped during response
- **What Went Wrong**: Things that slowed response
- **Action Items**: Concrete steps to prevent recurrence (with owners and dates)

---
> Source: [dragonked2/alphacode](https://github.com/dragonked2/alphacode) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
