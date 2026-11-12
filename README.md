# ☁️ AWS Hands-on Training Labs (10-Week Roadmap)

A comprehensive hands-on repository designed to refresh, solidify, and master core and advanced **Amazon Web Services (AWS)** concepts. Built with a production-grade mindset following the **AWS Well-Architected Framework**.

---

## 🎯 Repository Objectives

- **Solidify Core Knowledge**: Deep dive from foundations (IAM, Networking, Multi-AZ) to advanced architectures (Serverless, Event-Driven, Microservices).
- **Hands-on & Practical**: Every week features functional code, practical labs (NestJS / TypeScript), and automation scripts.
- **Production-Ready Documentation**: Maintain Architecture Decision Records (ADRs), system architecture diagrams (`.drawio`), security checklists, operational runbooks, and cost optimization plans.
- **Infrastructure as Code (IaC)**: Provision and maintain reproducible infrastructure via code with peer review, linting, and automated CI/CD pipelines.

---

## 📁 Repository Structure

```text
aws-training-labs/
├── labs/                          # Weekly hands-on lab modules
│   ├── week-01-fundamentals/      # Week 1: IAM, Security, CLI & Billing
│   ├── week-02-networking/        # Week 2: VPC, Subnets, Routing & Multi-AZ
│   ├── week-03-s3/                # Week 3: Storage (S3, Presigned URLs, Glacier)
│   ├── week-04-lambda/            # Week 4: Serverless, API Gateway & EC2
│   ├── week-05-database/          # Week 5: DynamoDB, RDS, Backup & Encryption
│   ├── week-06-messaging/         # Week 6: SQS, SNS, EventBridge & DLQ
│   ├── week-07-observability/     # Week 7: CloudWatch, CloudTrail, Tracing & Alarms
│   ├── week-08-containers/        # Week 8: Docker, ECR, ECS (Fargate) & CI/CD
│   ├── week-09-iac/               # Week 9: Infrastructure as Code (CDK / Terraform)
│   └── week-10-capstone/          # Week 10: Production System Design & High Availability
├── docs/                          # Architecture blueprints & operational docs
│   ├── adr/                       # Architecture Decision Records
│   ├── architecture/              # Architecture diagrams (Draw.io, Mermaid)
│   ├── security/                  # Security checklists, threat models & sample policies
│   ├── cost/                      # Cost estimation, budget tracking & optimization plans
│   └── runbooks/                  # Incident response & operational deployment runbooks
├── infrastructure/                # Infrastructure provisioning code
│   ├── cdk/                       # AWS CDK (TypeScript)
│   └── docker/                    # Dockerfiles & docker-compose for local development
└── README.md                      # Roadmap, milestones, and repo guide
```

---

## 🗓️ 10-Week Roadmap & Deliverables

| Week | Focus Area | Key AWS Services | Deliverable | Status |
|:---:|:---|:---|:---|:---:|
| **01** | **AWS Fundamentals & Account Security** | IAM, MFA, AWS Organizations, Budgets, CLI | CIS-compliant AWS account setup, active AWS CLI, least-privilege policies. | 🟡 In Progress |
| **02** | **Networking & Multi-AZ Architecture** | VPC, Subnets, IGW, NAT GW, Security Groups, NACLs | Multi-AZ VPC network baseline for multi-tier apps (Web/App/DB). | ⚪ Planned |
| **03** | **Storage Services** | S3, Presigned URLs, Lifecycle Rules, KMS | NestJS service for S3 upload, secure download, streaming, and encryption. | ⚪ Planned |
| **04** | **Compute & Serverless** | EC2, Lambda, API Gateway, ALB | Serverless REST API in TypeScript (Lambda + API Gateway, cold start tuned). | ⚪ Planned |
| **05** | **Databases (SQL & NoSQL)** | DynamoDB, RDS (PostgreSQL/MySQL), Backup | Resilient data layer: RDS Multi-AZ + DynamoDB single-table design. | ⚪ Planned |
| **06** | **Event-Driven Architecture** | SQS, SNS, EventBridge, DLQ | Asynchronous background worker system with idempotency, retries & DLQ. | ⚪ Planned |
| **07** | **Observability & Auditing** | CloudWatch, CloudTrail, X-Ray | Centralized structured logs, custom metrics, tracing & incident alert alarms. | ⚪ Planned |
| **08** | **Containers & CI/CD** | Docker, ECR, ECS (Fargate), GitHub Actions | Containerized NestJS API, automated ECR build & push, deployment to ECS. | ⚪ Planned |
| **09** | **Infrastructure as Code (IaC)** | AWS CDK (TypeScript) / Terraform | Multi-environment reproducible infrastructure defined in code. | ⚪ Planned |
| **10** | **Production Architecture & Capstone** | Well-Architected, High Availability, DR | Production blueprint: Architecture diagram, ADRs, Threat Model & Cost Model. | ⚪ Planned |

---

## 🛠️ Prerequisites & Tech Stack

- **AWS CLI v2** configured with IAM Identity Center (SSO) or least-privilege credentials.
- **Node.js** (>= 20.x LTS), **TypeScript**, **NestJS CLI**.
- **Docker & Docker Compose** for local containerization and service emulation.
- **AWS CDK** (`aws-cdk`) and/or **Terraform** CLI.
- **Recommended VS Code Extensions**:
  - AWS Toolkit
  - Draw.io Integration (to edit/view `.drawio` files)
  - Markdown Preview Enhanced / Mermaid Preview

---

## 📌 Development & Contribution Standards

1. **Lab Structure (`labs/week-xx/`)**:
   - `README.md`: Lab objectives, step-by-step instructions, and verification checklist.
   - `notes.md`: Key theoretical insights, architecture trade-offs, and gotchas.
   - Functional source code and automated test/verification scripts.
2. **Architecture Decision Records (`docs/adr/`)**:
   - Every major technology or architecture choice (e.g., DynamoDB vs. Aurora Serverless, CDK vs. Terraform) is documented using the standard ADR format: *Status, Context, Decision, Consequences*.
3. **Security & Cost Guardrails**:
   - **Never commit secrets**: No AWS credentials, `.env` files, or access keys in git history.
   - **Cost limits**: Setup AWS Budgets with billing alert thresholds before launching billable resources.
   - **Tear down resources**: Always run cleanup commands (`cdk destroy`, `terraform destroy`, or CLI terminate) immediately after validating labs.
