# Network Analysis {#LinkTarget_8732}

## Introduction {#section_f1w_3zf_xp}

The Network Analysis module provides advanced functions for both on-line
and off-line operational network simulation and analysis, including
Topology Analysis, Power Flow, State Estimator, and Contingency
Analysis.

Note: Related commands can be found under the Analysis menu. The
corresponding Analysis toolbar provides 1-click access to many of the
most commonly used commands.

## Application Modes {#section_p1w_3zf_xp}

In a typical PSS®ODMS deployment, most companies have several distinct
user classifications or roles, such as the following.

1.  An Engineer who is responsible for maintaining the network model,
    one-line diagram displays and the integrity of the solution.

2.  An Operator who may execute network analysis functions, but does not
    make any editing changes to the network model or the one-line
    diagrams.

To separately organize related functionality, PSS®ODMS provides two
basic modes of operation. Depending on which mode is active, different
functions will be available to the user. The related menu commands can
be found under the Tools menu (with corresponding toolbar buttons for
convenience):

The Model Maintenance command enables the functions designed for editing
the network model and graphical data. This mode is enabled by default
when no case has been loaded into memory.

The Network Analysis command enables analysis-related functions. A case
must be loaded in memory for this command to be enabled. The model can
be viewed, but model editing functions are disabled and diagram editing
functions may be restricted or completely disabled.

![Tools Menu](/images/PSSODMS_UserManual_2014-10-17114243_img_117.png)

Note: Specific Model Maintenance functions can be further restricted by
configuring users with roles and assigned privileges. Refer to the
Application Administration section for details.

### Model Maintenance {#section_q1w_3zf_xp}

Model Maintenance mode provides access to model editing, graphical
editing, import/export and database management functions.

Note: Maintaining a separate \"production\" model exclusively for
on-line operation, while restricting model changes to a parallel
\"maintenance\" version of the model is a recommended business process.

Diagram displays are a significant component of the Network Analysis
user interface and can be easily customized to achieve a similar
appearance to that of the customer\'s SCADA/EMS displays. In Model
Maintenance mode, open diagrams reflect the database network model only.
In Network Analysis mode, open diagrams additionally reflect the
contents of the current case in memory.

### Network Analysis {#section_z1w_3zf_xp}

Network Analysis mode enables network analysis functions when a case is
in memory. When a case is not in memory, Network Analysis mode is
unavailable and PSS®ODMS reverts to Model Maintenance mode.

In Network Analysis mode, open diagrams are automatically updated to
reflect the contents of the case in memory (depending on the current
analysis activity), and will respond to user events to allow interaction
with the case.

Note: For convenience, some basic diagram editing changes may be
allowed, such as repositioning symbols and result labels. This allows
for adjusting diagram layouts needed, based on the measurement/result
labels displayed at any given time. Diagram editing functions can be
completely disabled via configurable user Roles/Privileges.

In addition to the Network spreadsheet, dialogs are provided to view and
edit the dynamic attributes of individual devices in the case. For
example, the user is able to change the P and Q values for a given load
or scheduled generation and voltage for a given generating unit.

Each breaker/switch symbol is displayed as open or closed based on its
actual status in the case. Additional visual cues are provided to
represent breakers with no telemetry, telemetry which is manually
overridden, and/or status inconsistent with its normal status. The
application provides various methods (such as double-clicking) to toggle
the status of a breaker from the one-line display.

Note: Visual cues include coloring, additional label text and/or
alternative symbol display options.

Whenever a new analytical solution is run, open diagrams are
automatically updated to display the current results for the current
Activity. Dynamic visual indicators include results labels,
color-coding, and direction-of-flow arrows.

Note: All diagram color-coding is user-configurable.

## Case Management {#section_abw_3zf_xp}

All Network Analysis functions operate against an in-memory case, a
dynamic representation of the underlying network model which may also
contain telemetered measurement values and solution results. It is
effectively a complete \"snapshot\" of the computer-simulated power
network at a given point in time. For study purposes, this snaphot may
be manually adjusted. Because the entire case resides in program memory,
the performance of computations and results display is the fastest that
can be achieved, which is critical in a real-time operations
environment.

Cases can be efficiently saved and reloaded in binary file format. A
case that has been saved to disk in binary file format (.sav) is
referred to as a \"saved case.\" As with any file, a saved case may be
copied, shared, renamed, archived, etc. at will. There is no limit
(other than hardware) to the number of saved cases that may be created
and used.

Note: Despite the fact that PSS®E also uses the .sav file extension for
its binary saved case file, the two file formats are not the same.

### Static vs. Dynamic Attributes {#section_bbw_3zf_xp}

It is important to distinguish between two different types of attributes
that comprise the case. Static attributes are considered part of the
underlying network model and are available to the user on a read-only
basis. The \"normal\" status of a switching device is an example of a
static attribute. Dynamic attributes are quantities that are expected to
change due to an operational event, either because of changing online
system conditions or through user changes commonly required for study
analysis. The \"actual\" status of a switching device is an example of a
dynamic quantity. Other dynamic quantities include scheduled load,
generation, voltages, tap positions, ratings, etc.

The ability to change the dynamic attributes of the case at will allows
the user to perform \"what-if\" studies, analyzing the results of
different conditions on the system.

Changes to static attributes, on the other hand, must be done through
the database model and the case rebuilt. This restriction is useful in
that it helps prevent critical inconsistencies between the database
model and the case.

### Building a Case {#section_jbw_3zf_xp}

Building a case requires an open database model in PSS®ODMS.

1.  Choose the **Analysis>Build Case** menu command to launch the Build
    Case wizard-style dialog. The wizard has 4 pages:

    -   Options (1) - contains grouped General, Measurements and
        Planning data options

        Areas may be modeled in PSS®ODMS as SubGeographicalRegions or
        Geographical-Regions; the \'Area mapping\' option should be set
        accordingly.

        The \'Switch status mapping\' options provide additional
        flexibility for establishing the initial topological
        configuration of the case. Historically, the \'Normal Open\'
        attribute has been most commonly used to store the default
        switch position/status.

        Device names in the case must be unique, so by default, the
        corresponding ODMS ID (integer value) will be appended to the
        Name string in the model to ensure uniqueness.

        There are various possibilities for managing PSS®E bus numbers
        and names in the model; the corresponding mapping options direct
        the case build function to collect this data from the specified
        locations. For example, bus numbers can be optionally retrieved
        from the \'Alternate Bus Number\' attributes of
        TopologicalNodes. Where bus mapping data does not exist in the
        model, default bus numbers and/or names will be assigned by the
        case build function.

        The \'Use BusNameMarker priority for merged buses option\'
        allows for predictability of bus identification in exported
        PSS®E cases for varying topological situations.

        The \'Initialize bus voltages from stored results\' allows for
        the possibility of a non flat-start Power Flow solution.

    -   Options (2) - contains Special case build options

        In most situations, the majority of these options should be
        disabled.

    -   Limits (3) -contains options related to flow limit and voltage
        limit sets

        By default, the first 9 available limit sets (including the
        reserved \<Default> limit set) in the model will be retrieved
        from the model and added to the case. The Analysis Options
        dialog provides a selection control to change the active limit
        set for the current case at any time.

    -   Network (4) - contains a network selection control for partial
        case building (for special situations). As indicated in the text
        on this page, the option to include the entire model is always
        set by default, so this page can be skipped in most situations.

2.  After selecting the options, click the Finish button from any of the
    three pages of the wizard to initiate the build case function.

3.  After the build case build function completes, a file selection
    dialog will prompt to save the case to a binary (.sav) file.

4.  The Analysis Output window will contain a log of the case building
    procedures, including specific warning or error messages. If the
    case was built successfully (no fatal errors), Network Analysis mode
    will be activated.

Note: It is important to review this log in detail, since this is often
where model errors are first detected.

![Build Case
Log](/images/PSSODMS_UserManual_2014-10-17114243_img_118.png)

Note: The log is also saved in a text file \"BuildCase.log\" in the
PSS®ODMS log directory.

### Building a Partial Network Case {#section_kbw_3zf_xp}

The Network page of the Build Case wizard dialog can be used to build a
case from a selected portion of the database model. In CIM16 models,
equivalencing during case build is determined by explicitly modeled
boundary injections represented by EquivalentInjection instances located
at boundary TopologicalNodes. The boundary injections for excluded
portions of the network will be represented as Loads in the resulting
case. In addition to the desired GeographicalRegions, it is also
necessary to select the artificial GeographicalRegion associated with
the official boundary ModelingAuthoritySet.

### Saving a Case {#section_lbw_3zf_xp}

Any time a case is open, it may be saved to a binary file for later
retrieval. To save the case, use either the ***Analysis>Save Case*** or
***Analysis>Save Case As*** command.

Note: Spaces are not allowed in saved case file names.

### Opening a Saved Case {#section_tbw_3zf_xp}

A saved case can be opened at virtually any time there is a model open
in PSS®ODMS. No more than one case may be in program memory at any given
time, so opening a saved case when a case is already open will simply
reload program memory from the selected file. To open a saved case, use
the ***Analysis>Open Case*** command and select the appropriate .sav
file in the file selection dialog.

When a case is saved in PSS®ODMS, the corresponding file name is stored
in a special table in the model, creating a loose association between
the database model and the saved case file name. Whenever a saved case
is opened, the application searches this table for the file name and
presents the user with a warning message if it is not found. Because of
this validation feature, expect to receive a warning message if you open
a saved case file after renaming it using Windows Explorer. Simply
re-save the case in PSS®ODMS to prevent repeated warning messages.

Note: If Model Maintenance is currently active at the time a case is
opened, PSS®ODMS will automatically switch to Network Analysis to enable
related functions.

### Recent Cases Menu {#section_ubw_3zf_xp}

Recently opened saved cases can be viewed and opened more conveniently
using the ***Analysis>Recent Cases*** menu.

### Reloading a Case {#section_vbw_3zf_xp}

In some situations, it may be desirable to \"undo\" a particular change
made to the case in memory. If the change has not yet been saved, use
the ***Analysis>Reload Case*** command to reset the case in memory from
the most recently opened saved case file on disk.

### Closing a Case {#section_wbw_3zf_xp}

Network Analysis memory may be cleared by using the ***Analysis>Close
Case*** command. PSS®ODMS will automatically revert to Model
Maintenance.

### Exporting a Case {#section_xbw_3zf_xp}

The current case may be exported to a PSS®E RAW file at any time (if the
current Topology solution is valid). To export the case to PSS®E, use
the ***Analysis>Export to PSS®E*** command. Be sure to select the
correct PSS®E version in the file save dialog.

