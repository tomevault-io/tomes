---
name: invoice-expense-review
description: Invoice and expense evidence and policy checks. Load after document-review. Use when this capability is needed.
metadata:
  author: Private-Garden-Labs
---

Extract parties, invoice/expense/order identifiers, dates, currency, quantity, rate, tax, subtotal, total, payment details, and approver. Recalculate amounts and totals.

Check duplicates, missing receipts/orders/approvals, party/date/amount conflicts, and supplied policy differences. Use `Possible duplicate` without proof of one transaction; use `not documented` for missing evidence.

Table: category; record identifier; source fact; location; supplied criterion; check. Do not approve payments or reject expenses.

---
> Source: [Private-Garden-Labs/garden-desk](https://github.com/Private-Garden-Labs/garden-desk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
