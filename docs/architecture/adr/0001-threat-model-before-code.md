# ADR 0001 — Threat model before writing code

**Status:** Accepted
**Date:** 2026-07-24

## Context

Zarvyn stores secrets and credentials belonging to client organizations.
A design flaw in tenant isolation or access control would not be a bug —
it would be a breach affecting every client at once.

Security added after implementation tends to be a patch on top of wrong
assumptions. Fixing a design flaw found on paper costs almost nothing;
fixing the same flaw in production, with clients depending on the system,
costs incident response, contract penalties and trust.

## Decision

No production code is written before the threat model exists.

The first deliverable of this project is a documented threat model covering
STRIDE categories, PASTA stages and attack trees, reviewed and committed
before the first line of the API.

## Consequences

**Positive**
- Every component is implemented against a known set of threats
- Security requirements are explicit, not assumed
- Attack scenarios are documented before they can be exploited
- Design decisions can be traced back to a specific threat

**Negative**
- Slower start — no running code in the first phase
- The threat model must be revisited whenever a new surface is added,
  which is ongoing work rather than a one-time task
