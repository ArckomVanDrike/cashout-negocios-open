# CashOut Negocios Core Platform

## Overview

CashOut Negocios is built around a shared core platform.

The core provides the common operational foundation used by the different
business verticals:

- CashOut Urban
- CashOut Restaurant
- CashOut Hotel

The verticals extend the platform with domain-specific workflows, but they do
not replace or duplicate the shared foundation.

---

## Core Principle

The architectural model is:

```text
                      CashOut Negocios
                      Shared Core Platform
                             |
             +---------------+---------------+
             |               |               |
             v               v               v
           Urban         Restaurant         Hotel
```

The shared core contains capabilities that multiple business models require.

The verticals add only what is specific to their domain.

---

## Why a Shared Core?

Many business systems repeatedly implement the same infrastructure:

- authentication
- business context
- users and roles
- operational records
- sales
- POS integration
- audit
- configuration
- common services

Duplicating these components for every business type increases:

- maintenance cost
- security risk
- architectural inconsistency
- development effort
- integration complexity

CashOut Negocios instead follows:

```text
Common Capability
       |
       v
   Shared Core
       |
       +--> Urban
       +--> Restaurant
       `--> Hotel
```

A platform-level improvement can therefore benefit multiple verticals.

---

## Core Responsibilities

The shared platform can provide responsibilities such as:

```text
CashOut Negocios Core
 |
 |-- Business Context
 |-- Users / Roles
 |-- Authentication
 |-- Operations
 |-- Sales
 |-- POS Coordination
 |-- Audit
 |-- Shared Configuration
 |-- Common Services
 `-- Integration Boundaries
```

Not every deployment must expose every capability in the same way.

The important architectural principle is that these concerns belong to the
shared platform rather than being reimplemented independently by each vertical.

---

## Business Context

Every operational workflow exists within a business context.

Conceptually:

```text
User
 |
 v
Business Context
 |
 +--> Configuration
 +--> Permissions
 +--> Products / Services
 +--> Operations
 +--> Sales
 `--> Audit
```

The business context determines which resources and workflows belong to the
active organization.

Production identifiers, databases and customer records are intentionally not
published in this repository.

---

## Users and Roles

Different users may interact with CashOut Negocios through different operational
surfaces.

Examples may include:

- administrators
- owners
- cashiers
- restaurant staff
- hospitality staff
- operational users

The platform separates identity and permissions from the vertical workflow.

Conceptually:

```text
Identity
   |
   v
Role / Permission
   |
   v
Allowed Capability
   |
   v
Business Operation
```

Production authentication and authorization mechanisms remain private.

---

## Shared Operations

Operations represent actions that affect the state of a business.

Examples may include:

- opening or closing an operational workflow
- creating or updating a sale
- assigning work
- moving a restaurant table through service states
- completing a hospitality workflow
- preparing a POS transaction

The shared core provides common infrastructure for recording and coordinating
these operations.

---

## Sales

Sales are a cross-cutting capability.

A sale may originate from different vertical workflows.

For example:

```text
Urban
  |
  +------------------+
                     |
Restaurant --------->+--> Sale --> POS --> Payment
                     |
Hotel -------------->+
```

The domain-specific workflow may differ, while the commercial execution can use
shared infrastructure.

---

## POS Coordination

The POS layer is treated as an execution capability connected to the shared
platform.

Conceptually:

```text
Business Workflow
       |
       v
Sale
       |
       v
POS Coordination
       |
       v
Trusted Payment Boundary
       |
       v
Transaction Result
```

Provider-specific secrets, credentials, confidential SDK components and
production payment logic remain outside this public repository.

See [POS](pos.md).

---

## Audit

Operational traceability belongs to the shared core.

A meaningful operation can generate an audit event.

```text
User Action
    |
    v
Business Operation
    |
    +--> State Change
    |
    `--> Audit Event
```

This allows multiple verticals to benefit from a common approach to
traceability.

See [Operational Audit](audit.md).

---

## Shared Configuration

Different businesses require different settings, but configuration can still be
managed through a common platform model.

