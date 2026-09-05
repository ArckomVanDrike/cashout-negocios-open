# Security Policy

## Overview

CashOut Negocios is a commercial business operating platform that can interact
with operational data, POS systems, payment infrastructure and external
integrations.

Security-sensitive implementation details are intentionally kept outside this
public repository.

---

## Reporting a Vulnerability

Do not publish sensitive vulnerabilities through public GitHub issues,
discussions or pull requests.

If you discover a potential security issue, contact the project maintainer
privately.

A useful report should include:

- description of the issue
- affected public component or interface
- reproduction steps, when applicable
- potential impact
- screenshots or logs with secrets removed

Do not include:

- passwords
- API keys
- access tokens
- payment credentials
- private business data
- customer data
- production secrets
- confidential partner material

---

## Sensitive Areas

Potentially sensitive areas include:

- authentication
- authorization
- business data
- POS execution
- payment boundaries
- transaction handling
- device integrations
- external providers
- production infrastructure
- audit integrity

These implementation details may be maintained privately.

---

## Secrets

Never commit secrets to this repository.

This includes:

- passwords
- API keys
- tokens
- certificates
- private keys
- payment credentials
- partner credentials
- production configuration
- confidential SDK material

---

## Payment Security

Payment execution belongs behind a trusted integration boundary.

This repository does not publish:

- payment credentials
- provider secrets
- confidential transaction parameters
- protected SDK components
- production transaction logic
- device-specific secrets

---

## Responsible Disclosure

Please allow reasonable time for investigation and remediation before publicly
disclosing a confirmed vulnerability.

Good-faith security research is appreciated when it respects user privacy,
business continuity, service availability and applicable law.

---

## Public Repository Boundary

This repository documents selected architecture and public technical concepts.

Production security controls, confidential integrations and operational
infrastructure are maintained separately.
