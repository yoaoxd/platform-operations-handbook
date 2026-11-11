# Platform Operations Handbook

Practical runbook templates for engineers operating Kubernetes services. This repository focuses on deployment decisions, incident coordination, and evidence-based recovery verification.

## Runbooks

| Guide | Use when |
| --- | --- |
| [Deployment readiness and rollback](runbooks/deployment-readiness.md) | Preparing a release, defining abort criteria, or planning GitOps rollback |
| [Incident response and recovery verification](runbooks/incident-response.md) | Coordinating an outage and deciding whether a service has recovered |

## How to use

1. Copy the relevant template into your service documentation.
2. Replace placeholders with the actual owners, environment, dashboards, dependencies, SLOs, and recovery objectives.
3. Walk through the procedure in an isolated non-production environment and record observations.
4. Review the procedure with service owners before operational use and repeat verification after material changes.

## Scope and validation

These are reference documents, not an automated deployment system or evidence of a production-tested recovery plan. Example Kubernetes commands are read-only inspections and require a valid context and appropriate access. No cloud resources are provisioned by this repository.

The initial changes were checked for consistency and placeholder usage; commands were not executed against a cluster. Record your own validation results separately from hypothetical procedures.

## Contributing

Propose focused improvements through pull requests. Explain the operational problem, expected behavior, and validation performed. Credit actual collaborators accurately. Keep credentials, customer data, and private infrastructure details out of issues and examples.
