# Migration Plan

This document outlines a potential long-term migration strategy from the current proprietary DeltaSIB billing system to a more flexible and maintainable architecture.

The purpose of this plan is not immediate replacement, but gradual understanding and modernization of the system.

---

# Current System Overview

The current environment is composed of several tightly coupled components.

Core system layers:

Authentication Layer
FreeRadius server

Billing Engine Layer
Custom compiled binaries

Database Layer
MariaDB

Web Management Layer
Apache + PHP interface

The system is installed primarily under:

/payamavaran/

---

# Challenges With Current Architecture

Several challenges were identified during investigation.

Limited transparency
Many core system components are compiled binaries, which limits visibility into their internal behavior.

Vendor dependency
The platform appears to rely on proprietary components for system logic.

Limited documentation
System architecture and internal workflows are not fully documented.

Upgrade limitations
Maintaining and updating the platform may become difficult over time.

---

# Migration Goals

A future architecture should aim to achieve the following goals.

Transparency
System components should be well documented and easier to inspect.

Modularity
Services should be separated into independent components.

Maintainability
System updates and changes should be easier to implement.

Scalability
The system should support large numbers of subscribers.

---

# Proposed Future Architecture

A modernized architecture could include the following components.

Authentication Server
FreeRadius or another AAA server

Billing Engine
Custom application or open source billing platform

Database
MariaDB or PostgreSQL

API Layer
REST API for service communication

Web Interface
Modern web dashboard

---

# Proposed Architecture Model

Subscriber Device
│
▼

Network Router
│
▼

Authentication Server
│
▼

Billing Service API
│
▼

Database Storage
│
▼

Management Dashboard

---

# Migration Strategy

Migration should be performed gradually in phases.

Phase 1 — Documentation

Fully document:

filesystem structure
database schema
service dependencies
authentication flow

Phase 2 — Component Isolation

Identify which services can be separated from the proprietary platform.

Examples:

authentication services
database access
web interface

Phase 3 — Parallel Development

Develop replacement services while the current system continues operating.

Possible replacements include:

custom authentication modules
modern billing backend
improved monitoring services

Phase 4 — Gradual Replacement

Replace system components one at a time rather than attempting a full system migration at once.

This reduces operational risk.

---

# Benefits of Gradual Migration

A phased migration approach allows:

minimal service disruption
continuous testing
improved system understanding
incremental improvements

---

# Long-Term Vision

The long-term goal is a transparent, modular, and maintainable ISP management platform.

Key characteristics:

open architecture
well documented services
scalable infrastructure
simplified maintenance

---

# Related Documents

System investigation documentation:

investigation/filesystem_analysis.md
investigation/database_analysis.md
investigation/service_architecture.md

Findings:

findings/licensing_system.md
findings/radius_integration.md
