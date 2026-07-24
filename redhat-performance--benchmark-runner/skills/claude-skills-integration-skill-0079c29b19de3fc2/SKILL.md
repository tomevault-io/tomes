---
name: benchmark-runner
description: Run integration tests against a live OCP cluster. Use when this capability is needed.
metadata:
  author: redhat-performance
---
# /integration

Run integration tests against a live OCP cluster.

## Steps

1. **Run all integration tests**
   ```bash
   PYTHONPATH=. python3 -m pytest -v tests/integration/
   ```

2. **Run a specific workload test** (if args provided)
   ```bash
   PYTHONPATH=. python3 -m pytest -v tests/integration/benchmark_runner/workloads/test_oc_benchmark_runner.py -k "<workload_name>"
   ```

## Notes

- Requires a live OCP cluster with valid kubeconfig at `~/.kube/config`
- Tests create and delete real workloads on the cluster
- ODF-dependent tests are skipped on clusters without ODF

---
> Source: [redhat-performance/benchmark-runner](https://github.com/redhat-performance/benchmark-runner) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
