![License](https://img.shields.io/badge/license-MIT-blue)
# DeltaSIB System Analysis

This repository documents the technical investigation and architectural analysis of a DeltaSIB ISP billing system environment deployed on CentOS.

The goal of this research project is to understand the system architecture, document its components, analyze the licensing mechanism, and explore potential open-source replacement strategies for long-term sustainability.

---

# Project Goals

The objectives of this project are:

* Document the filesystem structure of the DeltaSIB installation
* Identify the main services used in the system
* Analyze how the billing platform integrates with FreeRadius
* Investigate the system licensing mechanism
* Document commands used during the investigation
* Prepare a roadmap for open-source replacement

This repository is intended for **system administrators, network engineers, and developers** studying ISP billing system architecture.

---

# Environment Information

Operating System

CentOS 7 (Core)

Typical Installation Path

/payamavaran/

Main technologies involved:

* FreeRadius authentication server
* MariaDB database
* Apache web interface
* ISP billing backend services
* Network authentication infrastructure

---

# Main System Directory Structure

The DeltaSIB system is primarily installed under:

/payamavaran/

Main directories observed during investigation:

bin → system binaries and service executables
conf → base configuration files
config → system service configurations
radius → FreeRadius server installation
www → web interface and management panel

---

# System Architecture Overview

Typical deployment architecture:

ISP Router / Mikrotik
│
▼
FreeRadius
│
▼
Billing Engine
│
▼
MariaDB
│
▼
Web Panel

Authentication flow:

User Device → Router → Radius → Billing → Database

---

# Repository Structure

deltasib-system-analysis/

README.md
LICENSE

investigation/
filesystem_analysis.md
database_analysis.md
service_architecture.md

commands/
system_commands.txt
investigation_commands.txt

findings/
licensing_system.md
radius_integration.md

diagrams/
system_architecture.png
billing_flow.png

notes/
migration_plan.md
open_source_replacement.md

---

# Investigation Sections

## Filesystem Analysis

This section documents the internal layout of the DeltaSIB installation including:

* binary executables
* configuration directories
* web interface files
* service components

Location:

investigation/filesystem_analysis.md

---

## Database Analysis

This section contains research about:

* database schema
* important tables
* system state storage
* authentication records

Location:

investigation/database_analysis.md

---

## Service Architecture

This section explains:

* how system services communicate
* FreeRadius integration
* web interface interaction
* backend components

Location:

investigation/service_architecture.md

---

# Commands Used During Investigation

All system commands used during the investigation are recorded for reproducibility.

Examples include:

* filesystem enumeration
* service inspection
* database queries
* USB hardware checks
* binary analysis

Location:

commands/system_commands.txt
commands/investigation_commands.txt

---

# Key Findings

The research currently focuses on:

* licensing mechanism behavior
* radius authentication integration
* internal system architecture
* service communication patterns

Location:

findings/

---

# Diagrams

System diagrams will be stored here:

diagrams/

Examples:

system_architecture.png
billing_flow.png

These diagrams help visualize the interaction between:

* ISP router
* Radius authentication
* Billing backend
* Database
* Web panel

---

# Future Work

Planned future work includes:

* deeper binary analysis
* database schema mapping
* service dependency documentation
* open-source architecture design
* migration roadmap

Notes and planning files are stored under:

notes/

---

# Disclaimer

This repository documents system architecture and technical investigation for educational and research purposes.

The goal is to understand how ISP billing systems operate and to explore open alternatives that can replace proprietary infrastructure in the future.

---

# Author

System investigation performed by the system administrator responsible for maintaining the DeltaSIB environment.
