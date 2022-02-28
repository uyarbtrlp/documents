# SQL Server Setup

## Overview

This chapter provides instructions for deploying PSS®ODMS on a Microsoft
SQL Server database platform. These steps should be performed by a DBA
or other qualified IT personnel.

## SQL Server Standard or Enterprise Edition

### Install SQL Server

**PSS®ODMS supports SQL Server 2017 or higher. Before upgrading an
existing SQL Server installation, be sure to export the PSS®ODMS
database model(s) to .bak format for migration to the new database.**

The SQL Server database should reside on the same network domain and
subnet as the PSS®ODMS workstations.

Windows authentication is the only authentication mode supported by
PSS®ODMS; be sure to pick this option during the installation process.

For an enterprise deployment with a high-availability requirement, be
aware of the required SQL Server database software as well as all
related operating system, hardware and networking prerequisites and set
up the server cluster accordingly. Note that an \"active listener\"
service must be hosted on a separate domain controller server outside
the cluster.

### Add PSS®ODMS Users

Use SQL Server Management Studio to add all PSS®ODMS users (by Windows
user name) to the database. Certain administrative privileges are
required to create and delete database models with PSS®ODMS; this
applies to importing, copying, deleting, upgrading and restoring model
backups. When assigning SQL Server database user privileges, keep in
mind that built-in user authorization in PSS®ODMS can limit
functionality based on configurable user roles (refer to the
Administration chapter of the PSS®ODMS User Manual for details).

## SQL Server Express Edition

This section provides detailed instructions for deploying PSS®ODMS on a
local Microsoft SQL Server Express Edition database. Microsoft SQL
Server Express Edition is prerequisite for the Single-user Edition of
PSS®ODMS and may be installed on individual workstations in any Standard
or Enterprise deployment for additional flexibility as needed.

### Install SQL Server Express Edition

**PSS®ODMS supports SQL Server 2017 (or higher) Express Edition.**

Download the SQL Server Express Edition installer from the Microsoft
Download Center website.

Note: SQL Server Management Studio is recommended for local database
management.

Run the installer and accept the suggestions below:

1.  Select the \"Named instance\" option and enter \"sqlexpress\" (case
    insensitive).   
    ![](/images/Fig_6-2.png)

2.  Keep the default Server Configuration options.  
    ![](/images/Fig_6-3.png)

3.  Be sure to select the \"Windows authentication mode\" option. Use
    the Add Current User and/or Add button as needed to designate the
    SQL Server administrator(s).  
    ![](/images/Fig_6-4.png)

## Validate Configuration

This section provides instructions for validating the SQL Server
configuration after completing the required setup steps.

### Test Connectivity

Run PSS®ODMS and choose the File>Open Database command. Select the \"SQL
Server\" database type and corresponding server (to connect to a local
SQL Server Express Edition database, type in \".\\sqlexpress\" for the
server name). Expand the model name drop-down list (note: this may take
a few seconds, during which a wait cursor will be displayed). PSS®ODMS
models in the database should now appear in the drop-down list; if the
database does not yet contain any models, the list should be empty.

If this test is successful, no error messages will be presented. If an
error message occurs, first verify all previously described setup steps,
then contact Siemens PTI Support for further assistance as needed.

This test can be repeated after conducting the other tests described
below.

### Create a Model

Run PSS®ODMS and choose the Model>Operations>New Model command, set the
database type and server name consistent with the database connectivity
test and enter a valid SQL Server database name for the new model. If
this test is successful, the model creation process will complete
without error and the new model name will be displayed in the tile bar
of the PSS®ODMS main window.

### Delete a Model

With the model from the previous test open in PSS®ODMS, choose the
Model>Operations>Delete Model command and select OK when prompted to
delete the model. If this test is successful, the process will complete
without error and the deleted model name will no longer be displayed in
the tile bar of the PSS®ODMS main window.

### Import a Model

Run PSS®ODMS. If a database model is open from a previous test, close it
by using the File>Close Database command. Then choose the
Model>Import>PSS®E Model command and select one of the installed sample
RAW files from the SampleData subdirectory of the PSS®ODMS installation
directory to import. If this test is successful, the import process will
complete without error; the new model name will be displayed in the tile
bar of the PSS®ODMS main window and the contents of the model will be
visible in the CIMedit window.
