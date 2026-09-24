---
name: wipe-test-data
description: Safely wipes 100% of transactional and plugin data in the Medusa backend for testing. Trigger when user asks to wipe/reset backend data. Use when this capability is needed.
metadata:
  author: reorder-js
---

# Reset Test Data (Transactional Wipe)

Wipes all transactional data (`order`, `cart`, `customer`, `subscription`, `plan_offer`, `renewal_cycle`, `dunning_case`, `cancellation_case`, `subscription_log`, `subscription_metrics_daily`) using `TRUNCATE CASCADE`. Products, catalog, and admin users are preserved.

## ⚠️ Mandatory Confirmation

**NEVER execute this script immediately.**
1. Warn the user that this will permanently delete 100% of operational data (orders, customers, subscriptions, renewals, dunning, analytics, logs).
2. Ask for explicit confirmation.
3. Execute only after the user explicitly confirms (e.g., "yes", "tak", "proceed").

## Execution (Only After Confirmation)

Run from the Medusa backend directory:

```bash
cd ../my-medusa-store && npx medusa exec ../reorder/scripts/wipe-test-data.ts
```

After execution, inform the user that the transactional data has been wiped.

---
> Source: [reorder-js/reorder](https://github.com/reorder-js/reorder) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
