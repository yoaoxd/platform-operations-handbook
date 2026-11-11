# Incident response and recovery verification

A practical template for a service outage. These are example procedures, not evidence of an actual incident or a production-tested recovery plan.

## First response

1. Confirm customer impact using application requests and business transactions; distinguish a monitoring failure from a service failure.
2. Record incident start and detection times in UTC, affected services, impacted users, and current symptoms. Preserve relevant logs with sensitive data removed.
3. Assign an incident lead, operations owner, and communications owner. One person may cover multiple roles on a small team; name a backup and escalation contact.
4. Inspect recent releases, configuration changes, dependency health, capacity, network paths, and certificate/authentication failures. Record hypotheses separately from observations.
5. Select the smallest reversible mitigation. Define its success signal, rollback method, owner, and observation window before making the change.

## Recovery gates

| Gate | Required evidence |
| --- | --- |
| Infrastructure | Capacity available; required nodes, storage, networking and dependencies healthy |
| Application | Ready workloads plus authenticated smoke tests and representative transactions |
| Data | Restore integrity, schema/constraint checks, expected records and measured missing transactions |
| Traffic | Errors, latency and saturation acceptable through the service-specific observation window |
| Ownership | Incident lead records recovery decision and owners for remaining risks |

A successful backup command does not prove recoverability. For database restoration, restore into an isolated target, preserve the damaged source, and verify data before reconnecting applications. Never include customer data or credentials in a public incident record.

## Recovery objectives

- **RTO target:** agreed maximum time to restore the defined service capability.
- **Observed recovery duration:** state its start/end boundaries and whether detection, approval, restore, validation and traffic cutover are included.
- **RPO target:** agreed maximum acceptable data-loss window.
- **Observed data gap:** compare the last verified recovered transaction with the incident boundary; include clock assumptions and any unverified interval.

Do not report a database restore duration as full application RTO. Timestamp age alone does not prove that all expected transactions were recovered.

## Status update template

```text
Time (UTC):
Impact and affected services:
Confirmed observations:
Current mitigation and owner:
Recovery verification completed:
Remaining risks:
Next update time:
```

## Post-incident review

Document impact, UTC timeline, trigger, contributing factors, detection gaps, mitigation, verification results, and follow-up actions with owners and due dates. Separate confirmed causes from open questions. Assign improvements to prevention, detection, mitigation, and recovery; verify completion with evidence.
