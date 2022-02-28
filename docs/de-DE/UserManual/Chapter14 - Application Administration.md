# Application Administration

## Introduction

This chapter contains information which is primarily relevant to system
adminstrators.

## Command Line Arguments

PSS®ODMS supports the following command line arguments:

-   database=\[SQL or ORA\]

-   server=\[server name\]

-   pwd=\[Oracle user password\]

-   case=\[fully qualified saved case path in quotes\]

-   case_browser=\[fully qualified directory path in quotes\]

-   diagram=\[saved diagram name\]

-   script=\[fully qualified Python script path in quotes\]

-   script_params=\[Python script parameters in quotes\]

-   hide_gui

Example command line invocation:

c:\\Program Files\\PTI\\ODMS\\ODMS.exe database=SQL server=.\\sqlexpress
model=MyModel case=\"c:\\saved_cases\\MyCase.sav\"
case_browser=\"c:\\saved_cases\" diagram=Overview

c:\\Program Files\\PTI\\ODMS\\ODMS.exe
script=\"c:\\scripts\\MyScript.py\" script_params=\"0,1,SUB1\" hide_gui

## User Authorization

The PSS®ODMS application contains special user authorization logic to
promote critical data security. User roles and associated privileges can
be created and maintained with a high degree of flexibility. This
information is stored within the PSS®ODMS database model itself. The
PSS®ODMS User Management utility program allows system administrators to
do this quickly and easily. The utility supports the creation and
editing of user Roles, Privileges and Groups. It is a small, standalone
program that can be run directly on your Windows database server or on
any client workstation. To begin using this utility, first obtain
ODMSUserManagement.exe from Siemens PTI.

The first time PSS®ODMS User Management is run, you will need to set the
connection to your database server using the File>Open Database command.
In the Open Database dialog, enter the database type and server name.
With Oracle, you also need to enter the ODMSCTRL user password as shown
below. If the default ODMSCTRL user password was changed, you will need
to obtain the current password from your DBA.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_173.png)

After establishing a connection to the database, the left panel displays
a list of all the PSS®ODMS models within the database. Expand any model
to view its Users, Privileges, Roles and Groups.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_174.png)

Each user should be assigned a role. Two default roles (Operator and
Administrator) are created automatically by the software; you can modify
them or create as many new roles as needed. For convenience, whenever
PSS®ODMS opens a database connection, the associated Windows user name
is added to the Users table if not already there.

Expand the Privileges item. This list is populated by the software and
should not be modified. Most privileges are self-explanatory and are
related to specific Project Modeling features; however, a few important
privileges are more general, such as \"EditBaseModel\" and
\"EditDiagram.\" Privileges may be added to or removed from specific
roles as desired. If no association exists between a given role and
privilege, then the corresponding functionality will be disabled in
PSS®ODMS for each user assigned to that role.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_175.png)

When different users log into the same workstation, various functions of
PSS®ODMS will be enabled or disabled accordingly. So for example, an
engineer user could temporarily log into an operator\'s workstation to
make a critical model change.

After configuring the database, there is an additional one-time setup
procedure required. On each PSS®ODMS workstation, run regedit.exe,
create a numeric value named Enable User Privileges under
HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\PTI\\ODMS (for 32 bit
PSS®ODMS) or HKEY_LOCAL_MACHINE\\SOFTWARE\\PTI\\ODMS (for 64 bit
PSS®ODMS) and set its value to 1. This enables PSS®ODMS database-driven
user roles/privileges on a workstation basis.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_176.png)

Alternatively, to enable or disable PSS®ODMS database-driven user
roles/privileges more selectively on an individual Windows user basis,
run regedit.exe and set the value of
HKEY_CURRENT_USER\\SOFTWARE\\PTI\\ODMS\\Enable User Privileges to 1 to
enable or 0 to disable. Note that the HKEY_LOCAL_MACHINE setting
overrides the HKEY_CURRENT_USER setting. Once the registry setting has
been enabled, for system security, if a user opens a database model in
PSS®ODMS in which he or she has not been assigned a role, then all
configurable privileges will be disabled by the software. Since this
method decouples user roles/privileges from the PSS®ODMS licensing and
registration process, the same license file can be used to register all
workstations, regardless.

## Extending the Database Schema

