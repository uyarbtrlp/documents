# Oracle Setup

## Overview

This chapter provides general instructions for deploying PSS®ODMS on an
Oracle database platform. These steps should be performed by a DBA or
other qualified IT personnel.

## Database Setup

The PSS®ODMS database may be hosted by a server machine running any
Oracle-supported operating system (e.g. Linux); however, the PSS®ODMS
client application supports Windows only.

### Install Oracle

Refer to the official Oracle documentation for installation
instructions. PSS®ODMS supports Oracle 12c Release 2 (12.2.0.1 minimum)
or higher.

To avoid potential localization issues, the \'Use Unicode (AL32UTF8)\'
character set option is recommended. The default language and territory
options should be set according to your local region.

For an enterprise deployment with a high-availability requirement, be
aware of additional required Oracle server software as well as all
related hardware and networking prerequisites and set up the server
cluster accordingly.

### Create Database Connection Entry

The PSS®ODMS database can be configured on any existing Oracle server
using either the Easy Connect or Local Naming methods. The Easy Connect
naming method eliminates the need for service name lookup in the
TNSNAMES.ORA files for TCP/IP environments. No naming or directory
system is required if you use this method. For more information on the
two naming methods, please refer to Section 8 of the Oracle Database Net
Services Administrator's Guide:

For Oracle 11g:
http://docs.oracle.com/cd/E11882_01/network.112/e10836/naming.htm

For Oracle 12c:
http://docs.oracle.com/cd/E16655_01/network.121/e17610/naming.htm

### Create Tablespaces and ODMSCTRL User

Two SQL files, cr_odmsctrl.sql and cr_tablespace.sql, are located under
the PSS®ODMS installation directory under the
\\DBTemplates\\Oracle\\Setup subdirectory. Edit cr_tablespaces.sql as
needed to specify the correct path for the Oracle data directory on the
server. Log into Oracle as user SYS, import both scripts and execute
them. Verify the tablespace files were created. Test logging into Oracle
as user ODMSCTRL (default password SMDO2005).

### Performance Optimization

There is a "parallel queries" setting which may be enabled by default.
For optimal performance of PSS®ODMS, this option needs to be explicitly
disabled as shown below.

**ALTER SYSTEM SET PARALLEL_MAX_SERVERS=0;**

## Workstation Setup

First, verify the hardware and third-party software prerequisites in
Chapter 2. The steps below must be performed in addition to (either
before or after) the PSS®ODMS application installation process described
in Chapter 2.

### Install Oracle Client

Use the Oracle Universal Installer to install the version of Oracle
Client that corresponds to your version of Oracle Server (11.2.0.4
minimum or 12.1.0.2 minimum). The traditional 32-bit version of PSS®ODMS
requires the 32-bit version of Oracle Client; the new 64-bit version of
PSS®ODMS requires the 64-bit version of Oracle Client. The following
components are required:

-   Oracle Client

-   Oracle Net

-   Oracle SQL\*Plus

-   Oracle Database Utilities

-   Oracle Provider for OLE DB

-   Oracle ODBC Driver

#### Oracle.ManagedDataAccess.dll

Oracle.ManangedDataAccess.dll version 4.122.1.0 is an additional
client-side prerequisite which can be downloaded from one of the
following links and installed manually.

32-bit version:
http://www.oracle.com/technetwork/database/windows/downloads/utilsoft-087491.html

64-bit version:
https://www.oracle.com/technetwork/database/windows/downloads/index-090165.html

Download ODP.NET_Managed_ODAC122cR1.zip (see image below)

![](/images/OracleManageDll.jpg)

Open the zip file and extract Oracle.ManagedDataAccess.dll from
odp.net\\managed\\common to the PSS®ODMS installed directory containing
ODMS.exe.

### Configuring Local Naming Methods

If using Local Naming methods, the TNSNAMES.ora file will need to be
copied to the PSS®ODMS installed directory.

Alternatively, the ODMS.exe.config located in the PSS®ODMS installed
directory can be edited to reflect the location of the TNSNAMES.ora
file. Uncomment the section below and adjust the TNS_ADMIN path to point
to the location of the TNSNAMES.ora on your environment.

![](/images/ODMSConfig2.png)

### Localization

IMPORTANT: The Oracle NLS_LANG registry setting must be consistent with
the Windows Region and Language settings on each workstation
(particularly related to the decimal symbol convention) and all
workstations must configured consistently.
