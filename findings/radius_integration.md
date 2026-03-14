# Radius Integration Analysis

This document describes how the DeltaSIB platform integrates with FreeRadius to provide authentication, authorization, and accounting for ISP subscribers.

FreeRadius acts as the central AAA (Authentication, Authorization, Accounting) server in the network infrastructure.

---

# Role of FreeRadius

FreeRadius is responsible for validating subscriber credentials when users attempt to access the internet.

Network devices such as routers and NAS gateways send authentication requests to the Radius server.

Typical devices that interact with Radius include:

* Mikrotik routers
* PPPoE servers
* hotspot gateways
* NAS access devices

These devices communicate with the Radius server using the standard Radius protocol.

---

# Radius Installation Location

The FreeRadius installation discovered during investigation was located at:

/payamavaran/radius/

Observed directory structure:

bin/
etc/
include/
lib/
sbin/
share/
var/

This indicates that the billing platform ships with its own bundled FreeRadius environment.

---

# Radius Configuration

Radius configuration files were found under:

/payamavaran/config/raddb/

Important configuration files typically include:

clients.conf
radiusd.conf
sql.conf
users

These files define how authentication requests are processed.

---

# SQL Integration

The Radius server appears to be integrated with the MariaDB database.

Database credentials are typically stored inside:

/payamavaran/conf/sql.conf

Through this configuration, Radius can query the billing database to verify user credentials and account status.

---

# Authentication Flow

The authentication process follows a standard ISP AAA model.

Step-by-step flow:

1. User device attempts to connect to the internet.

2. The router or NAS sends a Radius Access-Request packet.

3. FreeRadius receives the authentication request.

4. Radius queries the billing database.

5. The billing system verifies the user account.

6. Radius returns either:

Access-Accept
or
Access-Reject

7. If accepted, the user is granted network access.

---

# Accounting Flow

After authentication, Radius can also track user session data.

Accounting information may include:

* session start time
* session end time
* bandwidth usage
* IP address assigned
* service plan applied

Accounting records are typically written into the database for billing and reporting.

---

# Radius and Billing Engine Interaction

The billing platform appears to interact with Radius through:

* SQL queries
* accounting records
* session management commands

Some backend binaries likely interact with Radius to perform tasks such as:

* disconnecting users
* updating session limits
* enforcing service plans

---

# Example Operational Flow

Subscriber login attempt:

User Device
│
▼

ISP Router
│
▼

Radius Access Request
│
▼

FreeRadius Server
│
▼

Billing System Database
│
▼

Authentication Result

---

# Service Dependencies

The correct operation of the billing system depends on several services working together:

FreeRadius
MariaDB
Apache Web Server
Billing Engine Binaries

If any of these components fail, subscriber authentication may be affected.

---

# Investigation Observations

During the investigation the following observations were made:

* FreeRadius is embedded inside the platform installation
* configuration files are located within the system directory
* the database is tightly integrated with Radius
* the billing system likely controls user session behavior

---

# Future Research

Further investigation should include:

* detailed Radius configuration mapping
* database schema analysis for authentication tables
* accounting record storage
* session management behavior

Understanding these components is important when designing a possible open architecture replacement.

---

# Related Documents

Additional architecture information can be found in:

investigation/service_architecture.md
findings/licensing_system.md
