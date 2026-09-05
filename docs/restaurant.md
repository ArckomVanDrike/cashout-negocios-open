# CashOut Restaurant

## Overview

CashOut Restaurant is the food-service vertical of CashOut Negocios.

It extends the shared platform with restaurant-specific workflows while reusing
the same core capabilities for:

- users and roles
- business context
- operations
- sales
- POS
- payments
- audit
- shared services

Restaurant functionality is a vertical extension of CashOut Negocios.

It is not the central platform itself.

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

CashOut Restaurant adds domain-specific behavior on top of the shared core.

---

## Restaurant Workflow

A simplified restaurant flow can be represented as:

```text
Guest / Table
     |
     v
Open Service
     |
     v
Add Items
     |
     v
Manage Table State
     |
     v
Prepare Sale
     |
     v
CashOut POS
     |
     v
Payment
     |
     v
Close Service
     |
     +--> Business Record
     |
     `--> Audit
```

The domain workflow is restaurant-specific.

The underlying commercial execution remains part of the shared platform.

---

## Tables

Tables are a central operational concept in the Restaurant vertical.

A table may move through states such as:

```text
Available
   |
   v
Occupied
   |
   v
In Service
   |
   v
Payment
   |
   v
Closed
   |
   v
Available
```

The exact production state model may differ.

This document describes only the public architectural concept.

---

## Table Groups

Restaurant operations may require multiple tables to be handled as one service
group.

Conceptually:

```text
Table A ----+
            |
Table B ----+--> Table Group --> Shared Service
            |
Table C ----+
```

A group can allow the restaurant workflow to treat several physical tables as
part of the same operational context.

The production implementation of grouping and persistence remains private.

---

## Orders

Orders connect the service workflow with the commercial layer.

```text
Table / Group
      |
      v
Order
      |
      +--> Products
      +--> Quantities
      +--> Service State
      |
      v
Prepared Sale
```

The restaurant workflow can evolve independently from the shared sales
infrastructure.

---

## Service State

Restaurant operations are not only transactions.

They also represent an active service process.

Conceptually:

```text
Open Service
     |
     v
Take Order
     |
     v
Update Order
     |
     v
Serve
     |
     v
Prepare Payment
     |
     v
Close
```

Operational interfaces should make this state visible to authorized staff.

---

## Staff Workflows

Different restaurant roles may interact with the same service state.

Examples include:

- administrator
- cashier
- waiter
- service staff
- authorized operator

Conceptually:

```text
Waiter
  |
  +--> Table / Order

Cashier
  |
  +--> Sale / Payment

Administrator
  |
  +--> Configuration / Oversight
```

Identity and permission infrastructure belongs to the shared core.

---

## Operational PWA

CashOut Restaurant can expose restaurant workflows through a PWA.

Potential uses include:

- waiter interface
- mobile order entry
- table status
- service updates
- cashier coordination

Conceptually:

```text
Restaurant Staff
       |
       v
Operational PWA
       |
       v
Restaurant Vertical
       |
       v
CashOut Negocios Core
```

This allows mobile operational workflows without requiring the full business
administration interface.

---

## Table-to-Sale Flow

A restaurant sale can originate from an active table or table group.

```text
Table / Group
      |
      v
Active Order
      |
      v
Prepare Sale
      |
      v
Shared Sales Layer
      |
      v
CashOut POS
```

This is an important architectural separation.

Restaurant-specific state creates the commercial intent.

The shared platform handles sale execution.

---

## POS Integration

CashOut Restaurant uses the shared CashOut POS layer.

```text
Restaurant Workflow
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

The Restaurant module should not require knowledge of confidential provider
implementation details.

See [CashOut POS](pos.md).

---

## Payment Completion

A successful payment can complete the restaurant workflow.

Conceptually:

```text
Active Service
      |
      v
Payment Requested
      |
      v
Transaction Confirmed
      |
      +--> Sale Completed
      |
      +--> Table Released
      |
      `--> Audit Event
```

The exact production transaction and recovery logic remains private.

---

## Failed or Interrupted Payment

A payment attempt does not always end successfully.

The system should preserve a clear distinction between restaurant state and
payment outcome.

```text
Payment Attempt
      |
      +--> Confirmed
      |
      +--> Rejected
      |
      `--> Interrupted
```

A failed payment should not automatically produce an incorrect business state.

The precise recovery mechanisms are implementation-specific.

---

## Releasing Tables

Once the associated service has been correctly completed, tables can return to
an available operational state.

```text
Active Table
     |
     v
Service Completed
     |
     v
Payment / Closure Confirmed
     |
     v
Release Table
```

For grouped tables, release behavior can apply to the relevant group state.

---

## Audit

Restaurant workflows contribute to the shared audit capability.

Examples may include:

- opening a table
- joining tables
- modifying an order
- preparing payment
- closing a service
- releasing a table
- operational overrides

Conceptually:

```text
Restaurant Action
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

## Restaurant and Shared Core

Restaurant should only own restaurant-specific behavior.

```text
Restaurant Vertical
 |
 |-- Tables
 |-- Groups
 |-- Orders
 |-- Service Workflow
 `-- Restaurant State
          |
          v
     Shared Core
          |
          +--> Users
          +--> Sales
          +--> POS
          +--> Audit
          `--> Shared Services
```

This keeps the system modular.

---

## Separation from POS

Restaurant is not the POS.

POS is a shared execution capability.

```text
Restaurant
    |
    v
Business Intent
    |
    v
POS
    |
    v
Payment Execution
```

This distinction allows the same POS architecture to support other verticals.

---

## Separation from Urban

Urban handles general commercial workflows.

Restaurant adds food-service concepts such as:

- tables
- service state
- grouped tables
- waiter interaction
- restaurant order lifecycle

Both reuse the same platform core.

---

## Separation from Hotel

Hotel represents hospitality workflows such as rooms, guests and reservations.

Restaurant remains focused on food-service operations.

A future deployment may combine multiple vertical capabilities within the same
business environment without collapsing them into one domain model.

---

## Multi-Surface Operation

Restaurant workflows may be distributed across several interfaces.

```text
                 Restaurant State
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
   Waiter PWA      Cashier UI      Admin Web
        |              |              |
        +--------------+--------------+
                       |
                       v
              Shared Platform Core
```

The same operational state can therefore be accessed through role-appropriate
interfaces.

---

## Connectivity Considerations

Restaurant operations may occur in environments where connectivity is unstable.

The architecture can support resilience patterns such as:

- lightweight PWA interfaces
- local operational continuity
- retry-safe synchronization
- clear pending states
- controlled reconciliation

The exact production implementation remains private.

---

## Security Boundaries

Restaurant interfaces should expose only the capabilities required by each role.

Sensitive information may include:

- credentials
- user data
- transaction information
- payment secrets
- internal business configuration

These remain behind private production boundaries.

---

## Public Boundary

This repository may document:

- table concepts
- table grouping
- service workflow
- order relationships
- POS integration
- payment completion
- audit relationships
- multi-surface architecture

It intentionally does not expose:

- production database schemas
- internal table identifiers
- private APIs
- authentication material
- payment credentials
- provider-specific transaction logic
- proprietary synchronization mechanisms
- real customer or business data

---

## Design Principle

CashOut Restaurant follows this principle:

> **Keep restaurant-specific service state in the vertical while reusing the shared platform for business execution.**

In compact form:

```text
Restaurant Workflow
       +
Shared Core
       +
POS / Payment
       =
CashOut Restaurant
```
