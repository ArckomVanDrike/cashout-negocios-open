# CashOut Negocios Architecture

## Overview

CashOut Negocios is a modular business operating platform built around a shared
core and extended through business-specific verticals.

The architecture separates:

- shared business capabilities
- vertical workflows
- operational interfaces
- POS execution
- payment boundaries
- audit and traceability
- external integrations

The objective is to keep the platform reusable across different business models
without losing domain-specific behavior.

---

## High-Level Architecture

```text
+------------------------------------------------------+
|                  User Interfaces                     |
|------------------------------------------------------|
| Business Web | PWA | Restaurant | Hotel | Android POS|
+---------------------------+--------------------------+
                            |
                            v
+------------------------------------------------------+
|               CashOut Negocios Core                  |
|------------------------------------------------------|
| Business Context                                     |
| Users / Roles                                        |
| Operations                                           |
| Sales                                                |
| Shared Services                                      |
| Audit                                                |
+---------------------------+--------------------------+
                            |
              +-------------+-------------+
              |             |             |
              v             v             v
            Urban       Restaurant       Hotel
              |             |             |
              +-------------+-------------+
                            |
                            v
+------------------------------------------------------+
|                  Execution Layer                     |
|------------------------------------------------------|
| POS | Payments | External Services | Integrations    |
+------------------------------------------------------+
```

---

## Architectural Layers

CashOut Negocios can be understood through five main layers:

```text
Interfaces
    |
    v
Shared Core
    |
    v
Vertical Modules
    |
    v
Execution Layer
    |
    v
External Infrastructure
```

Each layer has a specific responsibility.

---

## 1. Interface Layer

Different users interact with the system through different surfaces.

Examples include:

- business administration
- cashier interface
- restaurant service interface
- hospitality interface
- PWA workflows
- Android POS devices

Conceptually:

```text
Owner / Admin ------> Business Web
Cashier ------------> POS / Cashier UI
Restaurant Staff ---> Restaurant PWA
Hotel Staff --------> Hotel Interface
Payment Device -----> Android POS
```

The interface layer should not redefine business rules independently.

It delegates business operations to the platform.

---

## 2. Shared Core Layer

The shared core contains reusable business capabilities.

Examples include:

```text
Shared Core
 |
 |-- Business Context
 |-- Users / Roles
 |-- Operations
 |-- Sales
 |-- Shared Configuration
 |-- Audit
 |-- Common Services
 `-- Integration Boundaries
```

The core is the architectural foundation of every CashOut Negocios vertical.

See [Core Platform](core-platform.md).

---

## 3. Vertical Layer

Vertical modules add business-specific capabilities.

```text
Shared Core
    |
    +--> Urban
    |
    +--> Restaurant
    |
    `--> Hotel
```

The verticals do not duplicate the platform.

They extend it.

---

## CashOut Urban

Urban provides general commercial workflows without restaurant or hospitality
specificity.

Typical areas may include:

- products
- services
- sales
- general business operations
- POS-connected workflows

See [Urban](urban.md).

---

## CashOut Restaurant

Restaurant extends the core with food-service operations.

Typical areas include:

- tables
- grouped tables
- orders
- service states
- waiter workflows
- cashier workflows
- payment completion

See [Restaurant](restaurant.md).

---

## CashOut Hotel

Hotel extends the core with hospitality workflows.

Typical areas may include:

- rooms
- guests
- reservations
- hospitality services
- operational coordination
- commercial activity

See [Hotel](hotel.md).

---

## 4. Execution Layer

The execution layer connects business intent to operational or external action.

Examples include:

- POS
- payment terminals
- external providers
- service integrations
- transaction confirmation

At a high level:

```text
Business Operation
       |
       v
Execution Request
       |
       v
Trusted Integration Boundary
       |
       v
External Execution
       |
       v
Result
```

The result can then update the platform state and audit trail.

---

## POS Architecture

The POS is a dedicated execution surface.

```text
CashOut Negocios
       |
       v
Prepare Sale
       |
       v
POS Interface
       |
       v
Payment Boundary
       |
       v
Payment Terminal / Provider
       |
       v
Transaction Result
       |
       +--> Business Record
       |
       `--> Audit
