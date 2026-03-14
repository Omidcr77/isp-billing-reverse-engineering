# Open Source Replacement Strategy

This document explores potential open-source technologies that could replace components of the current DeltaSIB billing platform.

The goal is to evaluate alternative solutions that provide similar functionality while offering improved transparency, flexibility, and long-term maintainability.

---

# Current System Components

Based on system investigation, the existing platform consists of several tightly integrated components.

Authentication System
FreeRadius

Billing Engine
Custom compiled binaries

Database
MariaDB

Web Management Interface
Apache + PHP

Monitoring
Monit service monitoring

---

# Replacement Philosophy

A replacement architecture should aim to provide:

transparency
modularity
maintainability
extensibility

Instead of a monolithic system, modern architectures often use modular services communicating through APIs.

---

# Authentication System

Current system

FreeRadius

FreeRadius is already an open-source AAA server and remains a strong choice for ISP authentication.

Possible alternatives include:

FreeRadius (continue using)
Radiator Radius Server
OpenAAA frameworks

Recommendation

Continue using **FreeRadius** due to its stability and widespread adoption in ISP environments.

---

# Billing Engine

Current system

Custom compiled proprietary binaries

Possible open-source alternatives include:

Splynx
Powercode
Radius Manager
Daloradius (management layer)

Another option is building a **custom billing backend** using modern frameworks.

Possible backend technologies:

Python (FastAPI / Django)
Node.js
Go

---

# Database Layer

Current system

MariaDB

Possible alternatives

MariaDB
PostgreSQL

Recommendation

MariaDB is already suitable and widely used in ISP billing systems.

PostgreSQL may offer advantages for advanced analytics and scalability.

---

# Web Management Interface

Current system

Apache + PHP web interface

Possible replacements include modern web frameworks.

Backend frameworks

Django
FastAPI
Laravel
Node.js Express

Frontend frameworks

React
Vue.js
Angular

These frameworks allow building modern dashboards and management panels.

---

# Monitoring and Observability

Current system

Monit

Possible alternatives

Prometheus
Grafana
Zabbix
Netdata

These systems provide advanced monitoring and visualization capabilities.

---

# Modern Architecture Example

A modern architecture for an ISP billing system could look like this.

Subscriber Device
│
▼

Network Router
│
▼

FreeRadius Authentication Server
│
▼

Billing API Service
│
▼

Database (MariaDB/PostgreSQL)
│
▼

Web Management Dashboard

---

# Possible Technology Stack

Authentication
FreeRadius

Backend API
Python FastAPI / Node.js

Database
PostgreSQL or MariaDB

Dashboard
React or Vue.js

Monitoring
Prometheus + Grafana

---

# Benefits of Open Architecture

Adopting open-source components offers several advantages.

Full system transparency
Greater flexibility
Easier debugging
Community support
Improved scalability

---

# Migration Considerations

Replacing an existing billing platform should be approached carefully.

Important considerations include:

database schema compatibility
authentication flow integrity
network device compatibility
subscriber session tracking

Migration should be performed gradually with proper testing.

---

# Long Term Vision

The long-term goal is a fully documented and modular ISP management platform.

Key characteristics

open architecture
API driven services
modern monitoring tools
scalable infrastructure

Such an architecture would allow easier maintenance and future development.

---

# Related Documents

Migration planning:

notes/migration_plan.md

System investigation:

investigation/filesystem_analysis.md
investigation/database_analysis.md
investigation/service_architecture.md

System findings:

findings/licensing_system.md
findings/radius_integration.md
