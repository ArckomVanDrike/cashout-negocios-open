# CashOut Hotel

## Overview

CashOut Hotel is the hospitality vertical of CashOut Negocios.

It extends the shared platform with hotel-specific and accommodation-oriented
workflows while reusing common capabilities such as:

- business context
- users and roles
- operations
- sales
- POS
- payments
- audit
- shared services

Hotel functionality is a vertical extension of the CashOut Negocios platform.

It is not the shared core itself.

---

## Position in the Platform

```text
                    CashOut Negocios
                    Shared Core
                         |
            +------------+------------+
            |            |            |
            v            v            v
          Urban      Restaurant      Hotel
```

CashOut Hotel adds hospitality-specific behavior while remaining connected to
the same operational foundation.

---

## Hospitality Workflow

A simplified hotel workflow can be represented as:

```text
Guest
  |
  v
Reservation
  |
  v
Room / Stay
  |
  v
Hospitality Services
  |
  v
Commercial Operation
  |
  v
CashOut Negocios Core
  |
  +--> POS
  |
  +--> Payment
  |
  `--> Audit
```

The hospitality workflow is domain-specific.

The commercial and operational infrastructure remains shared.

---

## Rooms

Rooms are a core hospitality concept.

A room may participate in an operational lifecycle such as:

```text
Available
   |
   v
Reserved
   |
   v
Occupied
   |
   v
Service / Stay
   |
   v
Checkout
   |
   v
Available
```

The exact production state model may differ.

This document describes the public architectural concept only.

---

## Guests

Guest-related workflows can include:

- reservation association
- stay context
- service requests
- commercial activity
- checkout
- operational history

Conceptually:

```text
Guest
  |
  +--> Reservation
  +--> Room
  +--> Services
  +--> Charges
  `--> Stay State
```

Private guest records and personal data are not part of this public repository.

---

## Reservations

Reservations connect future hospitality intent with operational room state.

```text
Reservation Request
        |
        v
Availability
        |
        v
Reservation
        |
        v
Assigned Hospitality Context
```

Reservation workflows may eventually interact with:

- rooms
- guests
- services
- commercial records
- payment workflows
- audit

The production implementation remains private.

---

## Stay Lifecycle

A hospitality stay may involve several operational stages.

```text
Reservation
    |
    v
Arrival
    |
    v
Check-In
    |
    v
Active Stay
    |
    v
Services / Charges
    |
    v
Checkout
    |
    v
Completed Stay
```

Different properties may require different workflows.

The architecture should allow hotel-specific behavior without duplicating the
shared platform infrastructure.

---

## Hospitality Services

Hotels may provide services beyond the room itself.

Examples may include:

- food and beverage
- additional services
- local experiences
- maintenance requests
- guest assistance
- transport coordination
- other chargeable services

Conceptually:

```text
Guest / Stay
      |
      v
Hospitality Service
      |
      v
Operational Record
      |
      v
Optional Charge / Sale
```

These services can connect to the shared commercial layer where appropriate.

---

## Commercial Activity

Hospitality operations can generate commercial transactions.

Examples may include:

- room-related charges
- additional services
- restaurant activity
- paid amenities
- other business services

At a high level:

```text
Hospitality Operation
        |
        v
Commercial Intent
        |
        v
Shared Sale
        |
        v
CashOut POS
        |
        v
Payment
```

This allows CashOut Hotel to reuse the same execution layer as other verticals.

---

## POS Integration

CashOut Hotel can use the shared CashOut POS architecture.

```text
Hotel Workflow
      |
      v
Prepared Sale
      |
      v
CashOut POS
      |
      v
Trusted Payment Boundary
      |
      v
Transaction Result
```

The Hotel vertical should not depend directly on confidential provider-specific
payment implementation.

See [CashOut POS](pos.md).

---

## Restaurant + Hotel

A hospitality business may require both hotel and restaurant capabilities.

The shared-core architecture allows these domains to coexist without forcing
them into one monolithic model.

Conceptually:

```text
                 CashOut Negocios Core
                         |
              +----------+----------+
              |                     |
              v                     v
         Hotel Vertical       Restaurant Vertical
              |                     |
              +----------+----------+
                         |
                         v
                 Shared POS / Audit
```

Each vertical maintains its own domain state while sharing common operational
infrastructure.

---

## Operational Roles

Hotel environments may include roles such as:

- owner
- administrator
- reception
- hospitality staff
- cashier
- operational personnel

The shared identity and permission architecture can determine which capabilities
each role may access.

```text
User
 |
 v
Role
 |
 v
Allowed Hospitality Capability
```

Authentication and authorization details remain private.

---

## Operational Interfaces

Hotel workflows may be exposed through different interfaces.

Examples include:

- business administration
- reception interface
- operational PWA
- mobile staff interface
- cashier interface
- POS device

Conceptually:

```text
                    Hotel State
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
   Reception UI     Staff PWA      Admin Web
        |              |              |
        +--------------+--------------+
                       |
                       v
              CashOut Negocios Core
```

---

## Audit

Hotel operations can participate in the shared audit system.

Potential events may include:

- reservation changes
- room state changes
- check-in
- checkout
- service operations
- commercial activity
- administrative actions

```text
Hotel Action
     |
     v
State Change
     |
     +--> Operational Result
     |
     `--> Audit Event
```

See [Operational Audit](audit.md).

---

## Privacy

Hospitality workflows may involve personal and operational data.

Sensitive information can include:

- guest identity
- contact information
- reservation details
- stay history
- payment information
- private service requests

Public architecture should describe responsibilities without exposing real
guest data or production records.

---

## Limited Connectivity

Hospitality environments may experience unstable or limited connectivity.

Operational interfaces may therefore benefit from resilience patterns such as:

- PWA support
- clear pending states
- local continuity where appropriate
- controlled synchronization
- graceful degradation

The exact production synchronization and reconciliation mechanisms remain
private.

---

## Separation from Urban

Urban focuses on general commercial workflows.

Hotel adds hospitality-specific state such as:

- rooms
- reservations
- guests
- stays
- hospitality services

Both remain connected to the same shared business platform.

---

## Separation from Restaurant

Restaurant focuses on food-service operations such as:

- tables
- grouped tables
- orders
- service state
- waiter workflows

Hotel focuses on accommodation and hospitality.

A real business may use both.

The shared-core model allows this without making one vertical the foundation of
the other.

---

## Shared Core Relationship

CashOut Hotel should own only hospitality-specific behavior.

```text
Hotel Vertical
 |
 |-- Rooms
 |-- Guests
 |-- Reservations
 |-- Stay Workflow
 `-- Hospitality Services
          |
          v
     Shared Core
          |
          +--> Users
          +--> Operations
          +--> Sales
          +--> POS
          +--> Audit
          `--> Shared Services
```

This keeps the architecture modular and reusable.

---

## Public Boundary

This repository may document:

- room concepts
- guest relationships
- reservation architecture
- stay lifecycle
- hospitality workflows
- POS relationships
- audit relationships
- multi-surface operation

It intentionally does not expose:

- production guest data
- real reservation records
- internal database schemas
- private identifiers
- authentication material
- payment credentials
- confidential integrations
- proprietary pricing logic
- production security mechanisms

---

## Design Principle

CashOut Hotel follows this principle:

> **Keep hospitality-specific workflows in the vertical while reusing the shared platform for business execution.**

In compact form:

```text
Hospitality Workflow
        +
Shared Core
        +
POS / Payment
        =
CashOut Hotel
```
