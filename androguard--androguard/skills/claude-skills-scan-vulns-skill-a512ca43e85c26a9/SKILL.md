---
name: scan-vulns
description: Run Androguard vulnerability detectors on an APK and summarize findings Use when this capability is needed.
metadata:
  author: androguard
---

# /scan-vulns — Vulnerability scan

## Input

`$ARGUMENTS` — path to APK.

## Run

```bash
androguard -i "$1" --scan-vulns
```

```python
from androguard import Application
app = Application("app.apk")
for hit in app.scan_vulns():
    print(hit)
```

Requires `androguard[decompile]` (dex-decompiler detectors).

## Triage

For each hit:
1. Extract class / method / rule id from the detector output
2. Decompile the site: `--decompile-method '…#…'` or `--getclass`
3. Confirm true positive vs framework noise
4. Rate impact (info / low / medium / high) with a one-line rationale

## Report

Append a **Vuln scan** section to `workspace/reports/<package>-<date>.md` with confirmed items only (or clearly label unverified detector noise).

---
> Source: [androguard/androguard](https://github.com/androguard/androguard) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
