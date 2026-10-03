# KubeRay Monthly Contribution Report: September 2026

- **Author:** [@wuallen57730](https://github.com/wuallen57730)
- **Period:** 2026-09-01 to 2026-10-11
- **Last updated:** 2026-10-03

## Summary

| Metric                         | Count                   |
| ------------------------------ | ----------------------- |
| PRs opened in this period      | 2                       |
| PRs merged in this period      | 3                       |
| Total PRs (opened or merged)   | **5**                   |
| Lines changed across these PRs | +1,308 / -42 (25 files) |
| Reviewed PRs                   | 0                       |
| Issues opened                  | 0                       |
| Issues picked up or discussed  | 5                       |
| Related PRs in ray-project/ray | 1 (merged)              |

## Pull Requests

### Merged

1. **[#5195](https://github.com/ray-project/kuberay/pull/5195) [Helm][Feat] Expose enableIngress and ingressOptions in the RayCluster chart**
   - Opened 2026-08-25, merged 2026-09-15. Closes [#5189](https://github.com/ray-project/kuberay/issues/5189).
   - KubeRay 1.7 added `headGroupSpec.ingressOptions` to the RayCluster CRD, but the `ray-cluster` Helm chart did not expose it. This PR adds `head.enableIngress` and `head.ingressOptions` to the chart so Helm users can create and customize the head dashboard Ingress. Both values are optional, and the default rendering is unchanged.

2. **[#5128](https://github.com/ray-project/kuberay/pull/5128) [History Server][CI] add unit tests for the lineage task summary**
   - Opened 2026-08-11, merged 2026-09-22. Closes [#5081](https://github.com/ray-project/kuberay/issues/5081).
   - Adds unit tests for `ToSummaryByLineage`, a follow-up promised in [#4469](https://github.com/ray-project/kuberay/pull/4469). The tests cover tree construction, actor grouping, sibling merging into `GROUP` nodes, recursive state count aggregation, sort order, and name fallbacks. No production code changed.

3. **[#5066](https://github.com/ray-project/kuberay/pull/5066) [RayCluster][CI] add e2e test for autoscaler scale-up with mTLS**
   - Opened 2026-07-31, merged 2026-09-22. Part of [#5048](https://github.com/ray-project/kuberay/issues/5048).
   - All worker pods share one cert-manager certificate whose IP SANs list the worker pod IPs, and the scale-up path that updates it had no e2e coverage. This PR adds `TestRayClusterTLSAutoscalerScaleUp`, which scales an mTLS cluster up twice with the autoscaler, checks that the new workers are covered by the certificate, then scales down and checks that removed pod IPs are dropped.

### Open (under review)

4. **[#5238](https://github.com/ray-project/kuberay/pull/5238) [History Server][CI] add unit tests for the list API filters**
   - Opened 2026-09-03. Part of [#5222](https://github.com/ray-project/kuberay/issues/5222).
   - Adds table-driven unit tests for query parameter parsing and filtering in `historyserver/pkg/utils/filter.go`. Coverage of `filter.go` goes from 0% to 98.8%, and coverage of `pkg/utils` goes from 27.3% to 46.2%.

5. **[#5363](https://github.com/ray-project/kuberay/pull/5363) [History Server] Bump Ray to 2.58.0 in examples and e2e test data**
   - Opened 2026-10-01. Part of [#5356](https://github.com/ray-project/kuberay/issues/5356).
   - Task logs did not show on the History Server task detail page with Ray 2.56, and Ray 2.58 fixes it. This PR bumps the Ray version in the History Server example YAMLs, e2e test data, and docs to 2.58.0, and updates the expected Grafana health response for the new dashboard UID. Verified by running the History Server e2e tests on kind.

## Reviewed PRs

None in this period.

## Other Contributions

### Related PR in ray-project/ray

- **[ray#66630](https://github.com/ray-project/ray/pull/66630) [Docs][History Server] Require Ray 2.58 for task logs** (merged 2026-10-02)
  - Updates the KubeRay History Server guide in the Ray docs to require Ray 2.58 or later. This is the docs side of [#5356](https://github.com/ray-project/kuberay/issues/5356), paired with #5363.

### Issue discussions and picked up work

- **[#5256](https://github.com/ray-project/kuberay/issues/5256) Make webhook and reconciliation validation logic consistent**: Picked up the issue and posted an implementation plan (2026-09-14). The plan reuses the reconcilers' `Validate*Spec` functions in the RayCluster, RayJob, and RayService webhooks. It also raises an open question about skipping validation when `deletionTimestamp` is set, so invalid objects can still be deleted.
- **[#4994](https://github.com/ray-project/kuberay/issues/4994) RayService worker `ray.io/serve` label**: Picked up the worker label part (2026-09-28). Proposed updating the label from the Serve API proxy status on each reconcile, which also covers the replica count case that [#4997](https://github.com/ray-project/kuberay/pull/4997) does not. Reproduction on kind is in progress.
- **[#5356](https://github.com/ray-project/kuberay/issues/5356) Set the Ray version to 2.58 in History Server examples**: Picked up the issue (2026-09-30) and delivered #5363 and ray#66630.
- **[#5222](https://github.com/ray-project/kuberay/issues/5222) History Server unit tests for uncovered functions**: Picked up the `pkg/utils/filter.go` item (2026-09-01) and delivered #5238.
- **[#5279](https://github.com/ray-project/kuberay/issues/5279) Move remaining History Server gosec exclusions into the permanent section**: Picked up the issue (2026-09-13).
