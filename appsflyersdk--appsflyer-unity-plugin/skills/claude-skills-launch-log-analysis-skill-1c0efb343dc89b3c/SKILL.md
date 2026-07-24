---
name: launch-log-analysis
description: Analyze logs for a specific app launch and determine whether AppsFlyer initialization, start flow, callbacks, and expected events occurred correctly in the Unity plugin. Use when this capability is needed.
metadata:
  author: AppsFlyerSDK
---

# Launch Log Analysis

Use this skill when inspecting logs from one or more app launches.

## Goal

Analyze each launch separately and determine whether expected AppsFlyer SDK flows occurred.

## Workflow

1. Separate logs by launch/session if multiple launches exist.
2. For each launch inspect evidence for: SDK initialization (`initSDK`), SDK start (`startSDK`), conversion callbacks, deep link callbacks, in-app events, warnings or errors.
3. Compare expected vs actual behavior for that launch.
4. Detect: missing events, duplicate events, unexpected events, inconclusive evidence.
5. Produce a launch-by-launch report.

## Output Format

For each launch return:
- Launch number
- Platform
- Expected events
- Confirmed events
- Missing events
- Duplicate or unexpected events
- Relevant log evidence
- Final result: Passed | Failed | Inconclusive

## Rules

- Treat each launch separately.
- Do not merge evidence from different launches.
- Do not guess when logs are noisy or incomplete.
- Recommend additional logging if needed.

---
> Source: [AppsFlyerSDK/appsflyer-unity-plugin](https://github.com/AppsFlyerSDK/appsflyer-unity-plugin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
