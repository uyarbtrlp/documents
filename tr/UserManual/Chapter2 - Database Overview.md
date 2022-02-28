# Database Overview

## The Data Repository

The PSS®ODMS Data Repository is built on commercial database technology
to support a multiuser client-server solution; clients have the choice
of Oracle or Microsoft SQL Server. Clients are responsible for
purchasing, installing and maintaining their own LAN and database
platform. Essentially, the Data Repository is a CIM-based schema
definition implemented on an Oracle or Microsoft SQL Server relational
database platform.

![Data Repository](/images/PSSODMS_UserManual_2014-10-17114243_img_5.png)

## Connecting to the Database

Each PSS®ODMS workstation needs to be able to connect to the database
server. For optimal performance, it is recommended that the client's IT
department allocate a dedicated database server to host the Data
Repository. The PSS®ODMS application connects to the database using the
appropriate database drivers, which must be properly installed on each
workstation. Oracle and SQL Server have different client-side
prerequisites. For more detailed information, refer to the PSS®ODMS
Installation Guide.

On Oracle, some key PSS®ODMS functions require a special user account
named ODMSCTRL with administrative privileges. This administrative
account enables PSS®ODMS to instantiate, copy, delete and import/export
instances of network models (sometimes referred to as schemas). During
the initial database configuration, the ODMSCTRL user password is
defaulted to SMDO2005 (case insensitive). If necessary, this password
can be changed by a Database Administrator.

After the database client and server components have been installed and
configured, the PSS®ODMS user can open any Model within the Data
Repository. To open a Model, use File>Open Database and pick the
appropriate database type and server. The Open Database dialog will
present a list of all the existing Models contained in the selected
database.

![Open Database Dialog](/images/C2_Open_Database_Dialog.png)

Note: Only one Model may be opened at a time in a single PSS®ODMS
instance; to work with multiple Models simultaneously, multiple PSS®ODMS
instances of may be launched.

Note: The Open Database dialog behavior varies somewhat depending on the
selected database platform. For example, SQL Server has the option to
use integrated security.

## Model Management

PSS®ODMS provides functions to import data (in various formats) into the
Data Repository. Each time the user runs a full model import function,
PSS®ODMS creates a new Model instance in the Data Repository. A Model is
a comprehensive collection of data including the complete static network
topology and engineering attributes (based on the CIM standard),
graphics data, external mappings, etc. A Model may also contain
historical and/or future network changes. In PSS®ODMS, a Model typically
represents a specific portion of the transmission network grid. The
number of Model instances that can exist within the Data Repository is
limited only by disk storage space.

With Oracle database, PSS®ODMS needs a password to open a database
connection to a given Model. The password for each new Model is
automatically defaulted to the Model name. For example, if you create a
Model named \"SAVNW1\" using the PSS®E Import function, then the
password will be defaulted to \"SAVNW1.\". With SQL server, password is
not required as PSS®ODMS uses Microsoft^®^ Windows user authentication
(Integrated Security).

![Multiple Models in the Data
Repository](/images/PSSODMS_UserManual_2014-10-17114243_img_7.png)

Note: In the above diagram, the Oracle term \"schema\" is used to
indicate a model instance.

## Security

PSS®ODMS maintains security and system integrity exclusively through the
operating system (Windows network) and commercial database accounts. No
internal (PSS®ODMS specific) user names or passwords are required.

The first level of security is the Windows user name and password. This
allows for a password-protected Administrator account as well as user
accounts. The operations a user can perform are restricted to the
permissions in their profile. These can be required items for system
logon and implemented according to security practices that may already
be in place at a given company.

The second level of security is achieved by using a database that
requires a user name and/or password for access. The database platform
itself also commonly provides additional security implementation at the
table, record, and field levels.

Whenever a new Model instance is about to be created, PSS®ODMS will
prompt the user for the Model name. On Oracle, this will result in the
creation of a new User/Schema and default password of the same name. If
additional security is required, a Database Administrator can change the
account password; a PSS®ODMS user will need to enter the corresponding
password to connect to the Model.

The third level of security is provided by PSS®ODMS licensing options
and configurable user Roles and Privileges (described in detail in
supplemental product documentation.

## Migrating from Oracle to SQL Server

For additional flexibility, PSS®ODMS provides a convenient function to
convert any database model from Oracle to SQL Server format with no loss
of data.

IMPORTANT: This function requires all client-side prerequisites for both
Oracle and SQL Server database platforms to be installed. Refer to the
PSS®ODMS Installation Guide for details.

![Migrate to SQL Server](/images/C2_Migrate_To_SQL.png)
