---
name: mintlify-api
description: Interact with the Mintlify REST API to manage deployments, trigger builds, and query documentation site metadata programmatically. Use when this capability is needed.
metadata:
  author: jacred-fdb
---

# Mintlify API

Use the Mintlify API to manage documentation sites programmatically. This skill covers deployment management, build triggers, and site metadata queries.

## Authentication

All API requests require an API key passed in the `Authorization` header:

```
Authorization: Bearer <your-api-key>
```

Generate API keys from the [Mintlify dashboard](https://app.mintlify.com) under Settings > API Keys.

## Core capabilities

### Trigger deployments

Programmatically trigger a documentation rebuild when your codebase changes outside of Git push events.

### Query site metadata

Retrieve information about your documentation site including deployment status, configured domains, and navigation structure.

### Manage preview deployments

Create and manage preview deployments for pull requests and branches to review documentation changes before they go live.

## Resources

- [API reference](https://mintlify.com/docs/api)
- [Dashboard](https://app.mintlify.com)
- [Deployment guide](https://mintlify.com/docs/deploy)

---
> Source: [jacred-fdb/jacred](https://github.com/jacred-fdb/jacred) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