Note: Exporting a case to PSS®E is nearly instantaneous and PSS®ODMS can
be configured to do this automatically after each real-time solution
process (using the Analysis Options dialog (Realtime Client page,
Advanced button).

## Network Analysis Functions {#section_ybw_3zf_xp}

In addition to Study and Realtime modes, there is a current Network
Analysis activity which affects things such as the results displayed on
open one-line displays. The activity has more impact in Study Mode than
in Realtime Mode. For example, in Study Mode, the behavior of the Solve
command is dependent on the current activity, whereas in Realtime Mode,
the Solve command forces execution of the entire Realtime solution
process.

### Topology Analysis {#section_xcw_3zf_xp}

The Topology Analysis activity allows the user to graphically view the
results of the Topology solution on the one-line displays. Different
color-coding options are provided to show active/inactive buses,
islands, out-of-service devices, etc. The default colors are arbitrary
but may be customized by the user; in general, bright colors are used
for \"active\" and dull colors are used for \"inactive\" portions of the
network.

The color settings for Topology Analysis activity can be configured from
the Display Settings dialog (**Analysis>Display Settings** menu
command).

1.  To view a portion of the network with the Topology results, open a
    diagram (***File>Open Diagram(s)*** menu command) with Topology
    Analysis set as the current activity.

    ![Graphical Topology
    Results](/images/PSSODMS_UserManual_2014-10-17114243_img_119.png)

2.  Text-based Topology results are displayed in the output window,
    including the total number of islands and which islands are active
    versus isolated.

3.  The contents of the Islands and Buses views on the Network
    spreadsheet are also derived from the Topology solution. These views
    will be empty whenever the current Topology solution is invalid.

    ![Islands
    View](/images/PSSODMS_UserManual_2014-10-17114243_img_120.png)

4.  To view islands in the network graphically, it is best to use a map
    board-style Worldview diagram with expanded substations.

### Power Flow {#section_ycw_3zf_xp}

The Power Flow activity allows the user to view the calculated voltages
and flows across the entire network, and is default activity for
Realtime Mode. In Power Flow activity, the one-line displays show bus
voltages and branch, generator, load and shunt flows. Various display
options are available, including color-coded results labels and animated
flow arrows.

1.  To configure the one-line display settings for Power Flow activity,
    use the **Analysis>Display Settings** menu command (or corresponding
    toolbar button) to launch the Display Settings dialog and activate
    the Power Flow page.

    The Display Settings dialog is modeless; the **Apply** button can be
    used to experiment with the different settings on open one-line
    diagrams without closing the dialog.

2.  To enable Power Flow activity, choose the ***Analysis>Activity>Power
    Flow*** command.

3.  To invoke a Power Flow solution, choose the ***Analysis>Solve***
    command. The solution convergence information is displayed in the
    Analysis Output window.

4.  The Alarms sheet is automatically updated after each Power Flow
    solution and can be configured to launch automatically.

    ![Alarms
    Sheet](/images/PSSODMS_UserManual_2014-10-17114243_img_122.png)

5.  Right-click on any record in the Alarms sheet and choose the Locate
    on Diagram context menu command to locate the corresponding device
    in the one-line display.

    ![Overloaded
    Transformer](/images/PSSODMS_UserManual_2014-10-17114243_img_123.png)

6.  The Power Flow solution results are summarized in the Network
    spreadsheet on various pages: System, Areas, Substations, Buses,
    etc.

    ![System Summary
    Results](/images/PSSODMS_UserManual_2014-10-17114243_img_124.png)

7.  The Power Flow solution options can be configured in the Analysis
    Options dialog.

#### DC Power Flow Option {#section_zcw_3zf_xp}

For greater flexibility in analyzing models for which a full AC power
flow solution normally would not converge, there is a DC power flow
solution option. DC power flow is an approximate power flow solution. It
is widely used in contingency analysis for contingency screening/ranking
(including the existing Outage Ranking function). It can also be used to
set the initial start point for a full AC power flow solution.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_125.png)

DC power flow is solved according to the following formula:

![](/images/PSSODMS_UserManual_2014-10-17114243_img_126.png)

The DC power flow solution provides the following results:

-   Calculated voltage phase angle of each bus section (voltage
    magnitude is defaulted to 1.0 p.u.)

-   Calculated MW flows on transmission lines

-   Calculated MW flows on transformers

-   Calculated swing bus generator MW

### State Estimator {#section_hdw_3zf_xp}

The State Estimator activity is designed primarily for SE tuning
purposes. It allows the user to view the preliminary SE results prior to
the realtime Power Flow solution. It also allows the user to execute the
State Estimator solution in Study Mode after changing various solution
parameters and/or measurement settings.

A solved Realtime Case requires a valid State Estimator and Power Flow
solution; the State Estimator activity shows intermediate results only
on the one-line displays.

