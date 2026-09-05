<img width="1536" height="1024" alt="cashout-negocios-github-hero" src="https://github.com/user-attachments/assets/3d2caab2-6904-478f-a27f-2c1732b3afe8" />


# CashOut Negocios

## Modular Business Operating Platform

**ERP, POS and operational infrastructure for retail, restaurants and hospitality.**

CashOut Negocios is a modular business platform designed around a shared core
for day-to-day operations, sales, auditability and payment-connected workflows.

The platform supports multiple business models through specialized verticals:

- CashOut Urban
- CashOut Restaurant
- CashOut Hotel

These products are not separate systems.

They extend a common operational foundation.

---

## One Core, Multiple Business Models

```text
                      CashOut Negocios
                      Shared Core Platform
                             |
             +---------------+---------------+
             |               |               |
             v               v               v
           Urban         Restaurant         Hotel
             |               |               |
             +---------------+---------------+
                             |
        +--------------------+--------------------+
        |                    |                    |
        v                    v                    v
      POS                Operations             Audit
        |                    |                    |
        +--------------------+--------------------+
                             |
                             v
                  Payment Infrastructure
```

The shared core provides the foundation required to build and operate each
business vertical without duplicating the entire platform.

---

## What is CashOut Negocios?

CashOut Negocios is being developed as a practical operating system for small
and medium businesses.

It brings together areas that are often fragmented across multiple tools:

- business operations
- point of sale
- product and service management
- staff workflows
- restaurant operations
- hospitality operations
- transactional traceability
- audit
- payment-connected workflows
- mobile and PWA interfaces

The objective is not simply to provide another administrative dashboard.

The objective is to connect **operations, sales and execution** through one
modular platform.

---

## Shared Core Platform

The core is the foundation of CashOut Negocios.

It provides common capabilities that can be reused by every vertical.

Conceptually:

```text
                    Shared Core
                        |
      +-----------------+-----------------+
      |                 |                 |
      v                 v                 v
 Authentication      Business          Operations
                     Context
      |                 |                 |
      +-----------------+-----------------+
                        |
        +---------------+---------------+
        |               |               |
        v               v               v
      Sales           Audit             POS
        |               |               |
        +---------------+---------------+
                        |
                        v
              Vertical Capabilities
```

This architecture allows vertical products to share infrastructure while still
supporting domain-specific workflows.

Read more in [Core Platform](docs/core-platform.md).

---

# Business Verticals

## CashOut Urban

CashOut Urban is the general-purpose commercial vertical.

It is designed for businesses that need a lightweight operational platform
without restaurant- or hotel-specific workflows.

Potential use cases include:

- retail
- local commerce
- service businesses
- neighborhood businesses
- small commercial operations

The Urban vertical can use the shared CashOut Negocios core for sales,
operations, auditability and POS-connected workflows.

Read more in [Urban](docs/urban.md).

---

## CashOut Restaurant

CashOut Restaurant extends the shared core with food-service workflows.

Areas include:

- tables
- table groups
- orders
- service workflow
- cashier operations
- payment coordination
- restaurant POS
- operational visibility

Conceptually:

```text
Customer / Table
       |
       v
Service Workflow
       |
       v
Order
       |
       v
CashOut Negocios Core
       |
       +--> POS
       |
       +--> Audit
       |
       `--> Payment
```

Restaurant functionality remains a vertical module.

It is **not** the central architecture of CashOut Negocios.

Read more in [Restaurant](docs/restaurant.md).

---

## CashOut Hotel

CashOut Hotel extends the same shared platform for hospitality operations.

Potential capabilities include:

- guest workflows
- rooms
- reservations
- hospitality operations
- service coordination
- commercial activity
- auditability
- POS-connected services

Hotel functionality can share the same core operational and transactional
infrastructure used by other CashOut Negocios products.

Read more in [Hotel](docs/hotel.md).

---

# Point of Sale

CashOut POS connects the operational platform with physical sales execution.

The public architecture treats the POS as a dedicated execution surface.

```text
CashOut Negocios
       |
       v
POS Interface
       |
       v
Sale Preparation
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
       v
Business Records + Audit
```

The POS architecture can support dedicated terminals and Android-based payment
devices through controlled integration layers.

The production implementation, credentials, private partner configuration and
provider-specific confidential details are maintained separately.

Read more in [POS](docs/pos.md).

---

# Payments

CashOut Negocios is designed so payment execution can become part of the
business workflow rather than an isolated external step.

At a high level:

```text
Business Operation
       |
       v
Sale
       |
       v
Payment Request
       |
       v
Trusted Payment Boundary
       |
       v
Provider
       |
       v
Confirmed Transaction
       |
       v
Operational Record
```

Payment integrations are isolated behind a trusted execution boundary.

This repository does not expose:

- payment credentials
- production tokens
- confidential partner configuration
- private SDK material
- protected payment implementation
- production security mechanisms

---

# Operational Audit

Traceability is a core concern of the platform.

CashOut Negocios is designed to retain meaningful operational events so
business activity can be inspected and reconstructed when appropriate.

Examples may include:

- sales activity
- operational changes
- user actions
- POS events
- administrative actions
- business workflow transitions

Conceptually:

```text
Action
  |
  v
Business Operation
  |
  +--> State Change
  |
  `--> Audit Event
          |
          v
     Traceability
```

Auditability is intended to be part of the shared platform rather than an
afterthought added individually to every vertical.

