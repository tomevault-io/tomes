---
name: publish-registry
description: Publish @agentos-software/* registry packages from AgentOS. Use whenever the user asks to publish or release registry software/agent packages. Use when this capability is needed.
metadata:
  author: rivet-dev
---

# Publish AgentOS Registry Packages

Registry packages live in `agentos/registry` and publish as
`@agentos-software/*`. They version independently per package.

## Procedure

1. Build native command artifacts and package tarballs:

```bash
just registry-native
just registry-build [pkg]
just registry-status --remote
```

2. Bump the package's own `package.json` version and commit it.
3. Publish from AgentOS:

```bash
just registry-publish <pkg>         # dist-tag dev
just registry-publish <pkg> latest  # deliberate latest release
just registry-publish-all [tag]
```

## Rules

- Do not publish registry packages from agentos.
- Do not move `latest` unless the user explicitly asks for a release.
- Prefer AgentOS workspace builds while iterating; published pins are for
  consumers and release validation.

---
> Source: [rivet-dev/agentos](https://github.com/rivet-dev/agentos) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
