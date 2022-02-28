# Importing Network Data

## Introduction

PSS®ODMS includes built-in functions to import network model and
measurement data from various file formats. This chapter describes how
to import data into a new PSS®ODMS database model, how to open and copy
existing PSS®ODMS database models, and how to import additional data
into an existing PSS®ODMS database model.

PSS®ODMS supports importing data in the following formats:

-   CIM/XML (Full, Partial and Incremental)

-   PSS®E RAW

-   Alstom/Areva

-   Siemens Spectrum 3

-   ISN measurements CSV

-   Analog measurements CSV

-   Switch measurements CSV

-   Equipment names

-   Generator types

-   Bus mapping CSV

Note: The time it takes for an import process to complete will vary
depending on the amount of data being imported in addition to other
factors such as database platform, hardware and networking
infrastructure.

## Importing a CIM/XML Model {#sect1_qjg_f3p_bq}

1.  First, make sure there is no database model already open in PSS®ODMS
    (as indicated by the title bar of the main window). If necessary,
    use the **File>Close Database** command to close the current
    database model.

2.  From the main menu, select ***Model>Import>CIM/XML***.

3.  In the resulting dialog, select the CIM/XML file and database
    information. PSS®ODMS will automatically detect the CIM version of
    the selected CIM/XML and display it accordingly. For some
    intermediate CIM versions which are not fully supported by PSS®ODMS
    (such as CIM13), there is an option to import the CIM/XML into a
    higher CIM version format.

    Note: When importing a CIM14 or higher version CIM/XML model, select
    either the \_EQ.xml file or a .zip file. If a \_EQ.xml file is
    selected, PSS®ODMS will optionally import the corresponding \_TP.xml
    and \_SV.xml files located in the same directory.

4.  Enter a name and (optional) description for the new model.

    IMPORTANT: Be aware of the name formatting restrictions of your
    database platform. As a general rule, model names should not include
    spaces or any special characters other than '\_' (underscore) in the
    model name.

    Note: Each PSS®ODMS database model has a unique name; if you enter
    the name of an existing model, PSS®ODMS will prompt you to replace
    it.

5.  Click the Finish button to dismiss the dialog and initiate the
    import function. After a successful import, PSS®ODMS will
    automatically open the new model. If the import fails (indicated by
    an error message), the corresponding log files should be reviewed
    and the selected CIM/XML file(s) checked for correctness.

![Import CIM/XML
Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_18.png)

## Importing a PSS^®^E Model {#sect1_akg_f3p_bq}

1.  First, make sure there is no database model already open in PSS®ODMS
    (as indicated by the title bar of the main window). If necessary,
    use the ***File>Close Database*** command to close the current
    database model.

2.  From the main menu, select ***Model>Import>PSS®E Model***.

3.  In the resulting dialog, select the PSS®E RAW file and database
    information.

    Note: PSS®ODMS will automatically detect and select the correct
    version number for any RAW file containing this information in its
    header.

4.  Select a CIM version for the new model.

5.  Enter a name and (optional) description for the new model.

    IMPORTANT: Be aware of the name formatting restrictions of your
    database platform. As a general rule, do not include spaces or any
    special characters other than '\_' (underscore) in the model name.

    Note: Each PSS®ODMS database model has a unique name; if you enter
    the name of an existing model, PSS®ODMS will prompt you to replace
    it.

    ![Import PSS®E Model Dialog (1st
    page)](/images/PSSODMS_UserManual_2014-10-17114243_img_19.png)

6.  Use the Next button to navigate to the second page of the Import
    PSS®E Model dialog, which contains more advanced options.

