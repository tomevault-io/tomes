---
name: gstack-security
description: | Use when this capability is needed.
metadata:
  author: LowyShin
---

# Gstack Security Analysis (CSO)

> "Zero-noise, high-confidence security findings with concrete exploit scenarios."

## 1. Methodology: OWASP Top 10 + STRIDE

When performing a security scan, use the following frameworks to identify risks:

- **STRIDE**: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege.
- **OWASP Top 10**: Broken Access Control, Cryptographic Failures, Injection, Insecure Design, etc.

## 2. Zero-Noise Filtering

To ensure actionable findings, apply the following filters:

- **Independent Verification**: Every finding must be independently verified by tracing the code path.
- **Confidence Gate**: Only report findings with **8/10+ confidence**.
- **Exclude False Positives**: Ignore known false positives (e.g., test files, internal-only tools, etc.).

## 3. Exploit Scenario Requirement

Every security finding must include:

1. **Vulnerability Type**: (e.g., SQL Injection, XSS, CSRF).
2. **Impacted File/Line**: Precise location in the codebase.
3. **Exploit Scenario**: A concrete description of how an attacker could exploit this.
4. **Recommended Fix**: Specific code changes to mitigate the risk.

## 4. Usage Table

| Category | Action |
|----------|--------|
| `cso scan` | Run a full security audit on the current scope. |
| `threat model` | Generate a STRIDE threat model for the current feature design. |
| `exploit {finding}` | Generate a detailed exploit scenario for a specific finding. |


## ⚡ Optimization Integration
When using this skill for critical tasks, please run it within a /native-trace context to capture performance data for self-improvement via /aioptimize.


---
> Source: [LowyShin/giip-dev-agent](https://github.com/LowyShin/giip-dev-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
