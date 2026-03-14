# Database Analysis

This document describes the database investigation performed on the DeltaSIB billing system.

The platform relies on a MariaDB/MySQL database to store system configuration, authentication records, billing data, and system state information.

---

# Database Engine

Observed database engine:

MariaDB

Typical connection method used during investigation:

mysql -u root -p deltasib

The primary database used by the platform is:

deltasib

---

# Database Purpose

The database acts as the central data layer for the billing platform.

It stores information related to:

* user authentication
* billing records
* system configuration
* reseller accounts
* service plans
* system state information

The database is accessed by:

* FreeRadius authentication services
* billing system backend processes
* the web administration interface

---

# Database Access Flow

Typical architecture:

Router / NAS
│
▼
FreeRadius Server
│
▼
Billing Backend
│
▼
MariaDB
│
▼
Web Management Panel

Authentication requests from network devices are validated through FreeRadius, which then communicates with the billing backend and database.

---

# Important Observed Tables

During investigation, one of the important system tables discovered was:

system_state

This table appears to maintain internal state information for the platform.

Example structure observation:

system_state

Columns observed:

* UpdatedAt

This column stores timestamp information related to system updates.

---

# Timestamp Handling

During investigation an issue appeared while attempting to modify the table schema.

Attempted query:

ALTER TABLE system_state MODIFY UpdatedAt DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP;

Result:

ERROR 1067 (42000): Invalid default value for 'UpdatedAt'

This error occurs on older MariaDB/MySQL configurations where DATETIME columns cannot use CURRENT_TIMESTAMP as a default value.

Possible workaround approaches include:

1. Using TIMESTAMP instead of DATETIME

Example:

ALTER TABLE system_state MODIFY UpdatedAt TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;

or

2. Removing the default constraint and allowing the application layer to set timestamps.

Example:

ALTER TABLE system_state MODIFY UpdatedAt DATETIME NOT NULL;

---

# Database Investigation Commands

The following commands were used during the investigation.

Connect to database:

mysql -u root -p deltasib

List tables:

SHOW TABLES;

Describe table structure:

DESCRIBE system_state;

View table contents:

SELECT * FROM system_state;

Inspect column definitions:

SHOW CREATE TABLE system_state;

---

# Configuration Files Referencing Database

Database configuration references were discovered in the filesystem under:

/payamavaran/conf/

Example configuration files:

radiusd.conf
sql.conf

These files typically contain database credentials used by FreeRadius.

Another configuration directory related to database setup:

/payamavaran/config/mysql/

---

# Role of Database in System Operation

The database acts as the core information storage for the platform.

It is used by:

FreeRadius
to verify authentication requests.

Billing engine
to process user accounts and service plans.

Web interface
to display and manage system information.

---

# Security Considerations

Database credentials are typically stored in configuration files.

Care must be taken to protect:

* database usernames
* passwords
* connection strings
* system configuration tables

Exposure of these values could allow unauthorized access to billing data.

---

# Future Database Investigation

Further research should include:

* full schema mapping
* table relationships
* billing record structures
* authentication tables
* accounting data tables
* reseller account management

This information will be useful when designing a possible open-source replacement architecture.

---

# Related Documents

Additional architecture information can be found in:

service_architecture.md
