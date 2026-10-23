# Documentation Roadmap

Sections planned for this project's documentation, and when each one enters.
A section is only added once the thing it documents actually exists — an empty
section signals abandonment, not ambition.

## Already in place

| Section | Location |
|---|---|
| Project Charter | `docs/PROJECT-CHARTER.md` |
| Threat Model (STRIDE, PASTA, Attack Trees) | `docs/THREAT-MODEL.md` |
| Purple Team Charter | `docs/PURPLE-TEAM-CHARTER.md` |
| Conventions | `docs/CONVENTIONS.md` |
| Current Status | `README.md` |
| Architecture | `docs/architecture/` |
| Architecture Decision Records | `docs/architecture/adr/` |
| Contributing Guidelines | `CONTRIBUTING.md` |
| Security Policy | `SECURITY.md` |
| Portuguese README | `README.pt-BR.md` |

## Planned

| Section | Enters when |
|---|---|
| Getting Started / How to Run | The API runs locally |
| Screenshots | There is something visual to show |
| How to Attack | There is a real target to attack in the lab |
| How to Defend | Paired with How to Attack — never published alone |
| Metrics | Observability is in place and numbers are real |
| Deployment Guide | Infrastructure is provisioned |

## Rules

1. A section is written when its subject exists, never before.
2. Offensive documentation is always paired with the corresponding defense.
3. All attack documentation refers to the controlled Zarvyn lab only.
4. No metric is published unless it was actually measured.
