# Contributing to CashOut Negocios

Thank you for your interest in CashOut Negocios.

This repository represents the public technical surface of a commercial
business operating platform.

---

## Current Contribution Scope

Useful contributions may include:

- architecture feedback
- modular platform discussion
- ERP/POS interoperability ideas
- restaurant workflow feedback
- hospitality workflow feedback
- PWA design discussion
- audit and traceability feedback
- documentation improvements
- real-world business use cases
- issue reports related to public documentation

---

## Before Opening an Issue

Please describe:

- the business problem
- the affected workflow
- expected behavior
- relevant constraints
- security considerations
- operational impact

Avoid including production data or secrets.

---

## Pull Requests

Documentation-focused pull requests are welcome.

Please keep changes:

- focused
- technically clear
- consistent with the shared-core architecture
- free of credentials
- free of customer or business data
- free of confidential partner material

Large architectural proposals should preferably begin as an issue or discussion.

---

## Public vs. Private Boundary

Do not submit material that exposes private implementation details.

This includes:

- production source code
- database contents
- private schemas
- credentials
- POS tokens
- confidential SDKs
- provider-specific secrets
- protected payment flows
- proprietary commercial logic
- fraud and security mechanisms
- private partner integrations

---

## Security Issues

Do not report sensitive vulnerabilities through public issues.

See [SECURITY.md](SECURITY.md).

---

## Architectural Principle

CashOut Negocios follows:

> **Build common business infrastructure once, then extend it with domain-specific verticals.**

Contributions should preserve that distinction between shared platform
responsibilities and vertical-specific behavior.

---

## Code of Conduct

Be constructive, technical and respectful.

The objective is to improve the quality of the public architecture and the
discussion around practical business software.
