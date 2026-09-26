---
name: review-security-k8s-understand
description: Analyzes Kubernetes project architecture and resources to build context before performing specific security reviews.
metadata:
  author: gke-labs
---
# Task
Analyze the Kubernetes project/repository to build comprehensive architectural and security context for specialized review agents.

# Checks
- **Architecture**: Identify main components, workloads, and architecture.
- **Docs**: Read `README.md`, diagrams, or architecture docs.
- **Categorization**: Explicitly categorize workloads as either *Infrastructure* (e.g., CSI drivers, ingress controllers) or *Application* (e.g., web APIs, DBs, etc).
- **Compensating Controls**: Explicitly note global security mechanisms (e.g., Service Mesh enforcing mTLS, global OPA/Gatekeeper policies, etc).

# Output
Output a concise summary of project purpose, workload categories, and compensating controls.

---
> Source: [gke-labs/kube-agents](https://github.com/gke-labs/kube-agents) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
