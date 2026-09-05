# CashOut Urban

## Overview

CashOut Urban is the general-purpose commercial vertical of CashOut Negocios.

It is designed for businesses that need operational, sales and POS capabilities
without restaurant-specific or hospitality-specific workflows.

Urban extends the shared CashOut Negocios core.

It does not replace it.

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

CashOut Urban reuses shared platform capabilities such as:

- business context
- users and roles
- sales
- operations
- POS
- audit
- shared configuration
- payment-connected workflows

and adds general commercial behavior where required.

---

## Target Businesses

Urban can support businesses such as:

- retail stores
- local commerce
- service businesses
- neighborhood shops
- small commercial operations
- mixed product and service businesses

The objective is to keep the operational model flexible enough for businesses
that do not require a specialized restaurant or hotel workflow.

---

## General Business Flow

A simplified Urban workflow can be represented as:

```text
Customer Need
     |
     v
Product / Service
     |
     v
Sale
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

The business workflow remains simple while still using the same shared platform
infrastructure available to other verticals.

---

## Products and Services

Urban can represent commercial activity involving:

- physical products
- services
- mixed product/service offers
- direct sales
- assisted sales

Conceptually:

```text
Catalog
  |
  +--> Products
  |
  `--> Services
          |
          v
        Sale
```

Production catalog schemas and private commercial data are intentionally not
published in this repository.

---

## Sales

Sales are handled through shared CashOut Negocios infrastructure.

```text
Select Product / Service
          |
          v
        Sale
          |
          v
      CashOut POS
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

This allows Urban to benefit from the same execution and traceability model used
across the platform.

---

## POS Integration

Urban can connect directly with the shared CashOut POS execution layer.

```text
Urban
  |
  v
Sale
  |
  v
CashOut POS
  |
  v
Trusted Payment Boundary
```

The vertical does not need to know the confidential implementation details of
the payment provider.

See [CashOut POS](pos.md).

---

## Operational Interface

Urban can be accessed through interfaces such as:

- business dashboard
- cashier interface
- desktop browser
- mobile browser
- PWA
- supported POS devices

Different interfaces can interact with the same shared business state.

---

## PWA Use

A PWA can provide a lightweight operational surface for businesses that need
mobility without deploying a full native client.

Conceptually:

```text
Business User
      |
      v
Urban PWA
      |
      v
CashOut Negocios Core
      |
      v
Sale / Operation
```

PWA support can also be useful in environments where connectivity may be
intermittent.

The exact production synchronization mechanisms remain private.

---

## Users and Roles

Urban may support several operational roles.

Examples include:

- owner
- administrator
- cashier
- staff member
- authorized operator

The vertical reuses the shared identity and permission architecture.

```text
User
 |
 v
Role
 |
 v
Allowed Urban Capability
```

Authentication and authorization details remain part of the private production
implementation.

---

## Audit

Urban operations can generate audit events through the shared audit capability.

Examples may include:

- sales
- administrative changes
- operational actions
- POS outcomes
- configuration changes

```text
Urban Action
     |
     v
Business Operation
     |
     +--> State Change
     |
     `--> Audit Event
```

See [Operational Audit](audit.md).

---

## General Service Businesses

Urban is not limited to product-based retail.

A business may sell services rather than physical goods.

Conceptually:

```text
Service
   |
   v
Customer Request
   |
   v
Commercial Operation
   |
   v
Sale
   |
   v
Payment
```

This makes Urban suitable for a broader range of local businesses.

---

## Shared Infrastructure

Urban benefits from improvements made at the core platform level.

For example:

```text
Shared Core Improvement
       |
       +--> Better Audit
       |
       +--> Better POS
       |
       +--> Better Security
       |
       +--> Better Operations
       |
       `--> Urban Benefits Automatically
```

This is one of the main advantages of the shared-core architecture.

---

## Separation from Restaurant

Restaurant workflows may require concepts such as:

- tables
- grouped tables
- waiter service
- dining state
- food-service order flows

Urban does not require those concepts.

```text
Urban
 |
 `--> General Commerce

Restaurant
 |
 `--> Food-Service Workflow
```

Both still share the same underlying business platform.

---

## Separation from Hotel

Hotel workflows may require:

- rooms
- guests
- reservations
- hospitality services
- stay-related operations

Urban does not require hospitality-specific state.

```text
Urban
 |
 `--> General Business

Hotel
 |
 `--> Hospitality Operations
```

Again, both use the same shared core.

---

## Commercial Simplicity

Urban is intended to provide a lower-complexity path into the CashOut Negocios
ecosystem.

The vertical should expose the capabilities required by a general commercial
business without forcing it to adopt domain-specific modules it does not need.

Conceptually:

```text
Shared Core
    +
General Commerce
    =
CashOut Urban
```

---

## Public Boundary

This repository may document:

- Urban architecture
- general commercial workflows
- shared-core relationships
- POS relationships
- audit relationships
- PWA concepts

It intentionally does not expose:

- production business data
- real customer records
- internal database schemas
- private pricing logic
- authentication secrets
- POS credentials
- payment provider configuration
- proprietary operational logic

---

## Design Principle

CashOut Urban follows a simple principle:

> **Provide general business capabilities without forcing specialized vertical complexity.**

In compact form:

```text
Shared Core
    +
General Commerce
    =
CashOut Urban
```
