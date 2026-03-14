# Filesystem Analysis

This document describes the filesystem structure of the DeltaSIB billing system as discovered during the system investigation.

The primary installation directory of the system is:

```
/payamavaran/
```

The majority of binaries, configuration files, services, and web interface components are stored within this directory.

---

# Root System Directory

```
/payamavaran/
```

Observed structure:

```
bin/
conf/
config/
radius/
www/
```

Each of these directories serves a different role in the platform.

---

# /payamavaran/bin

This directory contains compiled system binaries used by the billing platform.

Observed contents include executables responsible for network control, logging, notifications, and reporting.

Example listing:

```
ldap
lockinfo
pakdisconnect
pakjetflowmerge
pakmikrotikrate
paknetlogd
paknotify
pakurlreporting
wwwfinishd
```

Key binary discovered:

```
lockinfo
```

This binary appears to be related to the internal licensing or lock management system.

The exact behavior of this binary requires deeper analysis.

---

# /payamavaran/conf

This directory stores base configuration files for system components.

Observed files:

```
radiusd.conf
sql.conf
user.conf
```

These files appear to control FreeRadius authentication behavior and database connectivity.

---

# /payamavaran/config

This directory contains configuration files for services and infrastructure components.

Subdirectories observed:

```
db/
httpd/
jetflowd/
monit.d/
mysql/
raddb/
www/
```

Purpose of each component:

db/
Database configuration templates and scripts.

httpd/
Apache web server configuration files.

jetflowd/
Network flow monitoring configuration.

monit.d/
Service monitoring configuration.

mysql/
Database configuration for the billing system.

raddb/
FreeRadius configuration files.

www/
Web interface configuration.

---

# /payamavaran/radius

This directory contains the full FreeRadius installation used for authentication.

Observed structure:

```
bin/
etc/
include/
lib/
sbin/
share/
var/
```

FreeRadius is used by the billing system to authenticate ISP users through routers and access servers.

Authentication flow:

```
Router → FreeRadius → Billing system → Database
```

---

# /payamavaran/www

This directory contains the web interface of the billing system.

Typical components found in this directory include:

* PHP scripts
* CGI programs
* web interface modules
* authentication interfaces
* reseller panels
* administrator tools

Example discovered script:

```
config/www/cgi-bin/DSLockInfo.php
```

This script executes a binary to retrieve system lock information.

Example code behavior:

```
shell_exec("/bin/pak.lockinfo")
```

This suggests that licensing information is retrieved through a backend binary.

---

# System Observations

From filesystem analysis, the DeltaSIB platform appears to be composed of several major layers:

1. Network Authentication Layer

   * FreeRadius server

2. Billing Engine Layer

   * Custom binaries located in /payamavaran/bin

3. Database Layer

   * MariaDB/MySQL

4. Web Interface Layer

   * Apache + PHP

---

# Preliminary Architecture

```
ISP Router
   │
   ▼
FreeRadius
   │
   ▼
Billing Engine
   │
   ▼
Database
   │
   ▼
Web Interface
```

---

# Next Investigation Areas

Further analysis should focus on:

* database schema
* system binaries
* license mechanism
* service communication
* authentication pipeline

These topics are covered in the following documents:

```
database_analysis.md
service_architecture.md
```
