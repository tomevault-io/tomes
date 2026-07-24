---
name: deploy-single-device
description: Deploy Terraform config to one Junos device. Use when user says deploy one device, run targeted plan, or push config to a particular device alias. Use when this capability is needed.
metadata:
  author: Juniper
---

Deploy Terraform config to a single target device safely.

## Inputs

- Terraform working directory
- Device identifier (resource address or provider alias)
- Optional custom plan filename

## Steps

1. Validate context
- Confirm current working directory contains Terraform files.
- Confirm provider endpoint and port are configured for the target alias.

2. Resolve target
- If user gives a hostname/alias, derive the Terraform resource address.
- If ambiguous, list candidate resources and ask user to choose.

3. Create targeted plan

```bash
terraform plan -target='<resource-address>' -out one-device.plan
```

4. Apply targeted plan

```bash
terraform apply one-device.plan
```

5. Verify post-apply

```bash
terraform state show '<resource-address>'
terraform plan
```

6. Report
- Summarize applied resource, endpoint used, and whether final full plan is clean.

## Guardrails

- Prefer saved plan files for targeted operations.
- Do not use `-auto-approve` unless user explicitly asks.
- If endpoint lookup/connectivity fails, stop and provide host/port remediation steps.

---
> Source: [Juniper/junos-terraform](https://github.com/Juniper/junos-terraform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
