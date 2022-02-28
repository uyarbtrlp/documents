# Introduction

## Document Overview

This document describes the functionality of the PSS®ODMS product from
an end user perspective. Some content is additionally relevant for
system administrators. Other product documentation such as the PSS®ODMS
Installation Guide and detailed API reference documents can be found in
the installed ODMS\\Documentation directory and are linked from the
Windows Start menu.

Availability of certain features is controlled by software licensing and
is dependent on the specific modules purchased.

## Background

### About Siemens PTI

Siemens Industry, Inc., Power Technologies International (Siemens PTI)
is a world leader in providing software solutions, consulting services
and professional education for the electrical power industry. Among its
software product offerings include the widely used PSS®E for
transmission planning analysis.

### About PSS®ODMS

PSS®ODMS is a Siemens PTI commercial software product for electrical
power transmission system modeling and analysis. It is used by companies
around the world to convert, manage and exchange network model data,
monitor the transmission grid in real-time and produce short-term and
long-term study cases. PSS®ODMS is also used to train system operators,
augment SCADA/EMS, and facilitate regulatory compliance by exchanging
data compliant with the IEC CIM 61970 standard and NERC CPSM and ENTSO-E
profiles.

PSS®ODMS allows system engineers and operators to maintain, analyze and
exchange network data quickly and easily and includes built-in functions
for importing and exporting data in PSS®E and CIM/XML format.

## Product Overview

PSS®ODMS is one of the first viable commercial products built on the IEC
Common Information Model (CIM) standard. PSS®ODMS stores network data in
a CIM-based relational database which can be deployed on either
Microsoft SQL Server or Oracle. With the ability to model and analyze
transmission networks down to the node-breaker level of detail, combined
with historical change tracking and project modeling features, PSS®ODMS
supports maintenance of a unified transmission Planning-and-Operations
network model.

A PSS®ODMS solution optionally includes an OPC DA/UA client interface
(OPCsync) to provide \"plug-and-play\" integration of real-time and/or
historical measurement data. With its built-in State Estimator, Power
Flow and Contingency Analysis functions, and dynamic graphical user
interface, PSS®ODMS can be easily deployed as either a primary or
supplementary Advanced Network Applications and Operator Training
Simulation tool. With solved snapshot cases from PSS®ODMS automatically
exported in PSS®E format (with consistent identifiers), this type of
deployment also provides seamless Operations-to-Planning data exchange.

The PSS®ODMS database schema can be extended to include custom
user-defined fields. The product also includes comprehensive Python and
.NET APIs which allow clients to create their own user interface
extensions and/or integrate PSS®ODMS with other systems, such as asset
management, EMS, GIS, etc.

### Features

PSS®ODMS contains many features that provide the capabilities described
in the PSS®ODMS Overview section above. These features include the
following:

-   Automated network model import from PSS®E, CIM/XML and various
    EMS-specific \"flat file\" formats

-   Model Merge automatically merges two models together with tie line
    resolution (re-connection) the only manual aspect of the procedure

-   Automated network model export to PSS®E and CIM/XML formats

-   Automatic one-line diagram generation from the network model

-   Graphical support for creating, deleting and reconnecting equipment
    and modifying attributes including Copy/Paste equipment

-   Complete mapping of PSS®E identifying information such as bus
    numbers, names, areas, owners and zones

-   Project Modeling supports unlimited multi-phase projects and
    interchangeable alternative future network scenarios

-   Integrated Topology and Power Flow for model validation

-   Integrated State Estimator and Contingency Analysis functions for
    advanced real-time and study simulation

-   Powerful graphical results visualization capabilities including flow
    arrow animation and color contouring

### Benefits

-   Improved grid model accuracy and quality for long-term and
    short-term planning studies

-   Avoidance of regulatory compliance violations/fines

-   Increased collaboration and coordination between transmission
    planning and operations departments

-   Improved grid security, reliability and situational awareness

-   Reduced network disruptions and outage recovery time

-   Faster and more effective personnel development/training

-   Increased engineering productivity

-   Faster completion of grid studies and planning projects

-   Increased business process efficiency

-   Facilitates interoperability and information exchange between and
    within power transmission organizations

-   Provides the network analysis functionality of a traditional EMS at
    a fraction of the cost

### System Requirements

The PSS®ODMS application must be installed on a Windows PC workstation,
laptop or server. For a multi-user (enterprise deployment), a network
connection to an Oracle or SQL Server database is required (with Oracle,
the database server can be any Oracle-supported platform, including
Windows, UNIX or LINUX). For single-user and/or off-network use, SQL
Server Express Edition can be installed locally.

Please refer to the PSS®ODMS Installation Guide for a detailed list of
system requirements.

### Software Installation

PSS®ODMS and its related utilities are installed by using the
Siemens-PTI provided installation programs and registered via file-based
software licensing.

Please refer to the PSS®ODMS Installation Guide for detailed
installation and registration instructions.
