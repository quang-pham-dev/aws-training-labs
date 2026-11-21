# ADR-001: AWS Primary Region Selection

| Field | Value |
| :--- | :--- |
| **Status** | Proposed |
| **Date** | 2026-11-21 |
| **Scope** | ERP Cloud Architecture |
| **Decision Owner** | Engineering Team |

## Context

The ERP system uses Next.js, NestJS, PostgreSQL, and object storage. Approximately 95% of users are located in Vietnam. The training budget is \$0 and all labs are designed to be local-first. Production deployment requires separate approval.

## Decision

Use `ap-southeast-1` (Singapore) as the training reference region and candidate primary production region. Keep application and database workloads in the same region and distribute critical components across two Availability Zones (Multi-AZ).

## Decision Drivers

- **Latency:** Geographic proximity provides low network latency for Vietnam-based users, but actual ISP routing and application p95 latency must be measured.
- **Availability:** Multi-AZ deployment mitigates single-AZ failures, provided dependencies and failover mechanisms are correctly configured.
- **Compliance:** Assess personal data processing, cross-border transfers, sector-specific residency obligations, and contractual requirements with qualified legal reviewers.
- **Cost:** Estimate compute, database, load balancing, NAT gateways, storage, logs, backups, and cross-AZ data transfer costs before deployment.

## Alternatives Considered

| Region | Considerations |
| :--- | :--- |
| **Singapore (`ap-southeast-1`)** | Candidate primary region; lowest latency baseline, mature service availability. |
| **Thailand (`ap-southeast-7`)** | Alternative nearby region; newer region, check service feature parity and network stability. |
| **Tokyo (`ap-northeast-1`)** | Alternative regional location; slightly higher latency for Vietnam (~80-110ms), higher costs. |
| **N. Virginia (`us-east-1`)** | Default for global services; geographic distance causes significant latency (>200ms) for Vietnam users. |

## Consequences

- **Positive (Benefits):** Full regional AWS service support, expected low round-trip latency (<40ms to Vietnam), native Multi-AZ resilience.
- **Negative (Trade-offs):** Cross-border compliance requirements, additional cost for Multi-AZ standby instances and cross-AZ data transfer, regional outage blast radius.
- *Note:* Multi-AZ is high availability, not a backup or regional disaster recovery (DR) strategy.

## Validation & Acceptance Criteria

- [ ] Measure latency across major Vietnamese ISPs (Viettel, VNPT, FPT); record p50/p95 latency and packet loss.
- [ ] Define application latency SLOs, RTO (Recovery Time Objective), and RPO (Recovery Point Objective).
- [ ] Confirm required AWS service availability and service quotas in `ap-southeast-1`.
- [ ] Complete data classification and legal review before storing real production/customer data.
- [ ] Formulate a detailed monthly cost model using AWS Pricing Calculator.
- [ ] Simulate AZ failure, database failover, and backup restoration scenarios.
- [ ] Obtain engineering, security, and budget approval before moving status to **Accepted**.

## Training Guardrails

Use synthetic mock data and local emulators whenever possible. Do not provision unapproved paid resources or leave idle resources running. Architecture diagrams are design artifacts, not proof of live infrastructure.

## References

- [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [AWS Pricing Calculator](https://calculator.aws/)
- [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)