7.  Enable the following advanced options as needed:

    -   The naming convention specified by the ENTSO-E CIM profile may
        be enforced by the import function (refer to the profile
        document for details)

    -   PSS®E Areas may be mapped to Geographical Regions and Zones to
        Sub Geographical Regions (the default behavior maps Areas to Sub
        Geographical Regions)

    -   If the above option is disabled, then a default Geographical
        Region name can be specified for the single default Geographical
        Region instance created by the import function

    -   PSS®E Buses may be pre-grouped into Substations by the import
        function according the first n characters of each bus name (e.g.
        if the number of comparison characters is set to 3, then Buses
        \"MID230\", \"MID-EXT\" and \"MID500\" would all be pre-grouped
        into a substation \"MID\")

    -   Symmetrical phase shifters may be created as European-style
        phase shifters (the default is standard US-style)

8.  Click the Finish button to dismiss the dialog and initiate the
    import function. After a successful import, PSS®ODMS will
    automatically open the new model. If the import fails (indicated by
    an error message), the corresponding log files should be reviewed
    and the selected RAW data file checked for correctness.

![Import PSS®E Model Dialog (2nd
page)](/images/PSSODMS_UserManual_2014-10-17114243_img_20.png)

Note: In general, PSS®ODMS should be able to import any RAW data file
which PSS®E is able to load without errors.

## Opening a Model {#LinkTarget_3315}

Any model which has been successfully imported into the PSS®ODMS
database may be opened to perform editing or other operations. The
following steps describe how to open an existing model.

1.  From the main menu, select **File>Open Database** command.

2.  Select the appropriate database type from the drop-down list. Select
    the server name from the drop-down list, or if necessary, type in
    the server name.

    ![Open Database Dialog](/images/C2_Open_Database_Dialog.PNG)

3.  Select a model from the Model Name drop-down list (the list should
    contain all the existing PSS®ODMS models in the selected database
    server).

4.  If the \"Default Password to Model Name\" option is unchecked, enter
    the model password in the Password field (when a model is created,
    the password is initially defaulted to the model name).

5.  Click **OK** to dismiss the dialog and open the model.

Note: Most PSS®ODMS functions require an open database model.

## Copying a Model {#sect1_kkg_f3p_bq}

It is often useful to create a duplicate copy of an entire model within
the database. The following steps describe how to do this.

1.  Open the model you want to copy (see [Opening a
    Model](#LinkTarget_3315)).

2.  From the main menu, select the **Model>Operations>Copy Model**
    command.

3.  On the resulting Copy Model dialog, enter a unique name for the
    copied model and click **OK** button to dismiss the dialog.

    ![Copy Model
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_22.png)

4.  If the \"Open copied model\" option is checked, PSS®ODMS will
    automatically open the copied model after the copy process
    completes.

    ![Copy Model
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_23.png)

## Importing Data Into an Existing Model {#sect1_lkg_f3p_bq}

Especially during the initial model setup phase of a project, it may be
necessary to import additional data such as measurement and bus mapping
data into an existing model. The following steps describe how to do
this.

1.  Open the model (see [Opening a Model](#LinkTarget_3315)).

2.  From the main menu, select **Model>Import** command and choose the
    appropriate submenu command (only commands that import data into an
    existing model will be enabled).

    ![Import
    commands](/images/PSSODMS_UserManual_2014-10-17114243_img_24.png)

3.  Depending on the specific import command chosen, PSS®ODMS will
    present a dialog for selecting the file(s) to import into the model.

+-------------------+---------------------------------------------------+
| Menu              | Command                                           |
+===================+===================================================+
| CIM/XML Model     | Imports CIM/XML model (If no model is open in     |
|                   | PSS®ODMS, imports as a new model. If a model is   |
|                   | opened in PSS®ODMS, imports to the opened model   |
+-------------------+---------------------------------------------------+
| Incremental       | Imports incremental CIM/XML to the model          |
| CIM/XML           |                                                   |
+-------------------+---------------------------------------------------+
| PSS®E Sequence    | Adds PSS®E sequence data (.SEQ) to the model.     |
| Data              | Clears existing sequence data and import the      |
|                   | sequence data from PSS®E sequence data file       |
|                   | (.SEQ)                                            |
+-------------------+---------------------------------------------------+
| PSS®E Schedule    | Imports schedule data from PSS®E Raw data file    |
| Data              | (.RAW) into a specified season                    |
+-------------------+---------------------------------------------------+
| PSS®E Limit Set   | Imports limit set from PSS®E RAW data file (.RAW) |
|                   | into a specified season                           |
+-------------------+---------------------------------------------------+
| PSS®E Project     | Imports project data file (.PRJ). Project data    |
|                   | file can be created by comparing 2 sets of PSS®E  |
|                   | files by menu command **Model \>Operation         |
|                   | \>Compare PSS®E Models**                          |
+-------------------+---------------------------------------------------+
| PSS®E Dynamics    | Imports PSS®E Dynamics File (.DYR) into the model |
| Data              |                                                   |
+-------------------+---------------------------------------------------+
| PSS®E GCAP Data   | Imports PSS®E GCAP Data Files (.GCP) into the     |
|                   | model                                             |
+-------------------+---------------------------------------------------+
| Analog            | Imports Analog Measurements file (.CSV) to the    |
| Measurements      | model. (see [Importing Analog Measurements        |
|                   | ](#LinkTarget_5318))                              |
+-------------------+---------------------------------------------------+
| Switch            | Imports Switch Measurements file (.CSV) to the    |
| Measurements      | model. see [Importing Switch                      |
|                   | Measurements](#LinkTarget_5319))                  |
+-------------------+---------------------------------------------------+
| Bus Mapping Table | Imports Bus Mapping Table file (.CSV) into the    |
|                   | model.                                            |
|                   |                                                   |
|                   | Note: Bus Mapping Table file could be exported    |
|                   | from the model (by Menu **Model>Export>Bus        |
|                   | Mapping Table**).The exported file could be used  |
|                   | as a template for creating new Bus Mapping Table  |
|                   | file                                              |
+-------------------+---------------------------------------------------+
| Equipment Names   | Imports Equipment Names file (.NAM) into the      |
|                   | model.                                            |
|                   |                                                   |
|                   | Note: Equipment Names file could be exported from |
|                   | the model (by Menu **Model>Export>Equipment       |
|                   | Names**).The exported file could be used as a     |
|                   | template for creating new Equipment Names file    |
+-------------------+---------------------------------------------------+
| Generator Types   | Imports Generator Types file (.CSV) into the      |
|                   | model.                                            |
|                   |                                                   |
|                   | Note: Generator Types file could be exported from |
|                   | the model (by Menu **Model>Export>Generator       |
|                   | Types**). The exported file could be used as a    |
|                   | template for creating new Generator Types file    |
+-------------------+---------------------------------------------------+

### Importing Analog Measurements {#LinkTarget_5318}

#### Analog Measurement Data

Analog measurements could be imported to the model from a CSV format. An
example analog measurement CSV file is provided in sample folder (in
PSS®ODMS installed directory\\SampleData\\AnalogMeasurementSample.CSV).
This sample file can be imported in model created from savnw33.raw file.
The analog measurement CSV file can be imported by Menu
**Model>Import>Analog Measurements**. It will add Analog measurements
(Analog and Analog Value) to the equipment specified in the analog
measurement CSV file.

After importing the analog measurement CSV file, a log file
(ImportAnalogMeasurements.log) is generated in the log directory. Any
measurements that could not be imported into the model would be listed
in the log file.

Descriptions of the data in the analog measurement CSV file are as
follows.

**Measurement:** Name of the measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** Not required for PSSE identifier based import.

**Subscription ID:** Subscription ID of the measurement.

**Source:** Measurement Value Source of the measurement (ICCP, PI, PI
Historian, etc.).

**Device Type:** Device Type of the device associated with the
measurement.

-   Section: Voltage measurements

-   Line: MW and MVAR measurements of lines

-   Transformer: MW, MVAR and Tap measurements of transformers

-   Load: MW, MVAR measurements of Loads

-   Bank: MW, MVAR measurements of Banks/Shunts

-   Unit: MW, MVAR measurements of Units

**Units:** Units specifies the units of the measurements.

-   KV: voltage measurements

-   MW: Real power (MW) measurements

-   MVAR: Reactive power (MVAR) measurements

-   Tap: Tap position measurements

**Bus Number:** Bus number of the terminal in which the measurement
should be imported.

**From Number:** From bus number of the device corresponding to the
measurement. From Number is not required for voltage measurements
(Section).

**To Number:** To bus number of the device corresponding to the
measurement.(only needed for 2 or 3 terminal devices)

**K Bus Number:** Tertiary (K) bus number of the device corresponding to
the measurement. (only needed for 3 terminal devices)

**PSSE ID:** PSSE ID of the device corresponding to the measurement.
PSSEID is not required for voltage measurements (Section).

**Telemetry Code:** Telemetry Code of the measurement (optional).

1.  Default (receive the measurement from the measurement server in the
    Real Time mode)

2.  Telemetered (receive the measurement from the measurement server in
    the Real Time mode)

3.  Manual (Manually set measurement in the Real Time mode, overrides
    the measurement from the measurement server)

4.  Schedule

5.  Simulated

6.  Force Use

**Control Code:** Control Code of the measurement (optional).

-   0 - Accept

-   1 - Reverse (Reverse Flag: Set the measurement value to reverse.)

-   2 - Ignore (Ignore Flag: Ignore the measurement in Real Time mode.
    Measurement status will be changed to IGNOR/USER).

**Variance:** Variance of the measurement (optional).

**Limit:** Limit of measurement (optional).

**Measured value:** Numerical measured value (optional).

Note: Telemetry Code, Control Code, Variance and Limit are State
Estimator parameters which can be set during State Estimator Tuning (see
[???](#LinkTarget_3388))

An example of the analog measurement CSV file is given below. This
analog measurement CSV file can be imported by Menu
**Model>Import>Analog Measurements.**

  -----------------------------------------------------------------------------------
  Measurement   ODMS ID Subscription   Source   Device    Units   Bus       From Bus
                        ID                      Type              Number    Number
  ------------- ------- -------------- -------- --------- ------- --------- ---------
  Meas 500 Bus          1111K          ICCP     Section   KV      152       152

  -----------------------------------------------------------------------------------

  --------------------------------------------------------------------------------
  To Bus   K Bus    PSSE ID Telemetry   Control   Measured   Variance(%)   Limit
  Number   Number           Code        Code      Value                    
  -------- -------- ------- ----------- --------- ---------- ------------- -------
                            1           0         0          5             500

  --------------------------------------------------------------------------------

Importing this CSV file into a model will create a KV measurement in the
bus bar section corresponding to bus number 152

![Analog created after importing the analog measurement CSV file.
Telemetry Code, Control Code, Manual Value, Limit and Variance are
imported according to the values provided in the analog measurement CSV
file.](/images/analog measurement_fig 1.png)

![AnalogValue created after importing the analog measurement CSV file.
Measurement Value Source is set to Source data from the analog
measurement CSV file. Alias Name is set to the Subscription ID specified
in the analog measurement CSV
file.](/images/analog measurement_fig 2.png)

#### Importing Voltage Measurements based on Bus Bar Section ODMS ID

Voltage measurement import based on bus number is useful if the model is
only bus branch model (for example, after importing a PSSE raw file into
the model and before building node breaker detail). If the model has
node breaker detail and if there are multiple bus bar sections that have
same bus number, the analog import based on bus number will create
voltage measurement in each bus bar section. In order to import voltage
measurement to a particular bus bar section, ODMS ID of the bus bar
section could be specified.

Following fields should be specified in the analog measurement CSV file
for voltage measurement import based on bus bar section ODMS ID.

**Measurement:** Name of the measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** ODMS ID of the bus bar section.

**Subscription ID:** Subscription ID of the measurement.

**Source:** Measurement Value Source of the measurement (ICCP, PI, PI
Historian, etc.).

**Device Type:** Device Type should be Section.

**Units:** Units should be KV.

**Bus Number:** If ODMS ID of the bus bar section is specified, Bus
Number is only for information. The measurement will be imported to the
Bus Bar section with the specified ODMS ID. Bus Number will be imported
to Description field of the Analog.

An example of the analog measurement CSV file is given below. This CSV
file can be imported by Menu **Model>Import>Analog Measurements.**

.

  -----------------------------------------------------------------------------------
  Measurement   ODMS ID Subscription   Source   Device    Units   Bus       From Bus
                        ID                      Type              Number    Number
  ------------- ------- -------------- -------- --------- ------- --------- ---------
  DownTown west 43      1111m          ICCP     Section   KV      154       
  230                                                                       

  -----------------------------------------------------------------------------------

  --------------------------------------------------------------------------------
  To Bus   K Bus    PSSE ID Telemetry   Control   Measured   Variance(%)   Limit
  Number   Number           Code        Code      Value                    
  -------- -------- ------- ----------- --------- ---------- ------------- -------
                            1           0         0          5             230

  --------------------------------------------------------------------------------

Importing this CSV file into a model will create a voltage measurement
in the bus bar section with ODMS ID 43.

![Analog measurement created in bus bar section with ODMS ID
43](/images/voltage measurement_fig 1.png)

![Voltage measurement created in bus bar section DWNTN_West. Since ODMS
ID is specified, Voltage measurement is created in this particular bus
bar. Voltage measurement is not created for another bus bar, DWNTN_East
which also have the same bus
number.](/images/voltage measurement_fig 2.png)

#### Importing Bank Measurements

Switch shunts in PSS®E could have multiple bank sections. These bank
sections are imported into PSS®ODMS as multiple shunt compensators.
These multiple shunt compensators cannot be identified with PSS®E
identifiers. The flow measurements (MW or MVAR) for such shunts could be
imported by specifying ODMS ID of the shunt.

Following fields should be specified in the analog measurement CSV file
for bank measurement import based on shunt compensator ODMS ID.

**Measurement:** Name of the measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** ODMS ID of the bank section.

**Subscription ID:** Subscription ID of the measurement

**Source:** Measurement Value Source of the measurement (ICCP, PI, PI
Historian, etc.).

**Device Type:** Device Type should be Bank.

**Units:** Units should be MW or MVAR.

**Bus Number:** If ODMS ID of the Bank is specified, Bus Number is only
for information. The measurement will be imported to the Bank with the
ODMS ID specified. Bus Number will be imported to Description field of
the Analog.

An Example of analog measurement CSV file is given below. This CSV file
can be imported by Menu **Model>Import>Analog Measurements.**

  -----------------------------------------------------------------------------------
  Measurement   ODMS ID Subscription   Source   Device    Units   Bus       From Bus
                        ID                      Type              Number    Number
  ------------- ------- -------------- -------- --------- ------- --------- ---------
  Meas NUC      408     1111j          ICCP     bank      MVAR    151       
  plant1 mvar                                                               

  -----------------------------------------------------------------------------------

  --------------------------------------------------------------------------------
  To Bus   K Bus    PSSE ID Telemetry   Control   Measured   Variance(%)   Limit
  Number   Number           Code        Code      Value                    
  -------- -------- ------- ----------- --------- ---------- ------------- -------
                            1           0         0          30            1000

  --------------------------------------------------------------------------------

Importing this CSV file into a model will create a reactive power
measurement at linear shunt compensator with ODMS ID 408.

![Analog measurement created in linear shunt compensator bank with ODMS
ID 408](/images/bank measurement_fig 1.png)

![MVAR measurement created in linear shunt compensation NUCPLANT
1.](/images/Bank measurement_fig 2.png)

#### Updating Subscription IDs

Subscription IDs of measurements could change in the SCADA system due to
regular updates of the SCADA system. Subscription IDs of the existing
measurements in the model should also be updated according to changes in
the SCADA system. Subscription ID could be changed manually in CIMedit
by changing the AnalogValue Alias Name. In case of large number of
changes, subscription ID of existing analog measurements could be
updated by importing analog measurement CSV file.

Following fields should be specified in the analog measurement CSV file
for updating subscription ID of existing measurements.

**Measurement:** Name of the measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** ODMS ID of the Analog Measurement.

**Subscription ID:** new updated Subscription ID of the measurement.

**Source:** Measurement Value Source should be same as the Measurement
Value Source of the existing measurement.

Note: ODMS ID of the Analog Measurement and Source could be obtained
from **Measurement sheet>Analog Tab**.

An example of analog measurement CSV file for updating subscription ID
is given below. This CSV file can be imported by Menu
**Model>Import>Analog Measurements**.

  -----------------------------------------------------------------------------------
  Measurement   ODMS ID Subscription   Source   Device    Units   Bus       From Bus
                        ID                      Type              Number    Number
  ------------- ------- -------------- -------- --------- ------- --------- ---------
  Meas NUC      912     New_ID         ICCP                                 
  plant1 mvar                                                               

  -----------------------------------------------------------------------------------

  --------------------------------------------------------------------------------
  To Bus   K Bus    PSSE ID Telemetry   Control   Measured   Variance(%)   Limit
  Number   Number           Code        Code      Value                    
  -------- -------- ------- ----------- --------- ---------- ------------- -------
                                                                            

  --------------------------------------------------------------------------------

Importing this CSV file into a model will change the subscription ID of
measurement with ODMS ID 912 to New_ID.

### Importing Switch Measurements {#LinkTarget_5319}

#### Switch Measurement Data

Switch measurements could be imported to the model from a switch
measurement CSV format. An example of switch measurement CSV file is
provided in sample folder (in PSS®ODMS installed
directory\\SampleData\\SwitchMeasurementSample.CSV). The ODMS IDs of the
switches in the switch measurement CSV file need to be updated according
to the ODMS ID of the switches in the model before importing the file.
The switch measurement CSV file can be imported by Menu **Model>Import>
Switch Measurements**. It will add switch measurements (Discrete and
Discrete Value) to the switches specified in the switch measurement CSV
file.

After importing the switch measurement CSV file, a log file
(ImportSwitchMeasurements.log) is generated in the log directory. Any
switch measurements that could not be imported into the model would be
listed in the log file.

  --------------------------------------------------------------------------
  Substation     Switch name    ODMS ID        Subscription   Source
                                               ID             
  -------------- -------------- -------------- -------------- --------------
  DOWNTN         Breaker 101    906            PI_01          PI

  --------------------------------------------------------------------------

Description of Data in switch measurement CSV Files is as follows,

**Substation:** Substation Name (for information only).

**Switch name:** Name of the switch measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** ODMS ID of the switch. (Note: List of ODMS ID of the
switches in the model could be conveniently obtained by building the
case and opening the Network Sheet-Switches tab.)

**Subscription ID:** Subscription ID of the switch measurement.

**Source:** Measurement Value Source of the switch measurement (ICCP,
PI, PI Historian, etc.).

#### Updating Subscription IDs

Similar to analog measurements, subscription IDs of existing switch
measurements could be updated importing switch measurement CSV file.

Following fields should be specified in the switch measurement CSV file
for updating subscription ID of existing switch measurements.

**Substation:** Substation Name (for information only).

**Switch name:** Name of the switch measurement. A description name is
preferred as this measurement name will also be displayed in the
Measurement sheet.

**ODMS ID:** ODMS ID of the Switch.

**Subscription ID:** new updated Subscription ID of the Switch
measurement.

**Source:** Measurement Value Source should be same as the Measurement
Value Source of the existing measurement.

Note: ODMS ID of the Switch and Source could be obtained from
Measurement sheet Switch Tab. In the Switch Measurement sheet, Device ID
column is the ODMS ID of the Switch, which should be used in the CSV
file. ODMS ID column is the ODMS ID of the switch measurement which
should not be used in the switch measurement CSV file.

An example of the switch measurement CSV file for updating subscription
ID is given below. This CSV file can be imported by Menu
**Model>Import>Switch Measurements**.

  --------------------------------------------------------------------------
  Substation     Switch name    ODMS ID        Subscription   Source
                                               ID             
  -------------- -------------- -------------- -------------- --------------
  DOWNTN         Breaker 101    906            New_ID         PI

  --------------------------------------------------------------------------

Importing this CSV file into a model will change the subscription ID of
the existing switch measurement of the switch with ODMS ID 906 to
New_ID.
