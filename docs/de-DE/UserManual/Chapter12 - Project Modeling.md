# Project Modeling

## Introduction

Project Modeling is a powerful set of functions to interactively record,
manage and analyze planned model changes in advance of actual
commissioning. Future model changes are organized into multi-phase
Projects, with a specific Commission Date associated with each Phase.
Scenarios may be created based on any future date and further customized
to include selected Project Phases. Any Scenario can be \"activated\"
for previewing. When a Scenario has been activated, associated model
changes are \"virtually\" applied by the user interface (including NTE,
CIMedit and OneLine diagrams), allowing the user view the entire planned
future model at once. Switching to an alternate future version of the
model is done by simply activating a different Scenario. For additional
validation and study, a base case can be built based on the active
Scenario. This case can be directly exported to PSS®E for further
analysis. Since all Project Modeling data is contained in the PSS®ODMS
Data Repository, it is automatically shared by all users. Specific
Project Modeling functions can be restricted on a per-user basis by
configuring user Roles and Privileges in the database (using a special
standalone configuration tool).

Note: Project Modeling is a separately licensed module. Contact Siemens
PTI for an updated license file if you would like to purchase or
evaluate this module.

## Manage Projects Window

The Manage Projects window is the primary interface for Project
Modeling. It allows the user to create and edit Projects, Phases and
Scenarios. To open the Manage Projects window, choose the
***Model>Projects>Manage Projects*** menu command. If no Project
Modeling data exists, the window will be empty. Changes to Project
Modeling data made through the Manage Projects window are automatically
stored in the database model.

![Manage Projects
Window](/images/PSSODMS_UserManual_2014-10-17114243_img_152.png)

## Editing Projects and Scenarios

Projects and Scenarios are the two key concepts of Project Modeling. To
begin using Project Modeling requires at least one Project and one
Scenario.

### Creating a Project

A Project encapsulates a related set of planned model changes organized
as Phases. To create a new Project:

1.  Right-click on the Projects root item in the tree control and choose
    the New Project context menu command to launch the New Project
    dialog.

2.  Fill in the basic Project and (initial) Phase attributes. These
    properties can be changed later from the Manage Projects window and
    additional Phases can be added to the Project (an initial Phase is
    automatically created for convenience as each Project requires at
    least one Phase). The Commission Date box opens a calendar control
    for convenient selection.

3.  Click OK to confirm your selections dismiss the dialog.

    ![New Project
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_153.png)

4.  The new Project and Phase items will appear in the Manage Projects
    tree control.

5.  Click on the Project item in the tree control to view its properties
    in the right panel; click on the Phase item in the tree control to
    view its attributes. The Value boxes are editable for certain
    Project and Phase properties such as Name and Description. Any
    changes are automatically saved in the model. Other properties such
    as Creation Date and Created By are automatically populated by the
    software and are noneditable.

### Adding a New Project Phase

A new Phase can be added to a Project by right-clicking the Project item
in the tree control and choosing the New Phase context menu command.
Fill in the properties in the resulting New Phase dialog and click the
OK button. The new Phase item will appear under the Project. This
process can be repeated to create as many Phases as needed.

Note: The Manage Projects tree control automatically sorts Phases within
a Project by Commission Date.

![New Phase
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_154.png)

### Changing a Commission Date

Since the Commission Date is the single most important property of a
Phase, a separate command is provided to change it. To change the
Commission Date for a Phase, right-click on the Phase item in the tree
control, choose the Edit Dates context menu command and select a new
date using the calendar control in the resulting Phase dialog. After
OK-ing the dialog, the updated Commission Date will be displayed in the
Phase properties.

![Phase Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_155.png)

### Deleting a Project or Phase

To Delete a Project or Phase, right click on the tree control item and
choose the Delete context menu command.

Note: This command issues a verification prompt; deleting a Project or
Phase cannot be undone!

### Creating a Scenario

A Scenario represents a possible future state of the network model and
includes one or more Project Phases. At least one Scenario is required
to make use of the Project Modeling functionality. To create a Scenario:

1.  Right-click on the Scenarios root item in the tree control and
    choose the New Scenario context menu command to launch the New
    Scenario dialog.

    ![New Scenario
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_156.png)

2.  Fill in the Scenario properties. The boxed controls allow
    pre-selection of Project Phases to include in the Scenario. The
    selected Scenario Date is preserved as a property of the Scenario.
    Click the OK button to dismiss the dialog. The new Scenario will
    appear under the Scenarios root item.

### Customizing a Scenario

A Scenario may be customized to include selected Phases from the same
Project or from multiple Projects.

Note: To add a Phase to a Scenario, select a Phase item under a Project
in the tree control, drag the item and release it directly over a
Scenario item. The Phase item will appear under the Scenario.

If a Scenario contains a Phase, then the corresponding Project item will
also be visible for reference. A Scenario need not contain all the
Phases within any given Project; however, including a Phase will
automatically include all other Phases within the same project with
earlier Commission Dates.

![Drag-Dropped
Phase](/images/PSSODMS_UserManual_2014-10-17114243_img_157.png)

1.  To remove a Phase from a Scenario, right-click on the Phase item
    under the Scenario and choose the Remove from Scenario context menu
    command.

    Note: Removing a Phase from a Scenario does not delete the Phase.

2.  To update the contents of a Scenario based its selected date,
    right-click on the Scenario item and choose the Edit Scenario menu
    command to launch the Edit Scenario dialog. You can change the
    Scenario name, description, date and filtering options, or keep the
    same options and click OK.

    ![Update Scenario
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_158.png)