In State Estimator activity, the one-line display can be configured to
show estimated values against measured values (with different text
colors). Manually-entered measurement values are distinguished from
telemetered values by a different color with an option to include an
alpha-numeric identifier following the measurement value (e.g., \"m\").
The display settings for the State Estimator activity can be configured
on the State Estimator page of the Display Settings dialog.

Practical use of the State Estimator requires measurement data
integration (refer to the Measurement Integration section); however, for
test/demonstration purposes, analog measurement values can be simulated
by the software:

1.  From the **Analysis>Measurements** menu, choose the Simulate
    Measured Values command.

2.  Choose the State Estimator command from the ***Analysis>Activity***
    menu to set the current activity to State Estimator.

3.  Activate Realtime Mode and choose the ***Analysis>Solve*** command
    to force execution of the Realtime Process. The State Estimator
    convergence information is displayed in the Output window.

4.  Open a diagram using the ***Diagram>Open Diagram(s)*** menu command.

    ![State Estimator
    Results](/images/PSSODMS_UserManual_2014-10-17114243_img_127.png)

5.  By default, measured values are colored white and estimated values
    are colored green.

6.  The State Estimator results are also available on the Measurements
    sheet (***Analysis>Spreadsheets>Measurements*** command).

7.  State Estimator solution options can be configured on the State
    Estimator page of the Analysis Options dialog.

    ![State Estimator Options](/images/SEoptionFull.png)

#### State Estimator tuning {#sect1_r1y_2hz_35}

1.  After building a new case, if the model does not contain schedule
    data used for external or other unobservable areas with respect to
    the State Estimator, you may need to tune the case to obtain a good
    converged power flow solution; then direct the State Estimator to
    use the results of the power flow solution as schedule data by
    selecting "Load Schedule Data" under the Analysis-Case Tool menu.
    Save the case to avoid having to repeat this step.

2.  Open the Measurements sheet. Verify that the Subscription ID strings
    have been properly initialized based on the enabled
    MeasurementValueSource (accessible from the
    **Model>CIMEdit>Enumeration window**). Enter Realtime Mode (using
    the **Analysis>Realtime Mode** menu command or toolbar button) and
    wait several seconds until all the measurements in the case have
    been subscribed and updated. Checking the Subscribed and Updated
    columns on the Analog and Switch views on the Measurements sheet is
    the best way to verify this. Then go back to Study Mode and save the
    case under a different file name (e.g. "snapshot.sav"). This will
    capture all the input required by the State Estimator.

    ![CIMedit Enumerations](/images/Enumerations.png)

3.  State Estimator tuning may be performed using all the available
    telemetry data at once, or by selectively restricting the visibility
    of the SE. To use the second approach, in the Analog Measurements
    view, first check the "Ignore" boxes for all analog measurements via
    multiple selection and Copy/Paste. Then, right-click on any cell and
    choose the "Filter" command from the context menu to launch the
    Filter dialog. Set the filtering criteria to Substation and select
    the substations to be tuned. Press the OK button to apply the
    filtering options. Uncheck the "Ignore" boxes for all records in the
    filtered view. The SE will ignore all analogs except for those with
    unchecked Ignore boxes. Right-click on the view and choose the "Save
    Configuration" context menu command to save the current view
    filtering options. Save the case to save the currently ignored
    measurements.

    ![Filtering measurements for desired substations](/images/Filter.png)

4.  Open the State Estimator page in Analysis Options dialog and uncheck
    "Enable realtime power flow solution in Study Mode" option
    (highlighted below) to prevent Power Flow from diverging during the
    tuning period before the correct SE solution has been obtained.

    ![State Estimator Options, uncheck "Enable realtime power flow
    solution in Study Mode" option to prevent Power Flow from
    diverging](/images/SEoption.png)

5.  Run State Estimator by selecting the SE Activity button and clicking
    the Solve button.

6.  Click the "State Estimator Tuning Sheet" button to open the SE
    Tuning sheet. The State Estimator Tuning sheet is automatically
    populated after each SE solution and consists of six different views
    that highlight different types of problems with the solution that
    may be caused by modeling errors, measurement inconsistencies, etc.

    ![Suspect Topology for State Estimator
    Tuning](/images/SETuningSheet.png)

    **Suspect Topology**

    Lists analog measurements whose values are inconsistent with the
    topology as determined by the current switching configuration.

    **Suspect Flow Direction**

    Lists flow measurements where the measured and estimated values have
    different signs, indicating a conflict in measured vs. estimated
    flow direction.

    **Branch Credibility Failures**

    Lists branch devices where a large difference exists between
    from-end analog and to-end analog values.

    **Bus Credibility Failures**

    Lists buses where the total bus injection is a large nonzero value.

    **Suspect Generation**

    Lists generating units where the computed MW values differ
    considerably from the schedule values. The user can direct the SE to
    ignore the mismatch via the Accept checkbox.

    **Suspect Load Distribution**

    Lists loads where the computed MW and/or MVAR values differ
    considerably from the schedule values. The user can direct the SE to
    ignore the mismatch via the Accept checkbox.

    **Hint**

    The State Estimator Tuning sheet offers the same navigational
    features as the other spreadsheet displays. For example, you can
    right-click on nearly any cell and Locate the corresponding element
    in the one-line diagram. This is often very useful in identifying
    the causes of problems identified by the SE Tuning sheet.

7.  Identify flow direction errors using the State Estimator Tuning
    sheet.

    During the tuning process, flow measurement direction errors are the
    most common real-time data errors and it is not easy to identify all
    of them. The State Estimator Tuning sheet allows you to quickly
    identify and correct them with the following procedure.

    -   The Branch Credibility Failures page can help identify flow
        direction errors for branches with flow measurements at both
        ends.

        Example: Double-click Total Mismatch column to sort the data in
        descending order to find the largest value of 35.75455 MW;
        right-click on the branch name cell and use the Locate on
        Diagram command to navigate to the one-line diagram which shows
        the direction error on the left side of the transformer.

        ![Example of Branch Credibility for State Estimator
        Tuning](/images/BranchCred.png)

    -   The Bus Credibility Failures page can be used to quickly
        identify flow direction errors for buses with flow measurements
        on all connected branches.

        Example: Double-click the Total Injection column to sort the
        data in descending order to find the largest bus injection of
        71.29 MW; right-click on the bus name cell and use the Locate on
        Diagram command to navigate to the one-line diagram which shows
        the transformer at the bottom having direction error.

        ![Example of Bus Credibility for State Estimator
        Tuning](/images/Bus Cred.png)

    -   For other situations where there is less observability, the
        Suspect Flow Direction page lists the measurements where the
        sign of the measured and estimated values are different.

        Example: Double-click the Difference column to sort the data in
        descending order to find the largest value of 481.113 MW;
        right-click on the measurement name cell and use the Locate on
        Diagram command to navigate to the one- line diagram which shows
        the transformer with conflicting measured and estimated values.
        This kind of direction error may or may not be directly
        associated with the transformer flow measurements itself; it may
        be also caused by other erroneous flow measurements. Further
        investigation is required.

        ![Example of Suspect Flow Direction for State Estimator
        Tuning](/images/suspect flow.png)

8.  Correct direction errors for all flow measurements.

    Use the Reverse checkbox to selectively reverse the sign of flow
    measurements that need to be reversed.

9.  Identify Topology errors.

    The Suspect Topology page lists analog measurements which have
    either zero measured value and nonzero estimated values (e.g. a
    switch measurement may have incorrect "closed" status), or nonzero
    measured values and zero estimated values (e.g. a switch measurement
    may have incorrect "opened" status). This indicates a possible
    topology error in the network.

    By locating the measurement in the diagram, it can be seen that a
    given unit has nonzero MW and MVAR measurements but the unit is also
    out of service (switch is opened). This represents a contradiction:
    either the analog or switch measurement must be wrong.

    ![Example of Suspect Topology for State Estimator
    Tuning](/images/suspect topo.png)

10. Store SE Tuning Parameters to the model.

    A saved case includes all the tuning parameters (such as Manual,
    Reverse, Force Use, Ignore, Variance and Limit). However, these
    parameters need to be stored in the database model so that a rebuilt
    case can be properly initialized. This can be done easily via the
    Store Tuning Parameters command.

#### Boundary error handling {#section_se_boundary_error}

In real-time mode, the telemetered area (typically internal) is dynamic
with continually changing measurements, whereas the non-telemetered area
(typically external) is static. As a result, flows tend to be mismatched
at the boundary between the telemetered and non-telemetered areas. It is
generally desirable to \"push\" mismatch errors to the external area for
more accurate internal area results. However, sometimes large mismatch
errors in the external area may cause post-SE power flow solution
divergence.

The \"Boundary error method\" option provides a choice of three
different methods to handle different situations. This option can be
found in the State Estimator page of the Analysis Options dialog.

1.  **Internal accuracy:** This method favors internal area results
    accuracy by pushing a greater amount of boundary error out of the
    internal/telemetered area.

2.  **Balanced approach:** This method pushes a lesser amount of
    boundary error out of the internal/telemetered area for a balanced
    trade-off between internal area results accuracy and stable solution
    convergence.

3.  **External stability:** This method pushes the least amount of
    boundary error out of the internal/telemetered area for the most
    stable solution convergence possible, sacrificing internal area
    results accuracy.

It is recommended to initially select the \"Internal accuracy\" method.
If the real-time solution is unstable, next select the \"Balanced
approach\" method. Finally, if the real-time solution is still unstable,
select the \"External stability\" method.

When using the \"External stability\" option, more telemetry near the
boundary area is needed to achieve accurate results; when using the
\"Internal accuracy\" option, less telemetry near the boundary area is
needed.

Note: this option is not designed to replace proper State Estimator
tuning, which is a general prerequisite for stable solution convergence
and accurate results.

### Outage Ranking {#section_idw_3zf_xp}

The Outage Ranking activity is designed for single-outage contingency
screening prior to executing a full Contingency Analysis solution. The
Outage Ranking solution is a \"fast and rough\" probability analysis of
single-outage contingencies for all selected devices in the system to
determine which outages are most likely to cause real violations and
should be further analyzed by the Contingency Analysis solution.

Before setting up or attempting to run an Outage Ranking solution, first
make sure you have a valid base case Power Flow solution.

Three different ranking methods are available: Flow Violation ranking,
Voltage Violation ranking, and Voltage Collapse ranking. Outage Ranking
results are separated accordingly for branches and (bus) sections. A
percentage tolerance can be set for each method to limit the results.
The problem domain is restricted by the Outage Criteria, which allows
for selecting voltage levels, areas, and device types to include in the
calculation. Flow Violation ranking results can be further refined by
creating the appropriate Branch Monitoring Group(s). Calculated branch
violations outside the selected group(s) are ignored.

For the Outage Ranking solution to work properly, the Outage Criteria
must be set and at least one Branch Monitoring Group must be Added and
Selected.

1.  To set up Outage Ranking, launch the Analysis Options dialog and
    activate the Outage Ranking page.

    ![Outage Ranking
    Options](/images/PSSODMS_UserManual_2014-10-17114243_img_129.png)

2.  Set the outage criteria for branches and units by clicking the
    Branches and Units buttons and selecting the appropriate items in
    the resulting dialogs.

    ![Branch Outage
    Criteria](/images/PSSODMS_UserManual_2014-10-17114243_img_130.png)

3.  On the Outage Ranking page, use the Add button to create a new
    Branch Monitoring Group; select the appropriate items on the
    resulting dialog and click **OK**. Use the '\--\>' arrow button to
    move the new group item from the Available box to the Selected box.

    Up to five Branch Monitoring Groups may be added and selected;
    however, in most situations, only one is needed.

    Branch Monitoring Groups could be stored in the database by clicking
    on Store button. Branch Monitoring Groups saved in the database
    could be loaded by clicking on Load button.

4.  Click OK to accept the Outage Ranking setup changes.

5.  With the current activity set to Outage Ranking, use the
    **Analysis>Solve** command to run the calculation.

6.  The Outage Ranking results are displayed in a spreadsheet window,
    with outaged devices ordered by violation.

    ![Outage Ranking
    Results](/images/PSSODMS_UserManual_2014-10-17114243_img_131.png)

If the corresponding Outage Ranking option is set, a new set of
single-outage (N-1) Contingencies will be generated and selected for the
Contingency Analysis solution.

### Contingency Analysis {#section_rdw_3zf_xp}

The Contingency Analysis activity is used to analyze the impact of
various single-outage or (typically more complicated) user-defined
contingencies on the system with respect to flow violations and/or
voltage violations.

As described in the Outage Ranking section above, a set of single-outage
contingency cases can be automatically generated and pre-selected by the
Outage Ranking solution. In this case, it is only necessary to set the
current activity to Contingency Analysis and choose the
**Analysis>Solve** command to invoke the solution. More extensive use of
the Contingency Analysis feature involves creating and running
user-defined contingency cases.

Before creating user-defined contingency cases or attempting to run a
Complex Contingency solution, first make sure you have a valid base case
Power Flow solution.

#### Creating a User-Defined Contingency {#section_b2w_3zf_xp}

Most of the information that comprises a user-defined contingency is
captured in a contingency script file which is created and maintained by
the user. The saved case itself contains a list of user-defined
contingency cases along with the unqualified name of the corresponding
script file for each. Contingency scripts are written in Python. The
program provides an automatic \"recording\" feature to allow a Python
script to be generated simply by interacting with the GUI (e.g. toggling
breakers). However, for more sophisticated contingency modeling
involving complex logic, looping, variable declaration, etc., a manually
edited Python script is needed.

Python is a full-featured, modern, platform-independent programming
language with many freely available tools and libraries. Siemens PTI's
pssoPy module is an extensive, object-oriented Python API specifically
designed for Network Analysis scripting.

The following steps can be executed to create a user-defined
contingency:

1.  Set the current activity to Contingency Analysis.

2.  Choose the **Analysis>Spreadsheets>Contingency Setup** menu command
    (or corresponding toolbar button) to launch the Contingency Setup
    spreadsheet window.

3.  Activate the User-defined page.

    ![User-Defined
    Contingencies](/images/PSSODMS_UserManual_2014-10-17114243_img_133.png)

4.  To begin, type the name of the new user-defined contingency in the
    bottom-most row Contingency cell, replacing the \"\[New\]\" text.

5.  Choose ***Analysis>Scripting>Record*** command (or corresponding
    toolbar button) to begin recording the contingency script file. The
    Script Editor window will appear.

6.  Using available GUI components (including the interactive one-line
    diagram), perform the operations that define the contingency. For
    example, you can isolate a line by opening its surrounding breakers
    and adjust loads and generating units. Observe the commands being
    recorded in the script file window.

7.  Choose ***Analysis>Command File>Stop Recording*** menu command (or
    corresponding toolbar button) and save the operation file when
    prompted, (keeping the default path and file name, for consistency).
    Observe the script file name in the user-defined contingency record.

8.  To ensure that the user-defined contingency is always selected for
    the Contingency Analysis solution, check the Select Always option.
    Alternately, one or more \"trigger\" devices may be associated with
    the user-defined contingency to define additional selection
    criteria. This will cause the contingency to be selected for the
    solution only when the in-service status of any of its trigger
    devices changes.

    ![Trigger Devices
    Page](/images/PSSODMS_UserManual_2014-10-17114243_img_134.png)

9.  Right-click on a device record in the Network sheet (or an equipment
    symbol on the one-line diagram) and choose the Add to Trigger
    Devices context menu command to add the device to the list of
    trigger devices associated with the user-defined contingency.
    Right-click on a device record in the Trigger Devices page and
    choose the Remove Trigger Device context menu command to remove the
    selected device from the list.

If you set the Select Always option for a user-defined contingency, it
is not necessary to specify trigger devices.

#### Solving Contingency Analysis {#section_c2w_3zf_xp}

When one or more contingencies are selected (and the base case Power
Flow solution is valid), the Contingency Analysis solution may be run.
The list of selected contingencies can be a combination of single-outage
contingencies automatically generated by the Outage Ranking function as
well as user-defined contingencies.

The following steps detail how to invoke the Contingency Analysis
solution:

1.  Set the current activity to Contingency Analysis.

2.  Optionally, verify the selected contingencies by opening the
    Contingency Setup spreadsheet.

    ![Selected
    Contingencies](/images/PSSODMS_UserManual_2014-10-17114243_img_135.png)

3.  The Contingency Analysis solution function is dependent on the Power
    Flow, Outage Ranking and Contingency Analysis options, as well as
    any scripts associated with user-defined contingencies.

    ![Contingency Analysis
    Options](/images/PSSODMS_UserManual_2014-10-17114243_img_136.png)

4.  Choose the ***Analysis>Solve*** menu command to invoke the solution.

5.  After the solution completes, the program will launch the
    Contingency Results spreadsheet, which contains case summaries and
    device summaries for the worst flows and voltages.

    ![Contingency
    Results](/images/PSSODMS_UserManual_2014-10-17114243_img_137.png)

6.  Use the View Results button to see the detailed results for any
    solved contingency listed in one of the summary views.

7.  As with other Network Analysis spreadsheets, right-click on any
    record and choose the Locate on Diagram context menu command to
    locate the selected device in a one-line display.

8.  At this point, any solved contingency may be individually
    \"activated\" to examine its impact on a system-wide basis. To
    activate a a solved contingency, click the Activate button for the
    corresponding record in the Contingency Summary view. The active
    contingency record is highlighted in yellow; the Alarms sheet,
    Network sheet and one-line displays are all updated to show the
    results of this particular contingency.

    ![Activated
    Contingency](/images/PSSODMS_UserManual_2014-10-17114243_img_138.png)

9.  To deactivate the contingency, click the Activate button again and
    the system will return to displaying \"base case\" conditions. Or,
    if the Contingency has an associated Protection Scheme, the
    Protection Scheme will be applied to the active Contingency.

In Contingency Analysis activity, the status bar and spreadsheet title
bars indicate whether a particular solved contingency (or
contingency-protection scheme combination) is active.

Contingency Analysis can be configured to run automatically in Realtime
Mode (via the Realtime Client page of the Analysis Options dialog). In
this situation, the results will vary depending on the current Realtime
Case (State Estimator and Power Flow solution). This can provide the
operator with early warnings on potentially dangerous situations that
may occur due to varying real-time conditions.

Activating a contingency represents a \"what if\" scenario.

#### Protection Schemes {#section_l2w_3zf_xp}

A protection scheme represents a specific set of corrective procedures
(which may be manual, automated or a combination of both) that is
initiated in response to one or more contingencies in order to protect
specific devices from flow or voltage violation. Using the simulation
capabilities, the effectiveness of such procedures can be assessed in
the context of changing realtime system conditions.

Protection schemes are created similar to user-defined contingencies,
using the Protection Scheme page of the Contingency Setup sheet. A
Python script is typically used to model a protection scheme (refer to
the Scripting section). This script may be a high-level \"master\"
program designed to invoke the appropriate protection scheme function
depending on specific system conditions. Monitored devices (used for
results reporting) for a given protection scheme are selected similarly
to the way trigger devices can be selected for a user-defined
contingency.

After creating one or more protection schemes, use the Protection Scheme
combo-box column in the User-defined Contingency view to associate a
protection scheme with a user-defined contingency. The same protection
scheme may be associated with multiple contingencies.

![Contingency-Protection Scheme
Association](/images/PSSODMS_UserManual_2014-10-17114243_img_139.png)

Contingency-referenced protection schemes are automatically included in
the Contingency Analysis solution and are shown in the Protection
Summary page of the Contingency Results sheet. In Study Mode, from
either the Protection Summary or Contingency Summary views, click the
Activate button once to activate a solved contingency. If the
contingency has an associated protection scheme, push the Activate
button a second time to apply the protection scheme to the contingency
and observe the combined impact on the system. Push the Activate button
a third time to revert back to the base case.

#### Storing and loading user defined contingency setup data

Saving a case which contains user defined contingencies and protection
schemes will save the contingency and protection information in the
case. The save case could be opened in PSS®ODMS and contingency analysis
could be run from the case, provided that the referenced contingency and
protection scripts are in the specified contingency directory. However,
building a new case from the model would not have the user defined
contingencies and protection scheme.

The user defined contingency and protection scheme information from a
case can be stored in the PSS®ODMS model database by using Menu
**Analysis>Case Tool>Store Contingency Data**. This will store the
contingency setup into the model.

The stored information can be loaded in a case by Menu **Analysis>Case
Tool>Load Contingency Data**.

## Study Mode {#section_n2w_3zf_xp}

Network Analysis has two main modes of operation: Study Mode and
Realtime Mode. Study Mode provides the user with a greater degree of
control over the editable case attributes and the individual functions
to allow for analysis of the system under different conditions. Study
Mode is effectively an \"off-line\" mode; the application does not
receive measurement updates in Study Mode. The case represents a
snapshot of the system in time.

Study Mode is the default mode of operation after initially opening a
saved case. The user can switch back and forth between Study Mode and
Realtime mode via the checkable menu commands under the Analysis menu.

Network Analysis functions are grouped into different activities, only
one of which may be current at a given time. The one-line displays may
be updated differently depending on the current activity. Also, in Study
Mode, the **Analysis>Solve** command will invoke the appropriate
solution function depending on the current Activity.

![Activity Menu](/images/PSSODMS_UserManual_2014-10-17114243_img_141.png)

In Network Analysis, the status bar at the bottom of the main window
indicates the current mode and activity.

## Realtime Mode {#section_v2w_3zf_xp}

In Realtime Mode, the application subscribes to measurement updates from
OPCsync as they become available and automatically executes a Realtime
Process on a timed basis. In a typical control center deployment, a
given PSS®ODMS workstation in Realtime Mode would be receiving
continuous measurement updates, executing a State Estimator and Realtime
Power Flow solution in a predefined time interval and displaying the
results to the user via interactive one-line diagram and tabular
displays.

Outage Ranking and Contingency Analysis could also be executed after the
Realtime Power Flow solution. Execution of the various solution
functions is determined by the Realtime options. The available solution
functions that can be configured to run during each Realtime Process
are:

-   State Estimator

-   Realtime Power Flow

-   Outage Ranking

-   Contingency Analysis

![Realtime option. Analysis functions to be executed in Realtime mode
can be set up in this tab.](/images/C10_AnalysisOptionRealtime.PNG)

In the Realtime model, the **Analysis>Solve** command becomes Force
Solution and when invoked, simply forces the Realtime Process to occur
immediately, independent of the timer and the current Activity. The
Analysis Activity commands are available in Realtime Mode (Menu command
***Analysis> Activity***); however, their overall impact is largely
limited to how diagrams are dynamically updated. For example, when the
activity is set to Power Flow, Power Flow results will be displayed in
diagrams and when the activity is set to State Estimator, State
Estimator results will be displayed in diagrams.

In most situations, the Power Flow Activity provides the most
informative and useful one-line

displays for the solved realtime case and should be the default Activity
for most users in Realtime Mode. Advanced graphical features such as
animated flow arrows and limit-based result coloring are only available
in this Activity.

Most of the operational state attributes that are editable in Study Mode
are non-editable in Realtime Mode, since the purpose of Realtime Mode is
to capture a snapshot of real- world system conditions. This limitation
is very slight however, since the user can easily toggle back and forth
between Real-time Mode and Study Mode with a single mouse click by using
the Realtime Mode button on the Analysis toolbar. Attributes related to
State Estimator such as measurement's Manual, Ignore, Reverse flags,
Variance and Limit can be edited in the Realtime Mode. If a
switch/analog measurement is set to Manual by checking the manual flag
of the measurement, the value of the measurement could also be edited in
the Realtime Mode (manual override of measurement value).

![Manual override of measurements. The measurement value can be
overridden manually by checking the Manual flag and setting the
Value.](/images/C10_Manual Measurement.png)

The Analysis Output window displays continuous information for each
Realtime Process and the results of the analysis activities contained
therein. Open diagram and spreadsheet windows (including Alarms) are
automatically updated after the completion of each Realtime Process.

The Analysis Options dialog (Realtime and OPCsync pages) offers a
variety of configurable settings which affect Realtime Mode behavior.

To connect to an OPCsync server, specify Server the name of the server
and click on the "Test Connection" button next to the server name. The
Status should change to "Connected to OPCsync" if the connection is
established.

![OPCsync options. To test the connection to the OPCSync server, click
on the "Connect" button.](/images/C10_AnalysisOptionOPCSync.PNG)

### Realtime Solution Process {#section_RT_sol_process}

The Realtime Solution Process consists of a number of sequential steps,
which include validating measurement updates from OPCsync and executing
the enabled network analysis functions. Taken together, these steps
preprocess the measurement data, compute the estimate of the new system
state, use the state estimate to obtain a current model of the power
system, and analyze the measurements set to detect and identify bad
telemetered values.

The individual steps which make up the Realtime Solution Process are as
follows:

#### Measurement update validation {#section_meas_update_validation}

Upon entering Realtime Mode, PSS®ODMS subscribes to OPCsync and begins
receiving analog, switch status and in-service status measurement value
updates. The Output window shows a continuous log of the measurement
updates (in configurable detail). If PSS®ODMS could not subscribe to
certain measurements, the list of measurements that have subscription
issues is also logged in the Output window.

At the beginning of each Realtime Solution Process, PSS®ODMS checks for
updated measurements and logs measurements that have not been updated
(stale measurements) to the Output window. A measurement is considered
stale if the measurement's timestamp has not been updated for a certain
time period. This time period threshold is set in the OPCsync options
("Indicate state analog measurements after x non-updated minutes").

By default, PSS®ODMS will only use analog measurements that have Quality
flag set to "Good". Measurements with other Quality flag will be set to
"IGNOR/TELE" and will be ignored by the State Estimator.

However, the user has ability to use measurements with Quality of
Uncertain or Last Known in the real time process by checking "Treat as
Good quality: Uncertain or Last Known" option in the OPCsync Options
window. It is recommended to troubleshoot the issue which is causing the
Quality flag to Uncertain or Last Known instead of treating them as
"Good" measurements.

Here is an example of the progress log which shows the measurement
updates.

``` c
Realtime Solution n started mm/dd/yyyy HH:MM:SS

Warning: # subscribed measurements have not been updated

# measurement values input to State Estimator

# measurements could not be subscribed
        
```

The number of measurements subscribed by PSS®ODMS is also indicated on
the status bar located in the bottom right corner of the application.

![Status bar indicating number of measurements subscribed by
PSS®ODMS.](/images/C10_number_measurement_status_bar.png)

#### Pre-State Estimation Analysis {#section_preSE_esitmation_analysis}

As initial preparation for further network analysis, PSS®ODMS updates
the status of the switches in the case based on the status measurement
values retrieved from OPCsync. A Topology solution is then invoked.

Next, the analog measurement values are checked against measurement
limits. Based on the limit checking, the measurement status (SE Status
in Measurement sheet) is set. The list of possible measurement statuses
is given below. Only measurements with status "IN_USE" are used by the
state estimator.

-   IN_USE - used by the State Estimator calculation

-   IGNOR/DATA - ignored by the State Estimator due to known bad quality

-   IGNOR/USER - ignored by the State Estimator due to explicit
    \'Ignore\' user setting

-   IGNOR/TELE - ignored by the State Estimator due to lack of data
    update

-   REJ/LIMIT - rejected by the State Estimator due to failed limit
    check

-   REJ/BAD - rejected by the State Estimator due to Bad Measurement
    Identification check

-   DEACTVATED - \"permanently\" ignored by the State Estimator due to
    multiple rejections (can be manually reactivated via context menu
    command in the Analog Measurements spreadsheet view)

If the user has the "Status Correction based on analog data" enabled,
PSS®ODMS auto corrects the status of switches based on the analog
measurements. The threshold of the analog measurement to determine the
status of the equipment is specified in "Status Correction" window (In
Analysis Options-State Estimator Tab, click on "Status Correction"
button to get the "Status Correction" window).

![Auto-correction based on analog data. (In Analysis Options-State
Estimator Tab, click on Status Correction button to get the Status
Correction Window).](/images/C10_StatusCorrection.png)

An example of status correction is shown in
[figure_title](#StatusCorrectionExample). The status of the generator
breaker is auto corrected base on the MW and MVar measurement of the
generator.

Note: the breaker Gen_Brk_HYD has Auto-correct set to "Yes". The
measured status of the breaker is "Closed". The current status of the
breaker is set to "Open" by the status correction algorithm as the
generator has 0 MW and 0 MVar (Analog measurements).

![Auto-Correct.Example: Status of the breaker Gen_Brk_HYD is corrected
(Open) based on the generator analog measurement (0 MW, 0
MVar).](/images/C10_Status_correction_example.png){#StatusCorrectionExample}

Next, PSS®ODMS initializes its internal generation and load schedule
based on the actual measurements or calculated values based on the
actual measurements. This includes voltage schedules and real/reactive
power schedules.

This is called the Pre-State Estimator case which has statuses and load
and generation profile based on the measurements. A Power Flow solution
is run on the pre-State Estimator case.

Here is an example of the progress log indicating pre-State Estimator
Topology Analysis and Power Flow results.

``` c
Solving State Estimator...

State Estimator solved

 Turning off area interchange in all areas

 Turning off LTC transformers in all areas

 Turning off switched shunts in all areas
                     TOTAL   TOTAL    TOTAL    GENERATION     TOTAL     SWING
 ISLAND    STATUS    BUSES   LOADS    LOAD       UNITS    GENERATION     BUS
 ------  --------   ------   ------  ---------  ---------  ----------  ------
     1    ACTIVE        23      10    2859.82       7        2904.71    MINE_G                          
                     TOTAL   TOTAL    TOTAL    GENERATION     TOTAL     SWING
 ISLAND    STATUS    BUSES   LOADS    LOAD       UNITS    GENERATION     BUS
 ------  --------   ------   ------  ---------  ---------  ----------  ------
     1    ACTIVE        23      10    2859.82       6        2904.71    MINE_G                          
 
Ordering summary. Diagonals=    22.  Off-diagonals =    40  Max.size     57
 
Iter      DeltaP            DeltaQ            DeltaV/V            DeltaAng
----  ----------------  ----------------    ----------------    ----------------
 
 0.         12.0173            9.5174             0.07380           0.25515 
      SUB230              MID500              HYDRO1              DOWNTN_W            
 1.          1.1290            1.8070             0.04770           0.02528 
      NUCPANT             NUCPANT             CATDOG_G            NUCPANT             
 2.          0.0344            3.0415             0.04484           0.00715 
      NUCPANT             URBGEN              URBGEN              URBGEN              
 3.          0.0193            0.1599             0.00205           0.00037 
      SUB230              URBGEN              URBGEN              CATDOG_G            
 4.          0.0000            0.0295             0.00038           0.00005 
      EAST230             URBGEN              URBGEN              URBGEN              
  5.          0.0000            0.0017   
      SUB230              URBGEN             
 
 Reached tolerance in    5 iterations
 
Largest mismatch (at bus URBGEN                          ) :    -0.00 MW     
-0.17 MVAR       0.17 MVA. 
System total absolute mismatch:                0.17 MVA
        
```

#### State Estimation {#section_state_esitmation}

The Pre-State Estimator case topology and power flow results are input
to the State Estimator, which computes a further refined estimate of the
system state. The numerical State Estimator results can be viewed in
Analog Measurement sheet, the "SE result" column. These results are also
displayed in diagrams when the analysis activity is set to "State
Estimator" (Menu command **Analysis \> Activity \> State Estimator**).

The weighted-least-square method is used for State Estimation: the
object is to minimize the weighted sum of squares of the measurement
residuals. Therefore, the cost function is formulated as following:

where *z~i~* is the measured value for measurement *i*, *h~i~*(*x*) is
the estimated value (result from State Estimation) for measurement *i*,
\[*z~i~ -- h~i~* (*x*)\] is also known as residual for measurement *i*.
*R~i~* is the weighted factor derived from the convariance matrix
calculated based on measurement variance and State Estimator Jacobian
matrix.

The State Estimator also performs credibility checks on the measurement
values. The results are displayed in State Estimator Tuning Sheet (Menu
command **View>State Estimator Tuning Sheet**). The State Estimator
Tuning Sheet provides "Suspect Topology", "Suspect Flow Direction",
"Branch Credibility Failures", "Bus Credibility Failures", "Suspect
Generation" and "Suspect Load Distribution". Details of the State
Estimator process is described in [State Estimator
](#section_hdw_3zf_xp).

In addition, the normalized residual and bias can be calculated and
displayed in Analog Measurement Sheet (Menu command **View>Measurement
Sheet - Analog Tab**). The normalized residual is \[*z~i~ --
h~i~*(*x*)\]/*R~i~* as denoted in the cost function; And the bias is the
average of the cumulative (non-weighted) residual (\[*z~i~ -- h~i~*
(*x*)\]) over a span of up-to 100 solution cycles.

The log of the state estimator is shown in the Analysis Output window.
Here is an example of the log of a State Estimator solution.

``` c
The system has externals:


External buses:     0 Internal buses:    23
Sub-transmission buses:    23

Thu, Mar 21, 2019 10:51:27:  331     3     0 pseudo measurements added for 
observability

State Estimator Measurement Summary
Measurement
Model     Available  Rejected    In Use
Bus voltages                     15         10          0         10
Branch flows: Critical            2          -          -          -
Non-critical        0          -          -          -
Pseudo              0          -          -          -
Ampere              0          0          -          -
Total             2          4          0          4
Bus injections:
Measured:   Critical            8          -          -          -
Non-critical        0          -          -          -
Total             8          -          -          -
Zero-       Critical           10          -          -          -
injection:  Non-critical        0          -          -          -
Total            10          -          -          -
Pseudo                          2          -          -          -
Total                          20         24          0         24
Transformer Tap positions:
Measured            0          -          -          -
Unmeasured          0          -          -          -
Total                           0          0          0          0
Total measurements               37         38          0         38
Injection constraints are from row             1 to    10

Jacobian nonzeros before factorization:   107
Jacobian nonzeros after  factorization:   162
Nonzeros in Q mat before factorization:    54
Nonzeros in Q mat after  factorization:    55


Iteration   0
Cost                           0.5805679E+05
New cost =   0.84550E+02 old cost =   0.58057E+05

Iteration   1
Cost                      0.84550E+02
Max voltage correction    0.12874E-01 on Bus   MID230           (    9)
Max angle correction      0.54068E-02 on Bus   NUC-B            (   14)
Max P residual            0.11151E+00 for Flow on 1_354
Max Q residual            0.48406E+00 for Flow on 1_354
Chi-square percentile     0.00

Cost at solution =    0.8454997E+02

Solution converged in   1 iterations
          
```

#### Post-State Estimation Analysis {#section_post_SE}

The State Estimator results are used to set load and generation in the
network. If there is a discrepancy between the measured and the
estimated injection (load/generation), the injection is allocated based
on measurements and their variances (mis match allocation). The voltage
estimates are used for setting the regulation of generators, shunts,
SVCs etc. It also sets other setpoints such as HVDC flow setpoints, tap
positions etc.

Post-State Estimation Power Flow is calculated for the network. The
power flow results are updated in the network sheet. The power flow
results can also be viewed in the diagrams when the analysis activity is
set to the "Power Flow" (Menu command **Analysis>Activity>Power Flow**).
These are the final -- most refined -- results upon which any further
analysis (e.g. Contingency Analysis) will be based.

The log of power flow is also shown in the Analysis Output window. Here
is an example of the log from Post-State Estimator Power Flow:

``` c
Solving Realtime Power Flow...

Realtime Power Flow solved

Turning off area interchange in all areas

Turning off LTC transformers in all areas

State Estimator transfer to load flow

Algebraic sum of unallocated injections:     0.1 Mw     -0.0 Mvar
Absolute sum of unallocated injections:      0.2 Mw      0.1 Mvar

New value of mismatch distribution =   0


Ordering summary. Diagonals=    22.  Off-diagonals =    40  Max.size     57

Iter      DeltaP            DeltaQ            DeltaV/V            DeltaAng
----  ----------------  ----------------    ----------------    ----------------

0.         12.0178            8.3298             0.05860           0.31821
SUB230              MID500              MID500              NUC-A
1.          0.7469            2.4919             0.01910           0.03511
NUCPANT             HYDRO1              MID500              NUC-A
2.          0.0174            1.8799             0.02790           0.00394
NUCPANT             URBGEN              CATDOG_G            URBGEN
3.          0.0059            0.2758             0.00332           0.00043
SUB230              URBGEN              URBGEN              URBGEN
4.          0.0001            0.0287             0.00034           0.00005
SUB230              URBGEN              URBGEN              URBGEN
5.          0.0000            0.0020
SUB230              URBGEN

Reached tolerance in    5 iterations

Largest mismatch (at bus URBGEN                          ) :    -0.00 MW     
-0.20 MVAR       0.20 MVA.
System total absolute mismatch:                0.20 MVA
          
```

The status of the realtime solution is also indicated in the status bar.
The background color of text "RT" gives status of the Real Time
solution.

**Green:** All processes (Pre-State Estimator, State Estimator and
Post-State Estimator Power Flow) are converged.

**Yellow:** The final Post State Estimator Power Flow failed based on
State Estimation results, but converged based on updated real-time
measurement values. The snapshot case is not fully accurate, but can be
used for troubleshooting the issue.

**Red:** One or more of the processes diverged including the final
Post-State Estimator Power Flow. The resulting case is a diverged case
which could be used for troubleshooting the issue.

![Real Time solution status. Green indicate a solved real time
case.](/images/C10_RT_status_status_bar.png)

**Summarized Realtime solution process**

                      1.    Pre-SE PF:
                    
                            •  Read switch telemetry status -> Run Topology (if needed)
                          
                            •  Switch with flow measurement transfer into Zero Impedance Branch (ZBR) -> Run 
                                Topology (if needed)
                          
                            •  Read analog data -> Run Topology (if needed)
                          
                            •  Device status auto correction -> Run Topology (if needed)
                          
                            •  Run Power Flow
                          
                                 ◦  if failed: stop, PF red, SE red, RT red
                               
                                 ◦  if succeeded:
                               
                                      □  Set network parameters using measurements -> Run Topology (if needed)
                                    
                                      □  Run PF with updated network parameters
                                    
                                          -  if failed: revert back to schedule data Power Flow, continue to State Estimator
                          
                                          -  if succeeded: continue to State Estimator
                          
                      2.    SE:
                    
                            •  Initialize State Estimator
                          
                                 ◦  if failed: stop, PF green, SE red, RT red
                               
                                 ◦  if succeeded:
                               
                                      □  Run State Estimator
                                    
                                          -  if failed: stop, PF green, SE red, RT red
                            
                                          -  if succeeded: Retrieve State Estimator results for post-SE Power Flow, continue to 
                                             Post-SE Power Flow
                            
                      3.    Post-SE Power Flow:
                      
                            •  Update system parameters using State Estimator results
                            
                            •  Run Topology and Power Flow
                            
                                 ◦  if failed: revert to measurement-based Power Flow. Run Topology and Power Flow:
                                 
                                      □  if failed: PF red, SE green, RT red;
                                      
                                      □  if succeeded: PF green, SE green, RT yellow
                                      
                                 ◦  if succeeded: PF green, SE green, RT green
              

## Measurements {#section_w2w_3zf_xp}

When a new case is built, measurement instances are added from the model
to the case to act as locational placeholders for the telemetered values
(which are critical input to the State Estimator). PSS®ODMS supports
\"plug-in\" integration with real-time and/or historical measurement
data through OPC DA/HDA protocols.

SISCO's AX-S4 ICCP product provides an OPC DA server interface to ICCP
measurement data and is consequently often bundled with PSS®ODMS. Other
software vendors may provide their own OCP server interfaces. For
example, OSI provides an OPC DA/HDA server interface to PI Historian.

Unique identifiers are used to map actual measurement values to the
measurement instances used by the State Estimator function. Multiple
PSS®ODMS instances/workstations communicate directly with one instance
of the OPCsync utility (a standalone DCOM service) running on a server
machine. OPCsync handles the communication protocols required to
interface with an OPC DA/HDA server. PSS®ODMS subscribes to a set of
measurement points and OPCsync distributes the measurement values to
each connected PSS®ODMS instance simultaneously. Each PSS®ODMS instance
executes its own real-time process solution (maximizing flexibility and
performance). Measurement values are stored in saved cases, allowing for
unlimited off-line study of both real-time and historical snapshots.

Measurement instances (including external IDs) can be imported into the
PSS®ODMS CIM database model from various CSV file formats, including the
ICCP ISN format, making the process of measurement integration as
efficient as possible. PSS®ODMS supports multiple MeasurementValueSource
instances to allow convenient switching between different measurement
sources such as ICCP and data historian.

### Quality and Validity {#section_x2w_3zf_xp}

Measurement Quality (numerical) and Validity (text string) values are
retrieved from the OPC DA/HDA interface along with the measurement
value. The Quality code is used by the State Estimator in determining
whether or not to use the measurement value. The Validity string is
purely informational.

### Measurement Status {#section_y2w_3zf_xp}

After each State Estimator run, displayed analog measurement statuses
are automatically updated to the following:

-   IN_USE -used by the State Estimator calculation

-   IGNOR/DATA - ignored by the State Estimator due to known bad quality

-   IGNOR/USER - ignored by the State Estimator due to explicit
    \'Ignore\' user setting

-   IGNOR/TELE - ignored by the State Estimator due to lack of data
    update

-   REJ/LIMIT - rejected by the State Estimator due to failed limit
    check

-   REJ/BAD - rejected by the State Estimator due to Bad Measurement
    Identification check

-   DEACTVATED - \"permanently\" ignored by the State Estimator due to
    multiple rejections (can be manually reactivated via context menu
    command in the Analog Measurements spreadsheet view)

Note: For flow measurement (MW/MVar), the measurement is rejected
(status REJ/LIMIT) if the measured value exceed the limit of the
measurement. For Voltage measurement, ± 30 % of the limit of measurement
is used. Tap measurement is rejected if the measured value is outside
the tap range of the equipment.

### Normalized Residual and Bias {#section_ffw_3zf_xp}

The Normalized Residual is the residual calculated between the measured
value and the result from state estimation, using the following formula:
(Measured-Value - SE-result) \* sqrt(Weighted Factor)

Bias statistics can be retrieved based on the residual. The bias is the
average of the cumulative (non-weighted) residual (Measured-Value -
SE-result) over a span of up-to 100 solution cycles. Following logic
describes the relationship between Residual and Bias:

nmbias = nmbias + 1

if (nmbias .gt. 100) nmbias = 100

msbias = ((nmbias - 1) \* msbias + residl) / nmbias

(where nmbias is number of normalized residuals, msbias is bias, residl
is normalized residual).

PSS®ODMS has the capability to simulate real-time measured values for
demonstration purposes. A user-configured \"noise\" value can be applied
to the simulated measurement values for variance.

### Measurements sheet columns {#sect2_azx_2hz_35}

  -----------------------------------------------------------------------
  Column              Description
  ------------------- ---------------------------------------------------
  Subscribed          Whether or not the measurement successfully
                      subscribed to OPCsync for updates.

  Updated             The most recent time that the measurement was
                      updated in the State Estimator.

  Value               In-memory buffer containing the most recent
                      measured value from OPCsync.

  Quality             OPC quality code; for analog measurements, any
                      quality value besides c0 (GOOD) will be interpreted
                      as \"bad\" for the State Estimator solution.

  Validity            OPC validity string, for reference only (but should
                      be consistent with Quality).

  Timestamp           OPC timestamp, for reference only.

  SE Result           The measurement value estimated by State Estimator.

  PF Result           The result of post State Estimator power flow
                      solution.

  Manual Flag         Set the measurement value manually.

  Ignore Flag         Ignore the measurement from State Estimator
                      (Measurement status will be changed to IGNOR/USER).

  Reverse Flag        Set the measurement value to reverse.

  Normalized Residual Normalized difference between measured value and
                      State Estimator Result.

  Bias                Measurement bias over State Estimator execution.

  Variance (%)        Variance of the measurement, editable, smaller
                      variance SE tries to coerce results close to
                      measured value.

  Limit               Limit of measurement
  -----------------------------------------------------------------------

### Measurements submenu (Analysis menu) {#sect2_f1y_2hz_35}

Menu Analysis-Measurements provides following measurements submenu:

  -----------------------------------------------------------------------
  Menu                Description
  ------------------- ---------------------------------------------------
  Enable OPCsync      Enables OPCsync connection and measurement update
                      subscription.

  Simulate Updates    Disables OPCsync connection and enables simulated
                      measurement updates in Realtime mode (for
                      demonstration purposes only).

  Load Tuning         Loads State Estimator tuning parameters (Manual
  Parameters          Flag, Ignore Flag, Reverse Flag, Variance and
                      Limit) from the model into the current case.

  Store Tuning        Stores State Estimator tuning parameters (Manual
  Parameters          Flag, Ignore Flag, Reverse Flag, Variance and
                      Limit) from the current case to the model.

  Reload Subscription Initializes measurement subscription IDs from the
  IDs                 model.

  Reset to Defaults   Resets measurement update times and quality codes
                      to defaults.

  Store Measurements  Stores measured values from the current case to
                      MeasurementValue instances in the model associated
                      with the selected MeasurementValueSource.

  Store Result        Stores result measurement values from the current
  Measurements        case to MeasurementValue instances in the model
                      associated with the selected
                      MeasurementValueSource.

  Add Artificial      Creates artificial measurements in the case (for
  Measurements        demonstration purposes only).

  Refresh             Requests a full update of all subscribed
  Measurements        measurements from OPCsync.
  -----------------------------------------------------------------------

## Spreadsheet Windows {#section_gfw_3zf_xp}

PSS®ODMS provides various multi-tabbed spreadsheet windows that are key
to interacting with Network Analysis functions. The spreadsheet-style
tabbed views offer features such as context menus, double-click column
header sorting, resizable rows and columns, optionally hidden columns,
extensive filtering options, etc. Most spreadsheet views additionally
support an unlimited number of saved custom configurations which are
easily managed and accessible via sub-tabs.

Read-only cells are distinguished by color from editable cells (white).

### Alarms Sheet {#section_hfw_3zf_xp}

The Alarms sheet provides pre-sorted, color-coded tabular views to
display the computed flow and voltage-based percentage of limit values
based on the current Power Flow solution. All views in the Alarms sheet
are user-configurable. The Alarms sheet is launched from the
**Analysis>Spread-sheets>Alarms command**.

If the current Power Flow solution is invalid, the Alarms sheet will be
unavailable or empty.

### Network Sheet {#section_ifw_3zf_xp}

A large portion of the data that comprises the case is accessible from
the Network spreadsheet window, launched from the
***Analysis>Spreadsheets>Network*** command (or corresponding toolbar
button). The Network sheet contains different pages/views for the
various elements in the case, such as System (summary), Areas,
Substations, Islands, Buses, Sections, Switches, Lines, etc.
Additionally, it provides an Out of Service view, which lists all the
devices in the case that are electrically isolated at any given time
(based on the Topology solution).

### Measurements Sheet {#section_jfw_3zf_xp}

Measurement information is presented in a a separate spreadsheet window
launched from the ***Analysis>Spreadsheets>Measurements*** command (or
corresponding toolbar button). Analog and Switch measurements are listed
in different tabbed views. As with the Network sheet, the Measurements
sheet contains both editable and read-only cells. Editing changes are
immediately applied to the appropriate measurement object(s) in memory.

### State Estimator Tuning Sheet {#section_pfw_3zf_xp}

The State Estimator tuning sheet provides various views designed to
facilitate the process of State Estimator tuning by displaying
diagnostic reports of specific data problems. For more information,
refer to [State Estimator tuning](#sect1_r1y_2hz_35).

### Contingency Setup Sheet {#section_qfw_3zf_xp}

The Contingency Setup sheet provides a set of views designed for
configuring the Contingency Analysis solution.

## Output Window {#section_rfw_3zf_xp}

The Analysis Output window displays progress-related information in text
format, such as the build case log, Realtime Process execution
information with solution convergence information and error/warning
messages. The window can be launched from the **Analysis>Output Window**
menu command (or corresponding toolbar button).

![Analysis Output
Window](/images/PSSODMS_UserManual_2014-10-17114243_img_142.png)

## Scripting {#section_sfw_3zf_xp}

Network Analysis supports Python scripting using the built-in pssoPy
API. Script files are interpreted and executed by the software
internally, largely bypassing the GUI; however, custom output from any
script can be displayed in the Output window.

Python is a full-featured, modern, platform-independent programming
language with many freely available tools and libraries, which is ideal
for scripting. Siemens PTI's pssoPy module is an extensive,
object-oriented Python API specifically designed for Network Analysis
scripting. A comprehensive pssoPy API reference document is included
with PSS®ODMS and sample Python scripts can be found under the
Python\\example subdirectory.

ASC (Activity Sequence Control) is the original native scripting
language of the analysis engine. It has a similar syntax to IPLAN, the
original native scripting language of PSS®E. Support for this legacy
scripting language is now limited to basic commands.

Since PSS®E also supports Python scripting, it is possible to seemlessly
integrate PSS®ODMS and PSS®E, taking advantage of the ability to export
a case to PSS®E RAW format.

### Interactive Script Recording {#section_bgw_3zf_xp}

The application provides the capability to interactively record Python
script files by executing commands through the user interface. This
functionality is most commonly used to create scripts for user-defined
contingencies (which typically involves simply opening multiple
breakers). To record a Python script:

1.  Choose the ***Analysis>Scripting>Record Script*** command.

2.  The Script Editor window will appear.

    ![Recording a
    Script](/images/PSSODMS_UserManual_2014-10-17114243_img_146.png)

3.  Common study-oriented operations, such as toggling breakers/switches
    and adjusting load or generation will be captured as Python commands
    in the order in which they are executed in the GUI. The command file
    may also be manually edited at any time.

4.  When finished recording/editing, choose the
    ***Analysis>Scripting>Stop Recording*** command (or corresponding
    toolbar button). At this point, the case will revert to its previous
    condition and you will be prompted to save the script file.

5.  An open script file may be executed at any time by choosing the
    ***Analysis>Scripting>Run Script*** command (or corresponding
    toolbar button). If no script file is open, you will be prompted to
    select a previously saved script file.

6.  The results of the script execution may be displayed in the Output
    window. Additionally, any open spreadsheets and one-line diagrams
    will be updated to reflect any modifications the script may have
    made to the current case in memory.

Any script file may be opened for editing within the program by choosing
the ***Analysis>Scripting>Open Script*** command. Alternatively, script
files may be edited using a text editor or IDE of choice.

### Custom Commands Menu {#section_agw_3zf_xp}

***Analysis>Custom Commands*** is a user-customizable menu of ASC
commands (with several default commands provided for reference). For
convenience, this menu can be configured to contain frequently used ASC
commands.

![Custom Commands
Menu](/images/PSSODMS_UserManual_2014-10-17114243_img_145.png)

To customize the menu, edit the \"ASC Command Menu.ini\" file under the
\\PSSO subdirectory of the installation directory. The file format is
very straightforward and the file itself contains instructional
comments.

PSS®ODMS needs to be restarted after editing the \"ASC Command
Menu.ini\" file.

## Analysis Options {#section_jgw_3zf_xp}

The program options related to Network Analysis functions are all
grouped within a single multi-tabbed dialog (some tabs are dependent on
the license configuration). Solution options (such as Power Flow
settings) are locally stored in a special file named \"OPTIONS.DEF.\"
All other options are stored in the Registry under HKEY_CURRENT_USER
(standard practice for Windows program settings).

The Analysis Options dialog can be launched by choosing the
**Analysis>Options** menu command (or corresponding toolbar button).

### Analysis Options Overview {#section_nhw_3zf_xp}

  -----------------------------------------------------------------------
  Tab                 Description
  ------------------- ---------------------------------------------------
  General             Contains miscellaneous options including startup
                      settings, active limit sets and directory settings.

  Power Flow          Contains options specific to the Power Flow
                      activity.

  State Estimator     Contains options specific to the State Estimator
                      activity.

  Outage Ranking      Contains options specific to the Outage Ranking
                      activity.

  Contingency         Contains options specific to the Contingency
                      Analysis activity.

  Realtime            Contains client-specific options related to
                      Realtime Mode.

  OPCsync             Contains options related to OPCsync connectivity
                      and measurement updates.
  -----------------------------------------------------------------------

### General Options {#section_ohw_3zf_xp}

  -----------------------------------------------------------------------
  Option              Description
  ------------------- ---------------------------------------------------
  Startup             Controls program startup behavior.

  Limits              Specifies the active flow and voltage limit sets
                      for the current case, displayed condition and
                      preferred units; enables or disables special
                      reverse flow limit logic.

  Directories         Specifies the working directory and script
                      directory.

  Solution Options    Supports importing, exporting and archiving
                      solution options files (OPTIONS.DEF).

  PSS®E Export        The Options button launches a dialog of options
                      related to the PSS®E export function.
  -----------------------------------------------------------------------

### Power Flow {#section_xhw_3zf_xp}

  -----------------------------------------------------------------------
  Option              Description
  ------------------- ---------------------------------------------------
  Algorithm           Specifies which standard numerical method is used
                      for power flow computation.

  Start point         Specifies flat-start or non flat-start solution.

  Convergence         Specifies the global convergence tolerance in per
  tolerance (pu)      unit for the iterative numerical method. Power flow
                      convergence is reached given that the following
                      criteria are satisfied: (1) P mismatch is less than
                      the tolerance for ALL PQ buses; (2) Q mismatch is
                      less than the tolerance for ALL PQ buses; (3) P
                      mismatch is less than the tolerance for ALL PV
                      buses; (4) \|V\| mismatch is less than the
                      tolerance for ALL PV buses; (5) P mismatch is less
                      than the tolerance if any area-interchange
                      scheduled.

  Maximum iterations  Specifies maximum power flow iteration beyond which
                      the solution is treated as diverged.

  Var limit checking  Specifies the iteration at which to apply reactive
  iteration           power mismatch checking (set to 0 to apply before
                      the first iteration or -1 to disable).

  Zero impedance      Specifies the minimum reactance value for lines,
  threshold           below which they will be treated as zero impedance
                      branches.

  Tap adjustment type Specifies either step-adjusted or direct-adjusted
                      taps.

  Mismatch            Specifies how active power mismatch is distributed:
  distribution        \'Swing bus\' - system losses are compensated by
                      the swing bus generator output; \'Internal buses\'
                      - system losses are compensated by generators in
                      designated internal areas; \'External buses\' -
                      system losses are compensated by generators in
                      designated external areas; \'All buses\' - system
                      losses are compensated by all dispatchable
                      generators in the system; \'Slack load\' - area
                      interchange mismatches are compensated by
                      designated slack loads.

  Convergence         Specifies the level of detail for solution
  information         convergence output.

  Load profile        Specifies smoothing factor for load scaling.
  smoothing factor    

  Local allocation    Specifies whether to scale load based on the
  method              original individual allocated load parameters or
                      State Estimator results.

  Enable generator    Allows automatic adjustment for generator min/max
  reactive power      Mvar during MW output update, if capability curve
  limit adjustment    is avaialble.

  Calculate           Enables special computation for flows across
  approximate switch  switching devices in power-flow, which can be
  flows               displayed in the one-line diagram.

  Solution divergence Enables limited solution divergence prevention
  prevention          logic.

  Preserve            Enables transformer winding connection angle (e.g.,
  transformer winding 30 degree by wye-delta) preserved in a power-flow
  connection angles   solution. Note that this option does not apply to
                      phase shifters, i.e., angle shifting for MW control
                      purpose will always be preserved.

  Toggle adjacent     Enables switch status toggle on device In Service
  switches on device  change. When disabled, the adjacent switch status
  In Service change   becomes independent from the equipment status,
                      where equipment In Service solely represents
                      equipment availability, but not its online status.
                      E.g., a unit can be In Service while its associated
                      breaker is open, meaning that the unit is available
                      (stand-by) to be put back online by closing the
                      breaker, whereas Out of Service means the unit is
                      physically disconnected from the grid (maybe for
                      maintenance purpose), thus being not available and
                      infeasible to participate in operations such as
                      automatic generation control, area interchange
                      control, unit commitment, remedial action and etc.

  Automatic Controls  Opens a dialog to selectively enable area
  button              interchange, transformer and bank controls by area.
  -----------------------------------------------------------------------

### State Estimator {#section_h3w_3zf_xp}

+--------------------+-------------------------------------------------+
| Option             | Description                                     |
+====================+=================================================+
| Convergence        | Specifies the convergence tolerance (in pu) for |
| tolerance          | the iterative State Estimator numerical method. |
+--------------------+-------------------------------------------------+
| Maximum iterations | Specifies maximum state estimator iteration     |
+--------------------+-------------------------------------------------+
| Start point        | Specifies flat start or not flat start for      |
|                    | state estimator iteration                       |
+--------------------+-------------------------------------------------+
| Transformer tap    | Specifies transformer tap estimation (None,     |
| estimation         | Unmeasured, Measured or All)                    |
+--------------------+-------------------------------------------------+
|     Unmea          | Specifies variances to be used                  |
| sured tap variance |                                                 |
|     Virtual me     |                                                 |
| asurement variance |                                                 |
|     Pseudo-        |                                                 |
| injection variance |                                                 |
|     Pseud          |                                                 |
| o-voltage variance |                                                 |
+--------------------+-------------------------------------------------+
| Suspect generation | Specifies generation factor to be used for      |
| factor             | identifying suspect generation (displayed in    |
|                    | the tuning table)                               |
+--------------------+-------------------------------------------------+
| Suspect load       | Specifies generation factor to be used for      |
| factor             | identifying suspect load distribution           |
|                    | (displayed in the tuning table)                 |
+--------------------+-------------------------------------------------+
| Sequential         | Specifies number of sequential rejections after |
| rejection limit    | which the measurement is permanently ignored    |
|                    | (status "DEACTVATED")                           |
+--------------------+-------------------------------------------------+
| Total rejection    | Specifies number of total rejections after      |
| limit              | which the measurement is permanently ignored    |
|                    | (status "DEACTVATED")                           |
+--------------------+-------------------------------------------------+
| MW measurement     | Specifies MW mismatch limit for branch          |
| credibility limit  | credibility (displayed in the tuning table)     |
+--------------------+-------------------------------------------------+
| MVar measurement   | Specifies MVar mismatch limit for branch        |
| credibility limit  | credibility (displayed in the tuning table)     |
+--------------------+-------------------------------------------------+
| kv measurement     | KV measurement credibility limit is used to     |
| credibility limit  | check the inconsistence when multiple voltage   |
|                    | measurements exist at the same bus. If the      |
|                    | difference between a voltage measurement and    |
|                    | the average of total voltage measurements is    |
|                    | greater than KV measurement credibility limit   |
|                    | the measurement would be rejected in SE         |
|                    | calculation.                                    |
+--------------------+-------------------------------------------------+
| Default            | Set the largest value for flow or voltage       |
| measurement limit  | measurement which equals k time of flow or      |
| factor             | voltage measurement limit                       |
+--------------------+-------------------------------------------------+
| Boundary error     | Special option to handle the boundary error     |
| method             | between telemetered and non-telemetered area    |
|                    | for stability of post State Estimator real-time |
|                    | convergence (refer to [Boundary error           |
|                    | handling](#section_se_boundary_error)).         |
+--------------------+-------------------------------------------------+
| Enable realtime    | (When checked) Enables post SE realtime power   |
| power flow         | flow solution in Study mode                     |
| solution in Study  |                                                 |
| mode               |                                                 |
+--------------------+-------------------------------------------------+
| Disable SE         | (When checked) Disables SE algorithm and runs   |
| algorithm          | realtime power flow only                        |
| (realtime power    |                                                 |
| flow only)         |                                                 |
+--------------------+-------------------------------------------------+
| Random measurement | Only for demonstration purpose when simulating  |
| noise              | measurement updates. (When checked) Adds random |
|                    | noise to the simulated measurement values.      |
+--------------------+-------------------------------------------------+
| Update Tap control | (When checked) Enables transformer tap control  |
| kV range           | target/range update by Post SE power flow       |
+--------------------+-------------------------------------------------+
| Update Bank        | (When checked) Enables bank control             |
| control kV range   | target/range update by Post SE power flow       |
+--------------------+-------------------------------------------------+
| Look               | (When checked) Excludes sub-transmission banks  |
| sub-transmission   | from Bank kV adjustment                         |
| Banks              |                                                 |
+--------------------+-------------------------------------------------+
| Status Correction  | Launches a dialog of options related to switch  |
|                    | status auto-correction.                         |
+--------------------+-------------------------------------------------+

### Outage Ranking {#section_i3w_3zf_xp}

  -----------------------------------------------------------------------
  Option              Description
  ------------------- ---------------------------------------------------
  Ranking Method      Enables or disables the three available ranking
                      methods, along with corresponding violation-based
                      filtering options.

  Outage Criteria     Specifies the outage criteria (by area, voltage
                      level and device type) for branch and unit outages
                      to generate a list of single-outage contingencies.

  Branch Monitoring   Specifies the monitored branches (by area, voltage
  Groups              level and device type) for contingency result
                      pre-filtering.

  Exclude             This option is under Branch Monitoring Group window
  transformers        and it is applied to all groups defined by the
  connected to        user. Enable it means outage ranking will check if
  unselected voltage  the transformer is flow-violated only when kV
  levels              levels for both ends of the transformer are
                      selected by the user. This is useful to filter out
                      undesired candidates like distribution
                      transformers. Disable it means outage ranking will
                      check the transformer if kV level for either end is
                      selected. This option is unchecked by default.

  Local voltage       Convergence tolerance for local voltage ranking
  convergence         algorithm
  tolerance           

  Number of local     Specifies the number of tiers which the local
  voltage tiers       voltage ranking algorithm should include when it
                      builds the sub-networks to be analyzed for the
                      ranking. Larger number of tiers uses larger
                      sub-networks and is more accurate but takes longer
                      calculation time and vice versa.

  Limit condition for Specifies limit condition to be used (Normal,
  flow violation      Emergency1, Emergency2).
  ranking             

  Voltage deviation   Specifies the maximum acceptable deviation in bus
  percentage limit    section voltage. Voltages which deviate from the
                      specified base value by more than this amount will
                      be alarmed. The voltage deviation is specified as a
                      percentage of the base value.

  Automatic           Enables or disables automatic Contingency
  Contingency         generation/selection based on Outage Ranking
  Generation          results.
  -----------------------------------------------------------------------

### Contingency {#section_j3w_3zf_xp}

  -----------------------------------------------------------------------
  Option              Description
  ------------------- ---------------------------------------------------
  N-1 Contingency     Enables or disables automatic Contingency selection
  Selection           for the three available ranking methods.

  PF Solution         Specifies power flow solution parameters to be used
                      during Contingency Analysis runs.

  Limit Conditions    Specifies the condition-specific limit data used to
                      compute contingency result violations.

  Contingency Results Allows for general contingency results filtering.
  -----------------------------------------------------------------------

### Realtime {#section_r3w_3zf_xp}

+-------------------+---------------------------------------------------+
| Option            | Description                                       |
+===================+===================================================+
| Advanced          | Specifies the advanced synchronization mode for   |
| Synchronization   | this workstation:                                 |
|                   |                                                   |
|                   | Independent Console - allows opening any saved    |
|                   | case for Realtime Mode, uses the default          |
|                   | OPTIONS.DEF solution file.                        |
|                   |                                                   |
|                   | Synchronized Console - forces automatic reloading |
|                   | of the specified master saved case file (and      |
|                   | solution options) after each realtime solution    |
|                   | cycle; disables overwriting this file; requires a |
|                   | separate workstation to be configured with the    |
|                   | Master Console setting.                           |
|                   |                                                   |
|                   | Master Console - forces automatic overwriting of  |
|                   | the specified master saved case file (and         |
|                   | solution options) after each realtime solution    |
|                   | cycle; assumes at least one other workstation is  |
|                   | configured with the Synchronized Console setting. |
+-------------------+---------------------------------------------------+
| Outage Criteria   | Specifies realtime case backup behavior including |
|                   | file path and naming. The filename could be       |
|                   | appended with date/time or with a file counter.   |
|                   |                                                   |
|                   | The Advanced options allow for further automating |
|                   | exports to PSS®E, triggering external processes   |
|                   | and invoking scripts.                             |
+-------------------+---------------------------------------------------+
| Analysis          | Allows selectively enabling analysis functions    |
| Functions         | comprising the realtime solution.                 |
+-------------------+---------------------------------------------------+

### OPCsync {#section_s3w_3zf_xp}

+-------------------+---------------------------------------------------+
| Option            | Description                                       |
+===================+===================================================+
| OPCsync           | Specifies the OPCsync server name and related     |
| Connection        | options including a Connect button to test the    |
|                   | connection from this workstation to OPCsync.      |
+-------------------+---------------------------------------------------+
| Measurement       | Specifies the measurement update subscription     |
| Updates           | method and related options.                       |
|                   |                                                   |
|                   | Depending upon the measurement server, user could |
|                   | use Near real-time (OPC DA) or Historical (OPC    |
|                   | HAD) methods. For Historical methods, date/time   |
|                   | of the measurement update could be selected.      |
|                   |                                                   |
|                   | All log details are shown in the Analysis Output  |
|                   | log.                                              |
+-------------------+---------------------------------------------------+
| Solution Cycle    | Specifies the timed solution cycle affecting all  |
|                   | client workstations (this is actually an OPCsync  |
|                   | setting, so it requires connecting to OPCsync     |
|                   | first).                                           |
|                   |                                                   |
|                   | If "Force realtime solution whenever a measured   |
|                   | switch status changes" is selected, a wait time   |
|                   | in seconds can be specified in order to wait for  |
|                   | system stabilization and measurement updates.     |
+-------------------+---------------------------------------------------+

### Display Settings {#section_bjw_3zf_xp}

The Display Settings dialog is a multi-tabbed, modeless dialog
containing user-specific settings related to Network Analysis graphical
and tabular displays. It can be launched by choosing the ***Analysis>
Display Settings*** menu command (or corresponding toolbar button). The
Apply button can be used to examine the impact of different settings on
open diagram and spreadsheet windows without having to close and reopen
the dialog.

  -----------------------------------------------------------------------
  Tab                 Description
  ------------------- ---------------------------------------------------
  General             Contains miscellaneous display settings.

  Labels              Contains settings related to one-line diagram
                      labelling.

  Results             Contains settings related to power flow results
                      display.

  Alarms              Contains display settings related to the Alarms
                      sheet.

  Measurements        Contains settings related to measurement value
                      display.

  Topology            Contains display settings related to the Topology
                      Analysis activity.
  -----------------------------------------------------------------------

## Error Code Description {#section_igw_3zf_xp}

The list of program error codes returned by API\'s can be found in the
following table with a brief discription and a detailed example.

### Program Error Code {#section_kgw_3zf_xp}

  -----------------------------------------------------------------------
  Error Code  Short Description        Detail/Example
  ----------- ------------------------ ----------------------------------
  2001        Device name duplication  E.g., section name duplicate,
                                       adding section into network
                                       failed.

  2002        Maximum number exceeded  E.g., number of sections is
                                       greater than the configuration
                                       limit, adding section into network
                                       failed.

  2003        Invalid component handle E.g., section handle does not
                                       exist in the network.

  2004        Invalid data value       E.g., invalid in-service status
                                       for devices.

  2005        Invalid data code        E.g., invalid voltage control mode
                                       for generating unit.

  2006        Invalid data format.     E.g., OPTIONS.DEF file has invalid
                                       format.

  2007        Invalid topology         E.g., running power flow when
                                       system topology is invalid.

  2008        Invalid operation        E.g., running contingency analysis
                                       with DC power flow option.

  2009        Invalid network state    Network memory is not initialized.

  2010        Invalid component type   The type of the device is
                                       currently not supported in the
                                       network analysis.

  2011        Generic run-time error   Power flow failure, state
              in network analysis      estimator failure, real-time
                                       solution failure, get case
                                       failure, network memory
                                       initialization failure and etc.

  2012        Invalid component name   A given name is not found under
                                       certain type of device.

  2013        Data not available       E.g., voltage violation limit is
                                       not available.

  2014        Cannot open file         Cannot open the given file.

  2015        Cannot close file        Cannot close an opened file.

  2016        Cannot write to file     Cannot write to an opened file.

  2017        Substations have no      No switches exist in the network
              switching device         (primarily used in PSS®E v34
                                       node-breaker export).
  -----------------------------------------------------------------------

### Analysis Engine Error Code {#section_ugw_3zf_xp}

  -----------------------------------------------------------------------
  Error Code          Description
  ------------------- ---------------------------------------------------
  1                   .sav file cannot be opened

  2                   Multiple files with the same name are found for the
                      given .sav

  3                   .sav is opened but the length of the file is
                      incorrect

  4                   .sav is opened but the format of the file is
                      incorrect

  5                   File cannot be overwritten

  6                   Options.def file is invalid

  7                   Options.def file has the wrong format

  13                  Network model not loaded

  14                  Data errors in processing general system topology
                      analysis

  15                  Maximum number of device limit reached

  16                  Data errors in processing substation topology

  20                  Decoupled load flow divergence

  21                  DC load flow set up failure

  22                  Load flow calculation failure

  23                  No active island exist in the system

  24                  Load flow reached maximum number of iterations

  25                  Newton's load flow divergence

  26                  Bus optimal ordering failure

  89                  Pseudo voltage exceeds limit

  90                  Invalid tap ratio measurement in state estimator

  91                  State estimator diverged or reached iteration limit

  92                  State estimator did not reach solution tolerance

  93, 94              Ordering failed for state estimator

  95, 96, 97, 98      Reached maximum number of bad measurements

  99                  Reached maximum number of loads allowed, no more
                      external balance load can be added

  9999                File cannot be opened
  -----------------------------------------------------------------------
