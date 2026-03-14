# Service Architecture

This document describes the service architecture of the DeltaSIB ISP billing system as observed during the system investigation.

The platform appears to be composed of multiple layers working together to provide authentication, billing management, and administrative control for an Internet Service Provider network.

---

# High Level Architecture

The system integrates several components that communicate together.

Typical architecture observed:

ISP Router / NAS
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
Web Management Panel

Each component plays a specific role within the platform.

---

# Main Components

The system can be divided into the following major layers.

1. Network Authentication Layer
2. Billing Logic Layer
3. Database Layer
4. Web Management Layer

---

# Network Authentication Layer

Authentication of internet subscribers is handled through **FreeRadius**.

FreeRadius is located under:

/payamavaran/radius/

This service receives authentication requests from ISP network devices such as:

* Mikrotik routers
* NAS devices
* PPPoE servers
* Hotspot gateways

Typical authentication flow:

User Device → Router → Radius → Billing System

FreeRadius validates user credentials using information stored in the billing database.

---

# Billing Engine Layer

The billing logic appears to be implemented through several system binaries located in:

/payamavaran/bin/

Observed binaries include:

ldap
lockinfo
pakdisconnect
pakjetflowmerge
pakmikrotikrate
paknetlogd
paknotify
pakurlreporting
wwwfinishd

These binaries appear to perform tasks such as:

* network accounting
* session tracking
* service plan enforcement
* user disconnection
* network traffic reporting

These programs likely communicate with the database and authentication services.

---

# Database Layer

The system uses **MariaDB / MySQL** as the main data storage engine.

The primary database observed:

deltasib

The database stores critical system data such as:

* user accounts
* billing records
* authentication information
* service plans
* system configuration
* session accounting records

Database configuration is referenced in:

/payamavaran/conf/sql.conf

---

# Web Management Layer

The administrative web interface allows system operators to manage the ISP billing platform.

This interface is typically served through **Apache HTTP Server**.

Observed web interface path:

/payamavaran/www/

The web interface appears to include:

* administrator dashboard
* reseller management
* user management
* service configuration
* billing reports

Some backend functionality is implemented through CGI scripts.

Example observed:

config/www/cgi-bin/DSLockInfo.php

This script retrieves system lock information using backend binaries.

---

# Service Monitoring

Service monitoring configuration was observed in:

/payamavaran/config/monit.d/

This suggests the system uses **Monit** to monitor and restart services if they fail.

This helps maintain stability of critical system components.

---

# Radius Configuration

Radius configuration files were found under:

/payamavaran/config/raddb/

These files define:

* authentication methods
* SQL integration
* accounting behavior
* user policies

FreeRadius communicates with the database to verify subscriber credentials.

---

# Logging and Reporting

Some system binaries appear responsible for logging and reporting.

Example binaries:

paknetlogd
pakurlreporting

These likely generate usage reports and store accounting data.

---

# Internal Communication

The platform appears to communicate internally through:

* database queries
* system binaries
* shell execution from PHP scripts
* Radius authentication modules

This layered architecture allows the platform to handle large numbers of ISP subscribers.

---

# Preliminary Service Flow

Subscriber attempts internet connection

```
    │
    ▼
```

Router sends authentication request

```
    │
    ▼
```

FreeRadius validates credentials

```
    │
    ▼
```

Billing system verifies account status

```
    │
    ▼
```

Database stores session and accounting data

```
    │
    ▼
```

User receives network access

---

# Future Architecture Investigation

Further research should focus on:

* internal service communication
* network accounting process
* database schema relationships
* binary functionality
* licensing system integration

These topics are documented in:

findings/licensing_system.md
findings/radius_integration.md

---

# Summary

The DeltaSIB billing system appears to be a layered ISP management platform combining:

FreeRadius authentication
custom billing engine binaries
MariaDB database storage
Apache web management interface

This architecture is typical for ISP AAA (Authentication, Authorization, Accounting) systems.
