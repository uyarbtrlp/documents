# Workflow

## Introduction

PSS®ODMS includes a variety of features and functions to import, export
and maintain network model and graphical data over time and run
simulation functions including Topology Analysis, Power Flow, State
Estimator and Contingency Analysis.

## Importing Network Data

PSS®ODMS provides functions to import network model data in CIM/XML and
PSS®E formats. Additional functions are provided to import measurement
data from ISN (standard ICCP) format and several easily-constructed CSV
formats into an existing model. Similarly, functions are provided to
automatically import (seasonal or temperature range-based) schedule and
ratings data from multiple PSS®E RAW files into a single model. Refer to
[???](#LinkTarget_3278) for more information on model management.

To import data from any format not supported by the standard import
functions, the CIMdbNET API can be used to extend PSS®ODMS by creating a
custom data importer.

## Building Diagrams

The OneLine editor is designed to \"auto-build\" complete and accurate,
fully-mapped and interactive diagrams exclusively from the underlying
network model topology. A diagram can be created for a single substation
or an entire area and the user can specify either bus-breaker or
(abstract) bus-branch format. The initial layout is intended to be
manually adjusted; when the diagram is saved to the database, all
customization are preserved. Diagrams serve multiple purposes: they
facilitate both interactive graphical model editing and analytical
results visualization. Refer to [???](#LinkTarget_3326) for more
information on the OneLine editor.

## Model Validation and Editing

The automated model import functions contain a certain level of
validation to ensure correct data formatting, CIM associations,
equipment connectivity, etc. However, this level of validation is not
enough to support power system analysis. The Build Case function
provides the next level of model validation. After a case has been built
successfully, a Power Flow solution is needed. Once this has been
achieved, the Power Flow results can be compared with other
applications. If the model was originally imported from PSS®E, it is
especially useful to export the case back to PSS®E RAW format for direct
comparison. When errors are found, they can be quickly corrected using
the model editing tools within PSS®ODMS. Refer to
[???](#chapter_m4q_jyf_xp) for more information on model editing.

## Exporting Network Data

PSS®ODMS provides functions to export network model data to CIM/XML and
PSS®E formats. Refer to [???](#chapter_mnk_syf_xp) for further
information.

To export data in any other format (such as proprietary EMS), the
CIMdbNET API can be used to extend PSS®ODMS by creating a custom data
extractor/exporter.

## Integrating Measurements

PSS®ODMS includes an OPC DA/UA client to retrieve real-time measurement
data from a customer-provided OPC DA/UA server. For ICCP integration, a
third-party OPC DA server (such as SISCO AX-S4) can be deployed.
Measurement mappings are stored in the database model and managed by
PSS®ODMS, so there is little configuration required to achieve
integration. PSS®ODMS can additionally be configured to publish
real-time network analysis results via the same mechanism.

## Network Analysis

The Network Analysis module provides a set of built-in analytical
functions (for both real-time and study simulation) similar to the
Advanced Network Applications of a traditional EMS. These functions
include Topology Analysis, Power Flow, State Estimator, and Contingency
Analysis. The primary means of results visualization is the same OneLine
interface used for model viewing/editing; diagrams are fully reusable
for interactive results visualization. Additionally, there is a set of
Excel-style spreadsheet views of the detailed network and measurement
data and results. Diagram and spreadsheet windows support bi-directional
navigation. Refer to [???](#LinkTarget_8732) for further related
information.
