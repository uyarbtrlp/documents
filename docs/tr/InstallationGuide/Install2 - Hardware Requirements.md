# PSS®ODMS Setup

## Hardware Requirements

|                               |                                                               |
|---                            |---                                                            |
|  **Machine**                  | Microsoft Windows-compatible desktop, laptop, server or VM    |
| **Operating System**          | Windows 10 (64-bit) or Windows Server 2016 (or higher)        |  
| **CPU**                       | 2.6 GHz (minimum)                                             |
| **Memory**                    | 8 GB RAM (minimum)                                            |
| **Hard Disk**                 | 120 GB (minimum)                                              |
| **Graphics Card Resolution**  | 1280x720 (minimum)                                            |    


The minimum hardware requirements above apply to a typical Windows 10
workstation (laptop, desktop or VM) running PSS®ODMS along with other
installed software such as MS Office. By contrast, a dedicated
application server hosting multiple concurrent PSS®ODMS instances may
have substantially higher physical hardware requirements. As a general
rule of thumb, allocate 4 GB RAM per potential concurrent instance
(generally equal to the number of licensed current users). Required RAM
additionally increases to support very large network models, so it is
recommended to consult with Siemens PTI in these situations. Similarly,
deploying the Automated Case Creation add-on module with multiprocessing
requires additional CPU and RAM (e.g. 8 logical cores with 32 GB RAM).

## Third-Party Software

### General Prerequisites

The following prerequisite software must be installed on each PSS®ODMS
workstation or application server:

-   Microsoft .NET Framework 4.7.2 or higher

-   Python 3.8 for Windows (64-bit version)

    It is recommended to select the "Install for all users" option and
    specify an installation path directly under the c-drive (e.g.
    C:\\Python38). Be sure to select the option to add the Python
    installation path to the system path variable and verify this in the
    advanced system settings afterwards.

### SQL Server Prerequisites

To connect to an SQL Server database residing on a local network server,
no additional client-side software is required; however, for optimal
performance, the latest Microsoft OLE DB Driver for SQL Server is
recommended.

To deploy a standalone local database requires the following software:

-   Microsoft SQL Server Express Edition 2017 or higher

-   Microsoft SQL Server Management Studio (typically bundled with SQL
    Server Express Edition)

### Oracle Prerequisites

To connect to an Oracle 12c Release 2 database, Oracle Client version
12.2.0.1 or later must be installed on each PSS®ODMS workstation or
application server. Refer to Chapter 6 - Oracle Setup for details.

## PSS®ODMS Installation

The PSS®ODMS installer program is an MSI file which may be downloaded
from the Siemens PTI website (www.usa.siemens.com/odms-support) or
provided through a secure file exchange portal. Refer to the information
included with your software delivery notification. Administrative
privileges are required to install or uninstall PSS®ODMS.

### New Installation or Upgrade

Installing PSS®ODMS for the first time or upgrading a previous
installation requires running the provided installation program.
PSS®ODMS is a 64-bit Windows application and should typically be
installed in the C:\\Program Files directory. After successful
installation, PSS®ODMS will appear in the Windows Start menu.
Additionally, a dekstop icon will be created.

### Multiple Versions

