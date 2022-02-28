# PSS®ODMS Database

## Overview

The PSS®ODMS database is built on commercial relational database
software. The complete set of network model and graphical data is
centrally stored in the database and accessible to multiple users.

PSS®ODMS supports Microsoft SQL Server and Oracle. Refer to the
following chapters for deployment details. In most cases, procurement
and setup of the necessary hardware, operating system, database software
and network infrastructure is performed by the customer's IT department,
with hands-on assistance from Siemens PTI for the final
PSS®ODMS-specific configuration tasks. Once this has been completed, it
will be possible for PSS®ODMS users to connect to the database.

*Note: Oracle deployment involves additional client-side prerequisites
and database server configuration. Additionally, PSS®ODMS performance on
Oracle tends to be generally slower than on SQL Server.*

## Server Requirements

|                       |                                               |
|:--------------------- |:--------------------------------------------- |
| **Operating System**  | any OS compatible with the database platform  |
| **CPU**               | 2.6 GHz (minimum)                             |
| **Memory**            | 16 GB RAM (minimum)                           |
| **Hard Disk**         | 500 GB (minimum), SSD recommended             |
| **Database Software** | Microsoft SQL Server or Oracle                |

If the server which hosts the database is running Windows, the PSS®ODMS
application can be installed on the server machine itself for
convenience of certain procedures such as model backup and recovery.
