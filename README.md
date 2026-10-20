# Zarvyn

[![Phase](https://img.shields.io/badge/Phase%200-Security%20design%20complete-green)](docs/THREAT-MODEL.md)
[![Phase](https://img.shields.io/badge/Phase%201-API%20implementation%20next-orange)](#roadmap)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow)](https://opensource.org/licenses/MIT)

> A multi-tenant secrets API being engineered from its threat model — with security decisions, failures and controls made explicit and measurable.

## Table of Contents

- [Zarvyn](#zarvyn)
  - [Table of Contents](#table-of-contents)
  - [Project Description](#project-description)
  - [Current Status](#current-status)
  - [Security Model](#security-model)
  - [Architecture](#architecture)
  - [Architecture Decisions](#architecture-decisions)
  - [Tech Stack](#tech-stack)
  - [Project Structure](#project-structure)
  - [Roadmap](#roadmap)
  - [Documentation](#documentation)
  - [License](#license)
  - [Author](#author)

## Project Description

**Zarvyn** is a cloud-native, multi-tenant platform that stores and manages
secrets and credentials for client organizations.

The project is being built as an engineering system, not as a collection of
isolated exercises. Security decisions are documented before implementation,
then validated progressively through controlled experiments and measurable
evidence.

Current evidence includes:
- Threat modeling before implementation (STRIDE, PASTA, Attack Trees)
- Defined tenant-isolation and least-privilege requirements
- Project scope and security boundaries
- Purple-team operating rules
- Architecture Decision Records (ADRs)

Planned capabilities such as encryption at rest, audit logging, Infrastructure
as Code, CI/CD security gates and observability will only be presented as
implemented evidence after they exist in the repository and can be reproduced.

## Current Status

Zarvyn is in its foundational phase. Security design comes first: the threat
model, project charter and purple team rules are complete and committed before
any production code is written.

| Area                                       | State                    |
| ------------------------------------------ | ------------------------ |
| Threat model (STRIDE, PASTA, Attack Trees) | Complete                 |
| Project charter and scope                  | Complete                 |
| Purple team charter and lab rules          | Complete                 |
| Architecture decision records              | In progress (1 recorded) |
| API implementation                         | Not started              |
| Infrastructure as Code                     | Not started              |
| CI/CD pipeline                             | Not started              |

## Security Model

Security is designed before code, not added after. The current threat model
covers six STRIDE categories and two full attack scenarios, documented in
[`docs/THREAT-MODEL.md`](docs/THREAT-MODEL.md).

| Principle            | How it applies                                          |
| -------------------- | ------------------------------------------------------- |
| **Least privilege**  | Every identity gets only what it needs                  |
| **Tenant isolation** | No tenant can reach another tenant's data               |
| **Defense in depth** | Multiple independent layers, no single point of failure |
| **Auditability**     | Every sensitive action is logged and attributable       |
| **Zero trust**       | Authorization enforced server-side on every request     |

## Architecture

The core flow of a request to store a secret, as decomposed during threat
modeling. Every step exists for a reason and maps to a specific threat.
```
Client
│
▼
[1] API receives the request
│
▼
[2] Authentication ── who is this?
│
▼
[3] Authorization ── are they allowed to do this?
│
▼
[4] Input validation ── is the payload well-formed?
│
▼
[5] Encryption ── secret is encrypted before storage
│
▼
[6] Tenant binding ── secret is tied to the correct tenant
│
▼
[7] Persistence ── written to secure storage
│
▼
[8] Audit log ── who did what, and when
│
▼
[9] Response to client
```

Steps 2 and 3 form the trust boundary: before them, a request is untrusted;
after them, it carries a verified identity and a defined set of permissions.

Detailed diagrams and design notes live in [`docs/architecture/`](docs/architecture/).

## Architecture Decisions

Significant design decisions are recorded as ADRs (Architecture Decision
Records) in [`docs/architecture/adr/`](docs/architecture/adr/). Each record
captures the context, the decision itself and its consequences.

| ADR                                                            | Decision                         |
| -------------------------------------------------------------- | -------------------------------- |
| [0001](docs/architecture/adr/0001-threat-model-before-code.md) | Threat model before writing code |

## Tech Stack

Planned stack. Each item moves to the Current Status table only once it is
implemented and reproducible in this repository.

| Category              | Technology                         |
| --------------------- | ---------------------------------- |
| **API Core**          | Python 3.12 (FastAPI)              |
| **Data Layer**        | PostgreSQL                         |
| **Containerization**  | Docker                             |
| **Infrastructure**    | Terraform, AWS                     |
| **CI/CD**             | GitHub Actions with security gates |
| **Security Scanning** | Trivy, Checkov, SAST/SCA           |
| **Observability**     | OpenTelemetry, Prometheus, Grafana |

## Project Structure

What exists today:

```
zarvyn/
├── docs/
│   ├── PROJECT-CHARTER.md      # Scope, goals and boundaries
│   ├── THREAT-MODEL.md         # STRIDE, PASTA and attack trees
│   ├── PURPLE-TEAM-CHARTER.md  # Purple team mission and lab rules
│   ├── CONVENTIONS.md          # Naming and formatting standards
│   ├── ROADMAP-DOCS.md         # When each documentation section is added
│   └── architecture/
│       ├── README.md
│       └── adr/                # Architecture Decision Records
├── CHANGELOG.md
├── LICENSE
└── README.md
```

Directories for source code (`src/`), tests (`tests/`), infrastructure
(`infra/`), labs (`labs/`) and CI (`.github/workflows/`) are added in the phase
that implements them, following the rule in
[`docs/ROADMAP-DOCS.md`](docs/ROADMAP-DOCS.md): nothing is documented before it exists.

## Roadmap

**Phase 0 — Security design (complete)**

- [x] Project charter, scope and boundaries
- [x] Threat model: STRIDE, PASTA and attack trees
- [x] Purple team charter and lab rules
- [x] First ADR: threat model before code

**Phase 1 onward — Implementation**

- [ ] Core API with robust tenant isolation
- [ ] Authentication & authorization layer (RBAC/ABAC)
- [ ] Secrets management and encryption at rest
- [ ] Audit logging and centralized monitoring
- [ ] Container hardening and minimal base images
- [ ] Infrastructure as Code deployment (AWS)
- [ ] CI/CD pipeline integration with automated security gates

## Documentation

- [Project Charter](docs/PROJECT-CHARTER.md) — scope, goals and ownership
- [Threat Model](docs/THREAT-MODEL.md) — STRIDE, PASTA and attack trees
- [Purple Team Charter](docs/PURPLE-TEAM-CHARTER.md) — mission, scope and lab rules
- [Conventions](docs/CONVENTIONS.md) — naming and formatting standards

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## Author

**Luan Thales** — Cloud Security Specialist · [LinkedIn](https://www.linkedin.com/in/luanthales) · [GitHub](https://github.com/zar4t)
