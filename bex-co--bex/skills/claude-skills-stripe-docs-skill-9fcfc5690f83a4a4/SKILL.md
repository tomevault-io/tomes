---
name: stripe-docs
description: >- Use when this capability is needed.
metadata:
  author: bex-co
---

Use `stripe docs` instead of fetching [docs.stripe.com](https://docs.stripe.com/.md) content directly with `curl` or `WebFetch`.

- Fetches Markdown automatically
- Purpose-built for agents and terminal workflows

## Read a page by its web path

```bash
stripe docs /payments
```

## Search documentation by keyword

```bash
stripe docs search "payment intents"
```

## Look up API reference

```bash
# By resource name
stripe docs api product

# By HTTP method and path
stripe docs api GET /v1/products

# By event type
stripe docs api product.created
```

---
> Source: [bex-co/bex](https://github.com/bex-co/bex) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
