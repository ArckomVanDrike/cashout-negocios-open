# CashOut Negocios Roadmap

## Overview

CashOut Negocios is evolving as a modular business operating platform built
around a shared core and extended through specialized verticals.

The roadmap is organized around:

- shared platform maturity
- vertical capabilities
- POS and payment execution
- operational resilience
- auditability
- interoperability
- commercial deployment

Not every item described here is currently available in production.

---

## Phase 1 - Shared Core

The foundation of the platform is the shared CashOut Negocios core.

Key areas include:

- business context
- users and roles
- operations
- sales
- shared configuration
- audit
- common services
- integration boundaries

The objective is to establish a stable operational foundation reused by all
verticals.

---

## Phase 2 - CashOut Urban

Urban provides the general-purpose commercial layer.

Areas include:

- product and service sales
- cashier workflows
- general business operations
- PWA access
- POS-connected execution
- audit integration

Urban is intended to remain simple and adaptable for businesses that do not
require restaurant or hotel-specific workflows.

---

## Phase 3 - CashOut Restaurant

Restaurant extends the platform with food-service operations.

Areas include:

- tables
- table groups
- orders
- service states
- waiter workflows
- cashier workflows
- payment completion
- auditability

The long-term objective is a resilient operational workflow that can be used
from multiple devices and staff roles.

---

## Phase 4 - CashOut Hotel

Hotel extends the shared core for hospitality.

Areas include:

- rooms
- guests
- reservations
- stay lifecycle
- hospitality services
- commercial activity
- POS-connected payments
- auditability

The platform should allow Hotel and Restaurant capabilities to coexist where a
business requires both.

---

## Phase 5 - POS Integration

CashOut POS connects business operations with physical payment execution.

Key areas include:

- sale preparation
- controlled POS handoff
- transaction result handling
- provider abstraction
- audit integration
- device support
- transaction state clarity
- resilient execution

Provider-specific implementation details remain private.

---

## Phase 6 - Payment Infrastructure

Payments are treated as a trusted execution boundary.

The architectural direction includes:

```text
Business Operation
       |
       v
Sale
       |
       v
POS
       |
       v
Trusted Payment Boundary
       |
       v
Authorized Provider
       |
       v
Confirmed Transaction
```

Future work can include broader provider support while preserving a stable
business-facing interface.

---

## Phase 7 - Operational PWA

PWA workflows can improve mobility and resilience.

Potential areas include:

- waiter interfaces
- cashier workflows
- staff interfaces
- operational state
- limited-connectivity use
- graceful synchronization

The exact production synchronization model remains private.

---

## Phase 8 - Audit and Traceability

Audit continues as a shared platform capability.

Areas include:

- meaningful business events
- state transition traceability
- actor attribution
- incident reconstruction
- operational evidence
- controlled audit access

Auditability should evolve alongside every vertical rather than being added
afterward.

---

## Phase 9 - Interoperability

CashOut Negocios can progressively expose controlled public interfaces for
authorized integrations.

Potential areas include:

- business services
- POS interfaces
- third-party integrations
- device integrations
- public contracts
- selected SDKs

Any public interface must preserve security and commercial boundaries.

---

## Phase 10 - Multi-Surface Operations

The platform can evolve toward coordinated use across:

```text
Business Web
     +
Operational PWA
     +
Cashier Interface
     +
Android POS
     +
Vertical Interfaces
     |
     v
Shared Business State
```

The objective is consistent operational state across role-specific interfaces.

---

## Phase 11 - Commercial Scale

The longer-term platform direction includes commercial deployment across
different business types.

Potential priorities include:

- onboarding
- plan management
- operational monitoring
- deployment tooling
- merchant support
- device management
- partner integrations
- scalable infrastructure

Commercial and partner-specific implementation remains private.

---

## Cross-Cutting Priorities

### Security

Sensitive business, authentication and payment information must remain behind
controlled trust boundaries.

### Audit

Meaningful operational actions should remain traceable.

### Modularity

Shared infrastructure should remain separate from vertical-specific behavior.

### Resilience

Operational workflows should degrade safely under imperfect connectivity.

### Interoperability

External integrations should use explicit boundaries rather than internal
coupling.

### Practicality

CashOut Negocios should solve real business problems without unnecessary
platform complexity.

---

## Current Public Focus

This repository currently documents:

- shared-core architecture
- Urban
- Restaurant
- Hotel
- POS architecture
- operational audit
- public/private boundaries
- roadmap

Production systems, payment integrations and sensitive commercial components
are maintained separately.

---

## Long-Term Vision

CashOut Negocios is intended to connect:

```text
Business Management
        +
Operations
        +
Vertical Workflows
        +
POS
        +
Payments
        +
Audit
        +
Multiple Interfaces
        |
        v
Unified Business Operating Platform
```

The objective is not simply an ERP.

It is a modular operational platform that connects business state with
real-world commercial execution.