Examples may include:

- enabled modules
- business preferences
- operational parameters
- POS configuration
- vertical capabilities
- user permissions

Sensitive production configuration is not included in this repository.

---

## Vertical Extensions

Verticals extend the shared core.

They should add domain-specific behavior without redefining the entire platform.

Conceptually:

```text
                     Shared Core
                         |
          +--------------+--------------+
          |              |              |
          v              v              v
        Urban        Restaurant        Hotel
          |              |              |
          v              v              v
     Retail /       Tables /        Rooms /
     Services        Orders        Hospitality
```

This separation allows both common and domain-specific development to evolve
independently.

---

## CashOut Urban

Urban represents the general-purpose commercial vertical.

It can use shared capabilities such as:

- business context
- users
- sales
- operations
- POS
- audit
- payment-connected workflows

without requiring restaurant or hospitality logic.

See [Urban](urban.md).

---

## CashOut Restaurant

Restaurant extends the platform with food-service concepts.

Examples include:

- tables
- grouped tables
- service state
- orders
- waiter workflows
- restaurant-specific operations

These capabilities sit on top of the shared CashOut Negocios foundation.

See [Restaurant](restaurant.md).

---

## CashOut Hotel

Hotel extends the platform with hospitality-specific workflows.

Examples may include:

- rooms
- guests
- reservations
- hospitality services
- operational coordination

Hotel remains a vertical extension of the core rather than the core itself.

See [Hotel](hotel.md).

---

## Shared Data Boundaries

The architecture separates public concepts from private operational data.

This repository may document concepts such as:

```text
Business
 |
 +--> User
 +--> Operation
 +--> Sale
 +--> POS
 +--> Audit
 `--> Vertical State
```

It does not publish:

- production databases
- real customer records
- business credentials
- private identifiers
- transaction secrets
- confidential partner data
- private payment records

---

## Service Boundaries

The shared core should avoid unnecessary coupling between components.

Conceptually:

```text
Interface
   |
   v
Shared Service
   |
   v
Domain Capability
```

This allows vertical modules and operational surfaces to evolve without
requiring every implementation detail to be shared.

---

## Multiple Operational Surfaces

The same core can support several interfaces.

```text
                   CashOut Negocios Core
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
     Business Web     Operational PWA    Android POS
          |                |                |
          v                v                v
   Administration      Staff Flow      Sale Execution
```

This separation is important because different roles require different user
experiences while still operating against the same business foundation.

---

## Resilience

Some operational surfaces may need to function under unreliable connectivity.

The architecture therefore explores patterns such as:

- PWA support
- local operational state
- controlled synchronization
- graceful degradation
- retry-safe operations

The exact production synchronization mechanisms remain private.

---

## Security Boundary

The public core architecture describes responsibilities without exposing
security-sensitive implementation details.

```text
Public Platform Model
        |
        v
Documented Interfaces
        |
-----------------------------
        |
        v
Private Production Core
        |
        +--> Authentication
        +--> Authorization
        +--> Business Data
        +--> Credentials
        +--> Payment Secrets
        +--> Internal Services
        `--> Security Controls
```

---

## Commercial Architecture

CashOut Negocios is intended as a commercial platform.

The shared-core model allows different products and plans to reuse the same
technical foundation while exposing capabilities appropriate to each business
type.

Commercial pricing, internal licensing logic and proprietary business rules are
not defined by this public architecture.

---

## Public Boundary

This document intentionally describes:

- shared platform responsibilities
- vertical boundaries
- operational relationships
- public architecture
- integration principles

It intentionally does not expose:

- production source code
- database internals
- credentials
- private APIs
- proprietary commercial logic
- confidential integrations
- payment secrets
- security mechanisms
- customer data

---

## Design Principle

The core architectural principle of CashOut Negocios is:

> **Build common business infrastructure once, then extend it with domain-specific verticals.**

In compact form:

```text
Shared Core
    +
Vertical Capability
    =
Business Product
```

This is the foundation of CashOut Negocios.