Multiple versions of PSS®ODMS can exist in different directories on the
same machine. To preserve an older installation, either manually rename
the current installation directory (e.g. from \"ODMS\" to \"ODMS 11.7\")
prior to installing the new version or pick a different directory when
running the new installer. Note that the ability to uninstall older
version(s) of PSS®ODMS using Windows Control Panel will be affected.

**Important Considerations**

-   External processes using the .NET APIs as well as certain advanced
    PSS®ODMS functions require additional DLL registration. Locate file
    RegisterODMS.bat in the installation directory and choose the \"Run
    as administrator\" command prior to running the corresponding
    ODMS.exe.

-   Running different versions of PSS®ODMS simultaneously may cause
    unpredictable behavior.

-   When running an older version of PSS®ODMS, be aware that you will
    not be able to open a database model that has been upgraded to a
    newer PSS®ODMS version.

## Analysis Engine Dimensioning

The default configuration of the PSS®ODMS network analysis engine
supports detailed node-breaker models with up to 10000 planning buses
and 60000 nodes. A special configuration file can be edited as needed to
support larger models; please be aware that this may significantly
increase the amount of required physical RAM.

You can test if a given network model approaches or exceeds the
dimensions of the current engine configuration. To run a configuration
test, open a database model in PSS®ODMS and use the Analysis>Test
Configuration command. The resulting message box indicates if the test
passed or failed and the Output window displays detailed instance counts
against the maximum for each type. If necessary, you can increase the
dimensioning as follows:

1.  Shut down any running instances of PSS®ODMS.

2.  Navigate to the \\PSSO subdirectory of the PSS®ODMS installation
    directory in Windows Explorer.

3.  Copy file \"configration.xml\" to an editable local directory and
    open it for editing.

4.  Change the Bus value as needed (refer to the table below) and save
    the modified file.

5.  Copy the modified \"configuration.xml\" back to the PSSO
    subdirectory, overwriting the original file (requires administrative
    privileges).

6.  Run PSS®ODMS and run the configuration test. If necessary, repeat
    from step 4.

**Dimensioning Table**

 | Data type                    |      CIM class                        |            Size           |
 |:---------------              |:-------                               |:------                    |
 | Area                         | GeographicalRegion                    | 2000 (fixed)              |
 |  Zone                        | SubGeographicalRegion                 | 2000 (fixed)              |
 | Owner                        | OperatingParticipant                  | 2000 (fixed)              |
 | Substation                   | Substation                            | = Bus setting             |
 | PTC                          | PowerTransferCorridor                 | = 0.14 x  setting         |
 | Bus                          | TopologicalNode                       | = Bus setting             |
 | Section                      | ConnectivityNode                      | = 6 x Bus setting         |
 | Switch                       | Switch                                | = 6 x Bus setting         |
 | Line                         | ACLineSegment/SeriesCompensator       | = 1.05 x Bus setting      |
 | DC Line                      | DCLineSegment                         | 200 (fixed)               |
 | Transformer/Phase Shifter    | PowerTransformer                      | = 0.35 x Bus setting      |
 | Load                         | EnergyConsumer                        | = Bus setting             |
 | Unit                         | GeneratingUnit                        | = 0.5 x Bus setting       |
 | Bank                         | ShuntCompensator                      | = 0.3 x Bus setting       |
 | SVC                          | StaticVarCompensator                  | = 0.1 x Bus setting       |
 | Analog Measurement\*         | Analog                                | = 2 x Bus setting         |
 | Switch Measurement\*         | Discrete                              | = 4 x Bus setting         |
 | In Service Measurement\*     | Discrete                              | = 2 x Bus setting         |

\*Measurement dimensions only apply when the State Estimator module is
licensed, otherwise they are set to small limits by default to save
program memory usage (e.g. the maximum number of analog measurements is
set to 20).

**Important Considerations**

-   Configuration is on a per-machine (not per-user) basis.

-   The current configuration is displayed in the PSS®ODMS status bar.

-   The minimum Bus configuration value is 10000.

-   With older 32-bit PSS®ODMS versions, configuration is limited to
    50000 buses.

-   With the current 64-bit PSS®ODMS version, configuration is limited
    only by the available hardware capacity.

-   Dimensioning for most other data types is automatically scaled based
    on the Bus value.

-   Saved cases may be loaded with a smaller configuration than was used
    to build them. However, it is recommended that the same
    configuration (at minimum) is used to avoid potential loading case
    failure due to size limit change.

-   Be aware of physical resource constraints. If there is insufficient
    RAM, PSS®ODMS may become unstable. You can check the amount of
    in-use RAM with Windows Resource Monitor after building or loading a
    case in PSS®ODMS.