Note: The Update Scenario dialog is designed to accommodate changes to
Phase Commission Dates. Based on the Scenario Date and project state
filtering options, individual Project Phases can be automatically added
to or removed from the Scenario.

### Deleting a Scenario

To delete a Scenario, right-click on the Scenario item in the tree
control and choose the Delete context menu command.

Note: This command issues a verification prompt; deleting a Scenario
cannot be undone!

### Recording Model Changes

A Project Phase is designed to contain a set of related future model
changes. For dependency reasons, all future changes must be recorded in
the context of a Scenario. To record model changes to a Phase:

1.  Right-click on a Phase item under a Scenario in the tree control and
    choose the Start Recording context menu command. The Manage Projects
    window will indicate that the recording mode has been activated.

    ![Recording
    Activated](/images/PSSODMS_UserManual_2014-10-17114243_img_159.png)

2.  Using the OneLine diagram editor, CIMedit and/or CIM Properties,
    create, delete or modify network elements as you normally would when
    editing the base model.

    Note: Recording to a Phase automatically locks it by the current
    user. When a phase is locked, no other users will be allowed to make
    changes to it. A locked Phase is indicated by a \"padlock\" icon
    next to its name and also by its noneditable Locked By attribute.

    Note: If Voltage Level coloring is disabled, equipment additions
    will be highlighted in different colors (such as green) on One-Line
    diagrams.

    ![Recording Model
    Changes](/images/PSSODMS_UserManual_2014-10-17114243_img_160.png)

3.  After completing your modeling changes, save any modified OneLine
    diagrams to preserve the corresponding graphical changes for later
    Scenario activation.

4.  Right-click on the same Phase item in the tree control and choose
    the Stop Recording context menu command. A detailed list of the
    model changes recorded to the Phase will now be visible in the
    Project Modeling window (use the Refresh context menu command if
    necessary).

5.  Model changes recorded into a Phase are initially visible to the
    current user only. To make model changes visible to other users,
    right-click on the Phase item and choose the Publish Local Changes
    context menu command.

6.  After publishing changes, a message box prompt will appear to unlock
    the Phase for modification by other users. If you choose to keep the
    Phase locked, it can be unlocked later via the Unlock Phase context
    menu command.

## Activating a Scenario

Activating a Scenario enables previewing and studying a planned future
version of the model, from high-level one-line diagrams down to the last
detailed attribute. To accomplish this, future project changes are
processed internally by the software to present a comprehensive view of
a planned future version of the model. A typical user only needs to
execute a single command to activate a selected Scenario.

Note: When a Scenario has been activated (and model changes are not
being recorded), all model editing functions are disabled. Only one
Scenario may be activated at a time.

There are two ways to activate a Scenario:

Within the Manage Projects window, right-click on any Scenario item and
choose the Activate context menu command.

1.  With the Manage Projects window closed, choose the
    Model>Projects>Activate Scenario menu command to launch the Activate
    Scenario dialog. Pick a Scenario from the list and click OK to
    dismiss the dialog and activate the selected Scenario.

    ![Activate Scenario
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_161.png)

2.  An active Scenario may be similarly deactivated by right-clicking on
    the Scenario item in the Manage Projects window and choosing the
    Deactivate context menu command or via the Model>Projects>
    Deactivate Scenario menu command.

Note: When a Scenario is deactivated, the user interface returns to its
default state of presenting the \"baseline\" model.

## Building a Scenario Case

The Netowrk Analysis case building function is automatically aware of
the currently active Scenario. To build a case representing a planned
future version of the model, simply activate an existing Scenario, then
choose the Analysis>Build Case menu command and follow the steps as
described in Chapter 10. The Topology Analysis, Power Flow and
Contingency Analysis activities can be used to pre-validate the scenario
case. This case can be exported to PSS®E, which offers powerful
functions specifically designed for transmission planning analysis.

## Incremental CIM/XML

The recorded model changes associated with any Phase can be exported to
an Incremental CIM/XML file. To do this, open the Manage Projects
window, expand the selected Project item (under the Projects root item)
and right-click on the selected Phase item. Choose the Export Model
Changes context menu command and enter a file path in the Save As
dialog. Similarly, model changes can be imported into an empty Phase
from an Incremental CIM/XML file via the Import Model Changes context
menu command.

Note: Successfully importing an Incremental CIM/XML file into a Phase
requires URI's to be consistent between the file and the model. This is
especially important to verify if the Incremental CIM/XML file
originates from an external source (other than PSS®ODMS itself).

Note: The related commands are disabled when a Scenario is active.

## Committing Model Changes

Eventually, the Commission Date for each Phase may be reached, at which
time it is be desirable to incorporate its related changes into the
\"baseline\" network model. To do this, open the Manage Projects window,
expand the selected Project item (under the Projects root item) and
right-click on the selected Phase item. Choose the Commit to Model
context menu command and click OK on the resulting message box prompt.

Note: Incremental CIM/XML export/import is the mechanism that is used by
the software internally to apply recorded model changes to the baseline
model.

Note: The Commit to Model command is disabled when a Scenario is active.

Note: Be sure to back up your database model before using the Commit to
Model command as this operationcan not be undone.

After being committed to the model, the Phase item will remain under the
Project for reference (it may be deleted manually), but it will be
inactive. No further changes may be made to a committed Phase, including
recording model changes. The committed Phase will also disappear from
any Scenarios (since its associated model changes are now part of the
baseline model).

![Commit to Model
function](/images/PSSODMS_UserManual_2014-10-17114243_img_162.png)

![Phase after Commit to
Model](/images/PSSODMS_UserManual_2014-10-17114243_img_163.png)
