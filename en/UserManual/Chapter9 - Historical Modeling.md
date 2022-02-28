# Historical Modeling

## Introduction

PSS®ODMS provides the capability to record model changes, whether made
directly to the base model or via the Commit to Model function of the
Project Modeling module. The detailed model change history can be viewed
in a historical change log window and can be used to automatically
construct a temporary historical model for special study purposes.

## Tracking Model Changes

The automatic tracking of model change events allows for the following
capabilities:

1.  Reviewing the model change history in detail.

2.  The ability to create a historical (i.e. rolled-back) model for any
    point in recorded history for subsequent study.

3.  The ability to export model changes in Incremental CIM/XML format.

After the initial model setup stage, which may include importing and
merging models, inserting breakers and switches, consolidating and
reorganizing various hierarchical elements, and one-line diagram
construction, the model is ready to be transitioned into the
production/maintenance phase. At this point, you may choose to have the
software begin tracking editing changes to the model to provide the
ability to roll the model back to a previous point in time.

### Enabling Change Tracking

Model change tracking can be enabled or disabled for any model via the
Model>History>Track Model Changes menu command. To prevent historical
inconsistency errors, the model history will be reset each time this
command is invoked.

Note: To prevent the casual user from inadvertently wiping out the model
history, this menu command may be locked on an individual user basis by
setting the value of the following special Registry key to 0:

HKEY_CURRENT_USER/Software/PTI/ODMS/Settings/Enable Toggle Change
Logging

![Track Model Changes
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_106.png)

### Exceptions to Change Tracking

Some PSS®ODMS functions (such as Consolidate Substations) are
specifically designed for initial model setup activities which occur
prior to production use. These functions will not be available after
change tracking has been enabled.

In some situations, it may not be desirable to track a specific model
change event, even when change tracking is enabled. For example, the
Alias Name field of a MeasurementValue is commonly used to store a
measurement subscription ID string. If this ID is changed in the
3rd-party historian, it presents a problem for the Historical Case
Builder feature, which relies on valid (i.e. current) ID's to obtain
historical measurement data. Siemens PTI is continuing to research and
develop PSS®ODMS to accommodate these kinds of situations to maximize
usability and minimize maintenance effort.

### Example of Change Tracking

When model change tracking is enabled, the software will quietly record
all editing changes made to the model via the user interface. An example
(adding a new load) is shown below.

![New Equipment
Added](/images/PSSODMS_UserManual_2014-10-17114243_img_107.png)

Historical model change detail can be viewed by choosing the
Model>History>View History command.

![View History
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_108.png)

![Historical Change
Log](/images/PSSODMS_UserManual_2014-10-17114243_img_109.png)

Sets of changes are grouped into Revisions, each with an editable
comment field. Right-click on any Revision record for a context menu of
related commands. The changes associated with any Revision can be
exported in Incremental CIM/XML format via the Export Changes command.

![Export Changes
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_110.png)

### Viewing Individual Equipment History

Historical changes related to individual equipment can be viewed by
selecting the equipment instance in CIMedit and choosing the View
History context menu command.

![View History](/images/PSSODMS_UserManual_2014-10-17114243_img_111.png)

## Historical Case Builder

Historical Case Builder is a set of related functions executed in a
specific sequence to reconstruct a solved operational snapshot case
based on combined historical model and telemetry data. The first step
leverages the capability to automatically create a historical model by
reverse-applying the accumulated individual changes in the model
history. In the second step, a study case is built from the historical
model (refer to [Creating a Historical Model ](#section_epg_ntk_xp)).
Finally, historical measurements are retrieved from a 3rd-party data
historian (such as PI), a State Estimator/Power Flow solution is run and
the solved case is then exported to PSS®E.

![Overview of Historical Case
Builder](/images/PSSODMS_UserManual_2014-10-17114243_img_112.png)

### Creating a Historical Model

Historical model can be created from Model History window. In the Model
History window, expand the date to view model revision. The model
changes in the partucular revision could be seen in the Historical
Changes tab. The modified date/time and user creating the changes is
displayed in the Revision Info tab.

To create a historical model from a particular revision, right click on
the revision and select the ***Create Historical Model*** command.

![Create Historical Model Command in Model History
Window](/images/C9_CreateHistoricalModel.png)

PSS®ODMS will automatically create and connect to the historical model.
The first part of the historical model name will be the same as that of
the original model with a suffix appended to indicate the selected
day/month/year.

Note: The original model will be unaffected; it is only a copy of the
model that is \"rolled back.\"

Note: A historical model should be treated as a temporary copy, for
study purposes only. For example, you can not track changes in a
historical model to create yet another historical model and projects and
scenarios in the original model will not be transferred to the
historical model.

Note: Historical change tracking does not include graphical changes.
Consequently, the diagrams contained in a historical model will reflect
the current network topology, which will most likely not match perfectly
with the historical model. However, the ***Diagram-\>Synchronize with
Model*** command can be used to rectify this situation as needed.

### Building a Historical Case {#section_fpg_ntk_xp}

With the historical model open, first build a base case and solve Power
Flow (see Chapter 10 for detailed instructions). Configure OPCsync to
point to the historical measurement archive. Configure PSS®ODMS to
retrieve measurements for the selected date/time using the Analysis
Options dialog, OPC page.

![Configuring Historical
Measurements](/images/PSSODMS_UserManual_2014-10-17114243_img_115.png)

Finally, enter Realtime Mode and verify retrieval of the complete set of
historical measurement values in the Measurements spreadsheet. Solve
State Estimator/Power Flow and export the solved case to PSS®E.

Note: Additional State Estimator tuning may be needed to solve the
historical snapshot case.