To add your own custom data extensions to the PSS®ODMS database schema,
first create a file named customer.sql in either the \\Oracle\\ or
SQLServer\\ subdirectory of the PSS®ODMS installation directory and add
the DDL to specify the data extensions. If it exists, customer.sql will
be automatically executed by LoadAll.sql during model instance
initialization. This file will not be overwritten by the PSS®ODMS
installer when upgrading. Note: when extending the schema to model
many-to-many associations, the table name must end with the word \"Map\"
(Case Sensitive). See existing examples such as PsrToCompanyMap and
MeasurementToLimitSetMap for references.

### Enabling PSS®ODMS support

To enable full PSS®ODMS support for exensions (including CIM/XML import
and export functions, CIMedit interface and CIMdbNET API), the following
is required. All custom resource entries should be ResourceType=1 for
Class, 2 for Enumeration, or 3 for Property or Association. Verify that
they are created in the reserved range (ODMSID \> 2147345000). Each
Class resource requires an entry to be created in the Class table. Each
Enumeration resource requires an entry to be created in the Enumeration
table. Each Property resource requires an entry to be created in the
Property table. Each Association resource requires two entries to be
created in the Association table: one entry for the association and one
for its inverse. There are stored procedures for creating these entries
(refer to PTI.sql in the DBTemplates directory for examples of their
use). These stored procedures should be called by the customer.sql
script.

### PSS®ODMS model upgrade process {#section_wm4_nbl_xp}

Custom schema extensions are supported by the built-in PSS®ODMS model
upgrade process as long as the extensions are properly implemented as
described above using the customer.sql file. The model upgrade process
is outlined here for reference.

1.  Disable constraints and triggers.

2.  Apply PreProcess scripts (PreProcess-Rev\<old>To\<new>.sql - old and
    new versions are defined by data in the PTISchemaVersion table).
    This file is only necessary if the standard copy process (described
    in 3) cannot function without extra processing. Examples include new
    columns defined as NOT NULL with no DEFAULT specified, calculated
    values, tables that are erroneously copied, etc. Tables that are
    processed using this file will not be further processed by the copy
    data procedure.

3.  Copy data from old tables to new tables.

    a.  Every table owned by the user in the ODMS_TAB tablespace,
        (INSERT INTO SELECT \*). This gets all tables that have not
        changed since the previous version. Note that this method allows
        for column name changes since the column names are not used,
        only the values contained in them

    b.  If the above fails and the old table has no data, skip it.

    c.  For all remaining tables, build an insert statement. Columns
        that have the same name go to the same columns in the new
        version. If the column didn\'t exist in the old schema, either
        NULL or DEFAULT values are inserted.

4.  Enable triggers (constraints remain disabled).

5.  Apply PostCopy scripts (PostCopy-Rev\<old>To\<new>.sql). Any needed
    post-processing that should be done after all data is copied over
    should be done here.

6.  Enable and check constraints.

### Further considerations

Adding attributes to existing CIM classes/tables is by far the simplest
and most straightforward approach to adding custom extensions. Extending
classes by inheriting from existing CIM classes is much more difficult
in some situations. It is not advised to create these types of
extensions as they must typically be handled manually by the customer by
using triggers and stored procedures which adds complexity and will
impact overall performance. Extended classes may be used as long as they
inherit from one of the abstract CIM classes (IdentifiedObject,
PowerSystemResource, etc). If they inherit from one of the concrete
classes as defined in the CPSM or ENTSO-E profiles (Switch, Breaker,
BusbarSection, ACLineSegment, etc), then special care must be used. The
TableName column in the Resources table for the extended class must be
the most-derived CIM class name and not the extended class name. Foreign
keys to/from extended classes must be handled appropriately by triggers
as needed to handle cases when an instance (ResourceType=4) is added or
deleted from the model. ODMS has not been extensively tested with
schemas using extensions to CIM classes, so adequate testing should be
done if using this type of extension. Inserting extended classes into
the CIM inheritance hierarchy is currently not supported, unless it is
dealing with a part of the CIM that ODMS currently does not natively use
(i.e. ICCP/SCADA packages, Asset packages, etc - anything not dealing
with network topology or case build features). Instance data
(ResourceType = 4) that is added to the model during schema creation
(via customer.sql) must be handled appropriately. If the number of
instances **will not change** then it is safe to add them in the
\"normal\" range of ODMS IDs (between 0 and 2147345000) by adding them
at the end of the LoadAll.sql script after the sequence/identity is
reset, otherwise you should consider adding them in a separate reserved
range that is well above the range used by the CIM metadata and extended
attributes. If this is not done, then there may be overlapping of
ODMSIDs during a schema copy, causing any copy functions (upgrades, etc)
to fail.
