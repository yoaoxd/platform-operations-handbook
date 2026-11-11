# Deployment readiness and rollback

Use this checklist before a Kubernetes application release. Adapt thresholds to the service SLO and traffic; the examples are inspection commands, not an automated production deployment.

## Before deployment

- Record service owner, incident contact, target cluster/context, namespace, release commit, immutable image digest, and change window.
- Confirm the image exists, security checks passed, and configuration and secret references are present. Do not put secret values in change records.
- Check capacity, resource requests, quotas, disruption budgets, readiness/startup probes, and dependency health.
- Establish baseline request errors, latency, saturation, and business transaction success. Choose explicit abort thresholds and an observation window.
- Verify database migrations are compatible with both old and new application versions. A deployment rollback does not reverse database changes.
- Identify the previous working image/configuration and confirm the authorized rollback procedure.

## Inspect the target

Replace all placeholders and verify the current context before using these read-only commands.

```sh
kubectl config current-context
kubectl -n <namespace> get deployment <service>
kubectl -n <namespace> get pods -l app=<service>
kubectl -n <namespace> get events --sort-by=.metadata.creationTimestamp
kubectl -n <namespace> rollout status deployment/<service> --timeout=120s
```

A rollout being ready is necessary but does not prove that user requests work. Run an authenticated application smoke test and verify a representative business transaction. Avoid logging credentials or customer payloads.

## Abort and recover

1. Pause promotion if readiness fails, error/latency thresholds breach, or business verification fails. Record the timeline and evidence.
2. Determine whether the failure comes from application code, configuration, a dependency, or a migration.
3. For GitOps-managed services, revert the reviewed desired-state change and observe reconciliation. Coordinate emergency manual changes with the controller owner so reconciliation does not undo recovery.
4. If the previous version is incompatible with the current database schema, use the migration-specific recovery plan rather than blindly rolling back.
5. Re-run smoke tests and compare metrics with the baseline through the defined observation window.

## Change evidence

Record before/after revisions, deployment and verification timestamps, dashboard links, smoke-test outcome, abort decisions, and follow-up owner. Never claim a successful release from a green deployment status alone.