```

The public architecture documents this boundary without exposing confidential
provider implementation details.

See [POS](pos.md).

---

## Payment Boundary

Payments are handled behind a stricter trust boundary.

Conceptually:

```text
Sale
 |
 v
Payment Request
 |
 v
Trusted Payment Layer
 |
 v
Provider
 |
 v
Result
```

General business workflows should not require direct access to payment secrets.

Sensitive material such as credentials, provider tokens, confidential SDKs and
production integration details remains private.

---

## Audit Architecture

Auditability is cross-cutting.

Meaningful actions can generate audit events.

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

Audit records provide a way to inspect important operational transitions.

See [Audit](audit.md).

---

## Data Boundaries

CashOut Negocios separates public architectural models from private production
data.

Public concepts may include:

```text
Business
User
Operation
Sale
POS
Audit Event
Vertical State
```

Private operational data includes:

- production databases
- business records
- customer information
- transaction data
- credentials
- authentication material
- confidential partner information
- payment secrets

---

## Integration Boundaries

External systems should connect through controlled interfaces.

Conceptually:

```text
CashOut Negocios
       |
       v
Integration Boundary
       |
       +--> Payment Provider
       +--> External Business Service
       +--> Device Integration
       `--> Other Authorized Systems
```

The architecture should prevent third-party integration details from becoming
tightly coupled to the core business model.

---

## Android POS Boundary

Android-based payment terminals can act as a bridge between CashOut Negocios and
external payment capabilities.

Conceptually:

```text
Business Platform
       |
       v
POS Application
       |
       v
Device / Provider Integration
       |
       v
Payment Result
```

This repository intentionally does not expose confidential device SDK material,
provider credentials or protected implementation details.

---

## PWA Architecture

Operational PWAs allow staff to interact with the same core platform from
lightweight interfaces.

```text
Operational User
       |
       v
PWA
       |
       v
CashOut Negocios Core
       |
       v
Vertical Workflow
```

PWA workflows may support limited-connectivity scenarios where appropriate.

The exact synchronization mechanisms remain implementation-specific.

---

## Example: Restaurant Flow

```text
Open Table
    |
    v
Add Items
    |
    v
Restaurant Workflow
    |
    v
Shared Sale
    |
    v
POS
    |
    v
Payment
    |
    v
Transaction Confirmation
    |
    +--> Restaurant State
    +--> Business Record
    `--> Audit
```

This illustrates how a domain-specific workflow can use shared platform
capabilities.

---

## Example: Urban Sale

```text
Product / Service
       |
       v
Urban Workflow
       |
       v
Sale
       |
       v
POS
       |
       v
Payment
       |
       v
Business Record
       |
       v
Audit
```

The execution layers remain reusable even when the front-end workflow changes.

---

## Security Boundaries

Security-sensitive concerns belong to the private production layer.

```text
Public Architecture
        |
        v
Documented Responsibilities
        |
--------------------------------
        |
        v
Private Production Systems
        |
        +--> Authentication
        +--> Authorization
        +--> Credentials
        +--> Databases
        +--> Payment Secrets
        +--> Security Controls
        `--> Confidential Integrations
```

---

## Modularity

The platform is designed so that vertical modules can evolve independently while
sharing stable platform capabilities.

Conceptually:

```text
Stable Shared Core
      |
      +--> Urban evolves
      +--> Restaurant evolves
      `--> Hotel evolves
```

This reduces duplication and keeps security, POS, audit and infrastructure
concerns centralized where appropriate.

---

## Public Boundary

This document describes:

- architectural layers
- responsibility boundaries
- vertical relationships
- POS and payment boundaries
- audit relationships
- interface structure

It intentionally does not publish:

- production source code
- private database schemas
- confidential SDKs
- provider credentials
- proprietary payment flows
- internal security mechanisms
- customer data
- protected commercial logic

---

## Design Principle

The architecture follows one central rule:

> **Keep common business capabilities in the shared core and let verticals extend them without duplicating the platform.**

In compact form:

```text
Shared Core
   +
Vertical Workflow
   +
Execution Layer
   =
CashOut Negocios Product
```
