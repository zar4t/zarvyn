# Architecture

This page describes the request flow and trust boundaries defined during threat
modeling. It covers the secrets surface only: the API, its storage and the identity
and access controls around secrets. Components are added here when they are
implemented, not before.

## Request flow: storing a secret

| Step | Stage | Purpose | Threat it addresses (STRIDE) |
| --- | --- | --- | --- |
| 1 | API receives the request | Single entry point | Denial of Service (rate limits) |
| 2 | Authentication | Establish who is calling | Spoofing |
| 3 | Authorization | Decide if this identity may perform this action on this tenant's resource | Elevation of Privilege, Information Disclosure (IDOR) |
| 4 | Input validation | Reject malformed or oversized payloads | Tampering, Denial of Service |
| 5 | Encryption | Encrypt the secret before it is stored | Information Disclosure |
| 6 | Tenant binding | Bind the secret to the tenant derived from the verified identity, never from client input | Tampering, Information Disclosure |
| 7 | Persistence | Write to secure storage | Tampering |
| 8 | Audit log | Record who did what, when and with which result | Repudiation |
| 9 | Response | Return only what the caller is allowed to see | Information Disclosure |

## Trust boundary

Steps 2 and 3 form the trust boundary. Before them a request is untrusted; after
them it carries a verified identity and a defined set of permissions. Any value
that decides authorization, such as tenant or role, comes from the verified
identity and never from fields sent by the client.

## Related documents

- [Threat model](../THREAT-MODEL.md)
- [ADR 0001: Threat model before code](adr/0001-threat-model-before-code.md)