Read more in [Audit](docs/audit.md).

---

# PWA and Operational Interfaces

CashOut Negocios is designed to support multiple operational surfaces.

These may include:

- desktop browser
- mobile browser
- PWA
- cashier station
- waiter interface
- Android POS
- business dashboard

Different interfaces can interact with the same shared business core.

```text
                 CashOut Negocios Core
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
   Business Web      Operational PWA   Android POS
        |                |                |
        v                v                v
  Administration     Staff / Service   Payment Device
```

PWA-oriented workflows can also support resilience and limited-connectivity
scenarios where appropriate.

---

# Architecture

CashOut Negocios follows a modular architecture.

```text
+--------------------------------------------------+
|                 User Interfaces                  |
|--------------------------------------------------|
| Business Web | PWA | Restaurant | Hotel | POS   |
+-------------------------+------------------------+
                          |
                          v
+--------------------------------------------------+
|              CashOut Negocios Core               |
|--------------------------------------------------|
| Business Context                                 |
| Operations                                       |
| Sales                                            |
| Users / Roles                                    |
| Audit                                            |
| Shared Services                                  |
+-------------------------+------------------------+
                          |
           +--------------+--------------+
           |              |              |
           v              v              v
        Urban         Restaurant        Hotel
           |              |              |
           +--------------+--------------+
                          |
                          v
+--------------------------------------------------+
|                 Execution Layer                  |
|--------------------------------------------------|
| POS | Payments | External Services | Integrations|
+--------------------------------------------------+
```

The public architecture describes responsibilities and boundaries without
publishing production-sensitive implementation details.

See [Architecture](docs/architecture.md).

---

# Example: Restaurant Sale

A simplified operational flow can look like:

```text
Open Table
    |
    v
Add Products
    |
    v
Prepare Sale
    |
    v
POS
    |
    v
Payment
    |
    v
Confirmed Transaction
    |
    +--> Restaurant State Updated
    |
    +--> Business Records Updated
    |
    `--> Audit Trail
```

This illustrates the relationship between a vertical workflow and the shared
platform.

---

# Example: General Business Sale

For a general business:

```text
Product / Service
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

The same underlying platform can therefore support very different businesses.

---

# Why Modular?

Building separate systems for every business type creates duplication.

CashOut Negocios instead separates:

```text
What every business needs
          |
          v
      Shared Core
          |
          +
          |
What this business specifically needs
          |
          v
       Vertical
```

This allows shared improvements in areas such as:

- security
- audit
- POS
- operations
- infrastructure
- payment integration

to benefit multiple vertical products.

---

# Security and Trust Boundaries

CashOut Negocios handles business and transactional workflows.

The architecture therefore separates public interfaces from sensitive
operational components.

```text
Public Architecture
        |
        v
Documented Interfaces
        |
-----------------------------
        |
        v
Private Production Layer
        |
        +--> Credentials
        +--> Business Data
        +--> Payment Tokens
        +--> Provider Configuration
        +--> Security Logic
        +--> Private Integrations
        `--> Production Infrastructure
```

See [SECURITY.md](SECURITY.md).

---

# Public vs. Private Implementation

This repository is the **public technical surface of CashOut Negocios**.

It is intended to document:

- architecture
- platform concepts
- vertical boundaries
- POS architecture
- operational workflows
- audit principles
- high-level payment architecture
- roadmap
- public interoperability concepts

The production platform is maintained separately.

Private components include, but are not limited to:

- production databases
- business and customer data
- credentials
- authentication material
- POS tokens
- payment provider secrets
- confidential SDK components
- private partner integrations
- production configuration
- proprietary commercial logic
- fraud and security mechanisms
- protected operational infrastructure

> **Open the interface, document the architecture, protect the implementation where it matters.**

---

# Project Status

CashOut Negocios is an active commercial software project.

The broader platform includes ongoing work across:

- shared business infrastructure
- POS
- restaurant operations
- hospitality
- retail and general commerce
- operational audit
- PWA workflows
- payment integration

The public repository documents selected technical architecture while
production systems and sensitive integrations remain private.

See [Roadmap](docs/roadmap.md).

---

# Documentation

- [Architecture](docs/architecture.md)
- [Core Platform](docs/core-platform.md)
- [CashOut Urban](docs/urban.md)
- [CashOut Restaurant](docs/restaurant.md)
- [CashOut Hotel](docs/hotel.md)
- [CashOut POS](docs/pos.md)
- [Operational Audit](docs/audit.md)
- [Roadmap](docs/roadmap.md)

---

# Project

CashOut Negocios is an independent business technology project by
**Andreé Settembrino**.

Its objective is to build practical operational infrastructure connecting
business management, physical commerce, software workflows and payment
execution through a shared modular platform.

---

# Intellectual Property

CashOut Negocios is a **proprietary commercial technology platform**.

This repository exposes selected architecture, documentation and public
technical concepts for evaluation, discussion and interoperability purposes.

The production platform, proprietary business logic, private data models,
payment integrations, POS implementation, security mechanisms and confidential
partner integrations are maintained separately and remain proprietary.

Public access to this repository does **not** constitute an open-source release
or transfer ownership of the underlying technology.

See:

- [Intellectual Property](INTELLECTUAL_PROPERTY.md)
- [License](LICENSE)

Copyright (c) 2026 Andreé Settembrino. All Rights Reserved.
