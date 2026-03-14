# Licensing System Analysis

This document describes the observed licensing and lock mechanism used by the DeltaSIB system.

The purpose of this analysis is to understand how the platform verifies its operational status and retrieves system lock information.

---

# Overview

During filesystem investigation, several components were identified that appear to be related to the system licensing mechanism.

Key elements include:

* backend binaries
* web interface scripts
* internal service commands

These components interact to determine the operational state of the system.

---

# Lock Information Retrieval

A key discovery was a web interface script responsible for retrieving system lock information.

Observed script:

config/www/cgi-bin/DSLockInfo.php

Example behavior of the script:

```php
$lockinfo = shell_exec("/bin/pak.lockinfo");
echo $lockinfo;
```

The script executes a backend binary that returns lock information.

---

# Lock Information Binary

The binary responsible for returning system lock information is:

/payamavaran/bin/lockinfo

This executable appears to generate information related to system state and licensing.

The exact internal logic of the binary is not visible without deeper binary analysis.

---

# Lock Update Mechanism

Another observed component involved updating lock information through network communication.

Example command discovered during investigation:

pak.radius.lock.update.sh

The script appears to send a Radius accounting request.

Example command pattern observed:

Acct-Status-Type='17',User-Name='UpdateLockInfo'

This request is sent through a Radius client.

This suggests that lock information may be synchronized through Radius accounting messages.

---

# UDP Communication

Another component discovered during investigation was a UDP client used to retrieve lock information.

Example usage pattern:

pak.udpclient 127.0.0.1 1500 3000 showlockinfo

This suggests that a local service may be running that returns system state information through a UDP interface.

---

# License Information Flow

Based on current observations, the licensing information flow may resemble the following structure.

System service requests lock information

```
    │
    ▼
```

Backend binary retrieves lock status

```
    │
    ▼
```

Information returned to web interface

```
    │
    ▼
```

Administrator panel displays system state

---

# Hardware Investigation

During investigation, USB device checks were performed to determine if a hardware dongle was present.

Commands used:

lsusb

and

dmesg | grep usb

Results showed only system USB controllers and no dedicated licensing device.

This suggests that either:

* the license system does not rely on a USB dongle in this environment, or
* the hardware key was not present during the inspection.

---

# Observed Licensing Components

The following components appear to be related to licensing or lock management.

Binary programs:

lockinfo

Scripts:

pak.radius.lock.update.sh

Web interface components:

DSLockInfo.php

These elements interact to retrieve and display system lock information.

---

# Observational Notes

The lock mechanism appears to be implemented using a combination of:

* compiled binaries
* shell scripts
* web interface scripts
* Radius accounting messages
* local service communication

Further investigation would require deeper analysis of the binary components.

---

# Future Research

Further investigation could include:

* analyzing lockinfo binary behavior
* inspecting UDP communication services
* mapping lock update processes
* understanding how system state is stored in the database

These areas are relevant when considering possible future architecture designs.

---

# Related Documents

Additional information about system architecture can be found in:

investigation/filesystem_analysis.md
investigation/service_architecture.md
