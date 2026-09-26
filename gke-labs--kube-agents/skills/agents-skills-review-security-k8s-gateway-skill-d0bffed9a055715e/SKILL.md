---
name: review-security-k8s-gateway
description: Reviews Kubernetes Gateway API configs (Gateway, HTTPRoute, etc.) for security risks. Use when this capability is needed.
metadata:
  author: gke-labs
---
# Task
Review Kubernetes Gateway API configurations (`Gateway`, `HTTPRoute`, `TCPRoute`, `TLSRoute`, `ReferenceGrant`) for vulnerabilities.

# Checks
- **Route Hijacking**: Flag overlapping hostnames/paths in routes that allow hijacking critical traffic.
- **Cross-Namespace**: Flag routing or secret references across namespaces without narrow `ReferenceGrant`.
- **Listeners & TLS**: Verify TLS `mode` (`Terminate`/`Passthrough`) and secure certificate references.
- **Allowed Routes**: Require `allowedRoutes` to restrict attachment by namespace (e.g., `namespaces.from: Same` or `Selector`).
- **Permissive Hostnames**: Flag unnecessary wildcards (`*`) or overly broad hostnames in listeners/routes.

---
> Source: [gke-labs/kube-agents](https://github.com/gke-labs/kube-agents) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
