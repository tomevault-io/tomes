---
name: html-skills-stop
description: >- Use when this capability is needed.
metadata:
  author: f-labs-io
---

# html-skills-stop — tear down server mode

Pairs with `html-skills-listen`. Runs a bundled script that kills this session's receiver and removes its temp files, then stops the `Monitor` task whose id `html-skills-listen` saved.

## Steps

1. **Run the teardown script** with this session's id:

   ```bash
   bash "${CLAUDE_PLUGIN_ROOT}/skills/html-skills-stop/scripts/stop.sh" "${CLAUDE_SESSION_ID}"
   ```

   Output: `KEY=VALUE` lines. Always: `SID`, `STATUS`. When a Monitor was armed by `html-skills-listen` and saved, also: `MONITOR_ID`.

2. **If `MONITOR_ID` is printed, stop the Monitor task:**

   Call `TaskStop(task_id: "<MONITOR_ID>")`. If it fails because the task is already gone, that's fine — continue.

3. **Branch on `STATUS`:**

   - **`STATUS=WEB`** — Tell the user: `✓ html-skills server was inactive (web mode).`
   - **`STATUS=INACTIVE`** — Tell the user: `✓ html-skills server was already inactive — nothing to stop.`
   - **`STATUS=STOPPED`** — Tell the user: `✓ html-skills server stopped for this session.`

---
> Source: [f-labs-io/agent-html-skills](https://github.com/f-labs-io/agent-html-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
