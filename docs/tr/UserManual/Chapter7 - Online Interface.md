# OneLine Interface

## Introduction

This chapter describes how to use the OneLine interface to build and
manage diagrams and perform graphical model editing in PSS®ODMS.
Diagrams are normally saved to or loaded from the current PSS®ODMS
database model, but may also be imported or exported in various file
formats.

## OneLine Overview

The OneLine interface serves a variety of purposes in PSS®ODMS. It can
be used to auto-build diagrams to quickly validate the topology a newly
imported network model. Commonly, after auto-building a diagram, its
layout is manually adjusted and the diagram is saved to the database so
it can be reopened with all of the customizations preserved. OneLine
diagrams provide an intuitive way of interacting with the model and are
automatically mapped upon creation for convenient access to model
attributes (no manual network mapping is required). Diagrams are
self-synchronizing to account for any model changes that have been made
externally. Finally, the same OneLine diagrams used for model editing
are fully reusable for visualizing network analysis results and
conducting related studies.

## Substation Diagrams

A substation diagram is a schematic representation of all the equipment
contained within a given substation. Substation symbols show where the
ends of branch equipment connect to other substations and act as
navigational links to other substation diagrams.

![Example Substation
Diagram](/images/PSSODMS_UserManual_2014-10-17114243_img_30.png)

### Opening/Building Substation Diagrams

1.  Choose ***Diagram>Open Diagram(s)*** on the main menu (or use the
    corresponding File toolbar button) to launch the Open Diagram(s)
    dialog.

    ![Open Diagram(s)
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_31.png)

2.  The Open Diagram(s) dialog can also be used to generate other types
    of diagrams. Make sure the AutoBuild Type option is set to
    Substation.

    ![Open Diagram(s)
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_32.png)

3.  To open substation diagrams in normal bus-breaker format (the
    default option), set the AutoBuild Format option to Bus-breaker. To
    open substation diagrams in bus-branch format (advanced
    functionality), set the Format option to Bus-branch.

    Bus-branch format hides all breaker detail in the resulting
    schematic diagram and is heavily dependent on consistent and correct
    Topological Node associations in the network model.

4.  Expand area tree control item(s) and select one or more substation
    items. Multiple substations may be selected by holding down the Ctrl
    key while clicking on the individual substation items. All
    substations within an entire area can be selected at once by
    clicking on the area item.

    If a substation icon is colored black, it indicates a saved diagram
    exists for that substation; if colored gray, it indicates a saved
    diagram does not exist and if selected, will be auto-built from the
    network topology. This behavior is also dependent on the selected
    AutoBuild Format.

5.  If any substation items with gray icons are selected, click the
    AutoBuild Options\... button and verify the options in the resulting
    dialog. These options will affect the initial layout of auto-built
    diagrams only. Click the OK or Cancel button to dismiss the dialog.

    ![AutoBuild Options
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_33.png)

6.  Click the OK button in the Open Diagram(s) dialog to dismiss the
    dialog and open the selected substation diagram(s).

    To quickly open a single substation diagram, double-click the
    substation item in the tree control.

Note: Double-click any substation symbol in any diagram to open the
corresponding diagram. Alternately, right-click on any substation symbol
and choose **Substation>Open in Window** in the context menu.

### Advanced Options

The Open Diagram(s) dialog contains advanced options for automated
(batch) diagram processing.

![Advanced
Options](/images/PSSODMS_UserManual_2014-10-17114243_img_34.png)

-   The Rebuild saved diagrams option is used to auto-build all selected
    substation diagrams regardless of pre-existence.

-   The Reset diagram names option is used to rename saved diagrams
    consistent with the substation names in the model.

-   The Re-create measurement annotations option is used to
    automatically regenerate measurement annotation labels in the
    selected diagrams.

-   The Auto-save diagrams option is used to automatically save diagrams
    to the model immediately after being auto-built or updated upon
    opening.

-   The Auto-export diagrams option is used to batch-export selected
    diagrams to the graphical file format specified in the Export
    Diagrams dialog (launched when this option is checked).

-   The Close after saving option will automatically close each diagram
    immediately after it has been opened and saved or exported (when it
    is not desirable to have a large number of diagrams open at once).

## Worldview Diagrams

A Worldview diagram displays a selected set of substations with their
connecting branches. World-view diagrams can be arranged schematically
or geographically. Individual substations can be \"expanded\" within a
Worldview diagram to include their (pre-saved) detailed schematic
layouts; in

this way, it is possible to quickly convert an initial Worldview diagram
into a comprehensive and interactive Map Board-style diagram (a powerful
tool for system simulation/analysis).

![Example Worldview
Diagram](/images/PSSODMS_UserManual_2014-10-17114243_img_35.png)

### Building a Worldview Diagram

1.  Choose **Diagram>Open Diagram(s)** on the main menu (or use the
    corresponding File toolbar button) to launch the Open Diagram(s)
    dialog.

2.  Set the AutoBuild Type option to Worldview.

3.  Either select a single area item on the tree control or expand area
    tree control item(s) and select one or more substation items.
    Multiple substations may be selected by holding down the Ctrl key
    while clicking on the individual substation items.

    Note: If you select a single area item on the tree control, the
    Worldview diagram will be mapped to the corresponding SubControlArea
    for subsequent update/synchronization purposes. Only one Worldview
    diagram may be mapped to a given SubControlArea.

4.  Click the OK button in the Open Diagram(s) dialog to dismiss the
    dialog and open the newly built Worldview diagram.

5.  After making any adjustments to the diagram layout, save the diagram
    to the model by choosing **Diagram>Save Diagram** on the main menu.
    The resulting Save Diagram As dialog allows customizing the diagram
    name that will appear in the diagram window title bar and in the
    Open Diagram(s) dialog.

### Opening a Saved Worldview Diagram

1.  Choose **Diagram>Open Diagram(s)** on the main menu (or use the
    corresponding File toolbar button) to launch the Open Diagram(s)
    dialog.

2.  Expand the Worldview tree control item and select the diagram item
    to open.

3.  Click the OK button in the Open Diagram(s) dialog to dismiss the
    dialog and open the selected Worldview diagram.

    ![Saved Worldview
    Diagrams](/images/PSSODMS_UserManual_2014-10-17114243_img_36.png)

### Expanding and Collapsing Substations 

The saved schematic layouts for individual substations can be reused
within a Worldview diagram to add detail. This is done by \"expanding\"
an individual substation symbol. Correspondingly, an expanded substation
can be \"collapsed\" back to its original substation symbol.

### Build or open a Worldview diagram.

1.  Right-click on a substation symbol and choose **Substation>Expand**
    in the context menu:

    ![Expand Substation
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_37.png)

2.  The substation symbol will be replaced with a grouped set of
    graphical components corresponding to the saved substation diagram
    layout. The expanded substation components can be selected and moved
    as a group by clicking and dragging its dark gray background
    rectangle.

    Note: Except in certain special situations with advanced users,
    subsequently deleting the background rectangle or ungrouping the
    expanded substation components is not recommended.

    ![Expanded
    Substation](/images/PSSODMS_UserManual_2014-10-17114243_img_38.png)

3.  Repeat this process for the remaining individual substation symbols
    as desired.

4.  To collapse an expanded substation, right-click on its dark gray
    background rectangle and choose **Substation>Collapse** on the
    context menu:

    ![Collapse Substation
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_39.png)

It is intended for expanded substations to be repositioned relative to
each other, and for KneePoints to be inserted into connecting branches
and positioned as desired to achieve the best possible overall layout.
However, any adjustments to an internal substation layout should be
performed and saved within the individual substation diagram. The
expanded substation layout within the World-view diagram may then be
updated by right-clicking on the background rectangle and choosing
**Substation>Update** on the context menu. All expanded substations can
be updated at once by choosing **Diagram>Synchronize with Model** on the
main menu.

### Adding Substations to Existing Worldview diagram

1.  Switch to model maintenance mode by selecting Menu **Tool>Model
    Maintenance** .

2.  Open the worldview diagram in which substations need to be added.

3.  Select Menu **Diagram>Open**.

4.  In the Open Diagram(s) dialog, set the Auto Build Type to Worldview
    and enable "Add selected substations to the current Worldview or
    Planning diagram" checkbox.

    ![Adding substations to existing Worldview
    diagram.](/images/Opendiagram.png)

5.  Expand Network tree and select substations to be added to the
    worldview diagram (hold CTRL key to select multiple substations).

6.  Click **OK**. The selected substation should be added in the
    diagram.

    ![Worldview diagram before adding
    substations.](/images/WorldviewFlapco1.png)

    ![Substations EAST and SUB added to the worldview
    diagram.](/images/WorldviewFlapco2.png)

7.  Add Neighbors feature could also be used to add neighboring
    substations to the Worldview diagram. Right click on a substation
    and select **Substation-Add Neighbors** to add its neighbhor to the
    worldview diagram. All substations that are connected to the
    substation will be added to the diagram.

    ![Adding Neighboring substation to a worldview diagram. Right click
    on a substation and select Add
    Neighbors](/images/C7_AddNeighbors.png)

    ![Neighboring substation (HYDRO) is added to the
    diagram.](/images/C7_WorldviewFlapcoAddingNeighbors.png)

8.  Save the worldview diagram by Menu **Diagram>Save** (or
    **Diagram>Save As** to save as a different worldview diagram).

## Planning Diagrams

Planning diagrams are virtually identical to Worldview diagrams in terms
of construction and behavior. The key difference is that all expanded
substations within a Planning diagram are in bus-branch format as
opposed to bus-breaker format, having been built with the Bus-branch
AutoBuild Format option (refer to [Opening/Building Substation Diagrams
](#section_lfb_nwj_xp)).

![Saved Planning
Diagrams](/images/PSSODMS_UserManual_2014-10-17114243_img_40.png)

## Saving diagrams

Diagram layout including positioning of equipment and knee points could
be saved in the database by selecting Menu command **Diagram>Save**
(shortcut key **Ctrl+S**). A substation diagram with its layout saved is
indicated by a solid black diagram icon next the substation name in the
Open Diagram window (See [figure_title](#OpenDiagramWin)).

![Open Diagram window: Saved diagram will have a solid black substation
icon (e.g. substation EAST). Unsaved diagram will have gray substation
icon (e.g. substation
HYDRO)](/images/C7_saved_diagram_list.png){#OpenDiagramWin}

After changing the diagram layout or auto generating a diagram, the
diagram need to be saved (Menu command **Diagram>Save**) in order to
save the layout in the database. Diagrams not saved will have an
asterisk (\*) symbol next to the diagram name in the title bar of the
diagram window, refer to [figure_title](#UnsavedDiagram).

![Un-saved diagram: denoted by an asterisk (\*) symbol next to the
diagram name, SUB\*](/images/C7_unsaved_diagram.png){#UnsavedDiagram}

If an un-saved diagram is closed, a message box will prompt the user to
save the diagram, see [figure_title](#MsgBoxSave). Selecting **Yes**
will save the diagram with changes and selecting **No** will close
diagram without saving changes to the diagram.

![Message box confirming saving
diagram](/images/C7_save_diagram_msg_box.png){#MsgBoxSave}

Opening a previously saved diagram shows the saved equipment and their
layout. The equipment in a saved diagram may not correspond to equipment
in the model. For example, if a load added to a substation in CIMedit
after a substation diagram is saved, the saved diagram will still have
the added load. In order to update the diagram with equipment in the
model, choose the **Diagram>Synchronize** with Model command. This will
update diagram with the model and may add missing equipment or remove
deleted equipment. After updating diagram, the diagram need to be saved
so that the correct layout is loaded when the diagram is opened later.

## Diagram Options

The OneLine diagram editor is highly configurable in terms of appearance
and behavior. To view or adjust the options, select
***Diagram>Options*** from the main menu to launch the Diagram Options
dialog.

![Diagram Options
Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_41.png)

The Diagram Options dialog has the following tabbed pages:

-   General - contains settings that affect the navigational behavior
    and storage/retrieval performance for all diagrams

-   Default -contains default diagram settings

-   Current - contains settings that apply to the active diagram only

-   Symbols - contains symbol-specific settings, including settings that
    affect the appearance of default symbols as well as selecting to use
    custom symbol(s) for a particular equipment type

-   Voltage Levels - contains Voltage Level color mode settings

-   Lines/Bays -contains special Line and Bay color mode settings

-   Tooltips - contains graphical tooltip settings

## Viewing Editing Model data from Diagrams

Any equipment in a diagram can be located in CIMedit. To locate the
corresponding data of equipment in CIMedit, right click on the equipment
on the diagram and select **"Locate in CIMedit"** from the context Menu.

![Right click on equipment to bring up **"Locate in CIMedit"** and
**\"CIM Properties\"**](/images/C7_DiagramContextMenu.png)

CIM Properties window also gives a summary attributes of equipment. To
view CIM Properties of equipment, right click on the equipment and
select **\"CIM Properties\"**. Equipment attributes could be changed
either from CIMedit or from CIM Properties window.

![CIM Properties window](/images/C7_CIMProperties.png)

CIM Properties window shows properties of selected eqipment in the
diagram. If user selects a different equipment in the diagram, CIM
Properties window will display properties of the newly selected
equipment.

CIM Properties window is useful tool for viewing/editing equipment in a
diagram. However, CIMedit provides a comprehensive detail of the
equipment including association to other equipment/CIM classes.

***Note: After editing any parameters in CIM Properties window, user has
to press Enter key or click on another value/property field in order to
commit the change to the database. If different equipment is selected or
if the CIM Properties window is closed without committing the change,
the change will be not be lost.***

## Basic Editing Functions

This section describes how to use the OneLine editor interface to add,
reconnect and delete equipment in the model.

Note: The OneLine editor enforces CIM connectivity rules. Equipment with
Terminal-ConnectivityNode association(s) must be connected to an
existing BusbarSection or ConnectivityNode symbol (for branches, this is
sometimes abstracted to include Substations).

Note: Diagram editing may be restricted by various factors such as user
permissions, the current mode of operation, explicit diagram locking,
etc.

### Adding Equipment

The following examples illustrate how to add various types of equipment
to the model using the OneLine editor. Here are some important points to
keep in mind:

-   The Construction toolbar contains all of the available commands for
    setting the diagram interaction mode for adding new equipment.

-   The connection order when drawing 2-Terminal equipment effectively
    determines the \"primary\" and \"secondary\" Terminals in the model,
    which may affect results display and/or Measurement placement.

-   For Transformer equipment, the connection order additionally sets
    the default primary and secondary Windings.

-   When an equipment symbol is drawn, the equipment is immediately
    added into the model.

-   The Save/Save As commands are used to save the graphical diagram
    data only; they do not affect the network model.

-   Press the Esc key at any time to set diagram interaction back the
    default Select mode.

-   The commands for the addition of certain types of equipment are
    restricted depending on the diagram type. For example, switching
    equipment can not be added to a Planning or PlanningSub diagram and
    BusbarSections and ConnectivityNodes can only be added within a
    Substation or PlanningSub diagram.

### Adding a BusbarSection

A BusbarSection provides a point of connectivity for multiple other
equipment instances. This example illustrates how to create a new
BusbarSection.

When a new BusbarSection is created, the software automatically creates
its implied Terminal and ConnectivityNode in the model.

The TopologicalNode-ConnectivityNode association is not required for
basic equipment connectivity, but it is critical for other purposes
(such as Bus mapping and bus-branch diagram creation).

1.  Open a Substation diagram and click the BusbarSection (Horizontal)
    or BusbarSection (Vertical) command button on the Construction
    toolbar to set the diagram interaction mode.

    ![BusbarSection
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_42.png)

    ![New TopologicalNode
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_43.png)

2.  Right-click on one of the VoltageLevel items in the resulting Select
    TopologicalNode dialog and choose the New TopologicalNode command.

    ![New
    TopologicalNode](/images/PSSODMS_UserManual_2014-10-17114243_img_44.png)

    Note: If the desired VoltageLevel does not yet exist, it can be
    created here by right-clicking the Substation item and choosing the
    New VoltageLevel command.

3.  Enter a name for the TopologicalNode (typically the corresponding
    Planning Bus number) and click the OK button to dismiss the dialog.

    Note: You can alternately select an existing TopologicalNode for
    association with the new Busbar-Section. A TopologicalNode
    association is not required for basic connectivity, but is highly
    recommended.

4.  Position the cursor in the diagram where you want the BusbarSection
    symbol to appear and left-click the mouse.

    ![New
    BusbarSection](/images/PSSODMS_UserManual_2014-10-17114243_img_45.png)

5.  Click the Select command button on the Construction toolbar (or
    press the Esc key) to restore the default diagram interaction mode,
    enabling the new Busbar symbol to be selected, repositioned,
    resized, etc.

    ![Select
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_46.png)

6.  Choose the **Diagram>Save Diagram** command on the main menu to save
    changes to the diagram.

### Adding ConnectivityNodes

A ConnectivityNode also provides a point of connectivity for multiple
equipment instances. The process of adding ConnectivityNodes is very
similar to that of adding BusbarSections (refer to [Adding a
BusbarSection ](#section_nwc_nwj_xp)).

Note: ConnectivityNodes do not have their own Terminals, but are usually
linked to the Terminals of other equipment.

1.  Open a diagram and click the ConnectivityNode command button on the
    Construction toolbar to set the diagram interaction activity.

    ![ConnectivityNode
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_47.png)

2.  Select an existing TopologicalNode in the dialog (or create a new
    TopologicalNode as described in [Adding a BusbarSection
    ](#section_nwc_nwj_xp)).

    ![Selected
    TopologicalNode](/images/PSSODMS_UserManual_2014-10-17114243_img_48.png)

3.  Position the cursor in the diagram where you want the new
    ConnectivityNode to appear and left-click the mouse. Repeat for as
    many ConnectivityNodes as desired.

    ![New Connectivity
    Nodes](/images/PSSODMS_UserManual_2014-10-17114243_img_49.png)

4.  Click the Select command button on the Construction toolbar (or
    press the Esc key) to restore the default diagram interaction mode,
    enabling the new ConnectivityNode symbols to be selected,
    repositioned, etc.

5.  Choose the ***Diagram>Save Diagram*** command on the main menu to
    save changes to the diagram.

### Adding a Breaker

This example illustrates how to create a new Breaker between an existing
BusbarSection and ConnectivityNode. The same basic process applies to
other switch types and 2-Terminal equipment

types in general. Open a diagram and click the Breaker command button on
the Construction toolbar to set the diagram interaction mode.

![Breaker
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_50.png)

1.  Select a Bay association on the resulting dialog (optional).

2.  Position the cursor along the BusbarSection symbol until an empty
    connection port becomes visible.

    ![\"From\"
    Connection](/images/PSSODMS_UserManual_2014-10-17114243_img_51.png)

3.  Left-click on the connection port drag the cursor over the
    ConnectivityNode until its connection port becomes visible.

    ![\"To\"
    Connection](/images/PSSODMS_UserManual_2014-10-17114243_img_52.png)

4.  Release the mouse and the new Breaker will appear between the
    selected connection ports.

    ![New
    Breaker](/images/PSSODMS_UserManual_2014-10-17114243_img_53.png)

5.  Repeat steps 3-6 for as many Breakers as desired, then Click the
    Select command button on the Construction toolbar (or press the Esc
    key) to restore the default diagram interaction mode.

6.  Choose the ***Diagram>Save Diagram*** command on the main menu to
    save changes to the diagram.

### Inserting Breakers/Switches

This example illustrates how to insert a new Breaker between existing
2-Terminal equipment (including another Breaker/Switch) and the
connected BusbarSection or ConnectivityNode at one end. The same process
applies to other switch types also.

1.  Open a diagram and click the Breaker command button on the
    Construction toolbar to set the diagram interaction mode.

2.  Select a Bay association on the resulting dialog (optional).

3.  Click the Insert Breaker/Switch command button on the Construction
    toolbar to set the additional diagram interaction mode to \"Insert
    Breaker.\"

    ![Insert Breaker/Switch
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_54.png)

4.  Position the cursor roughly near the mid-point of a link at one end
    of an existing branch symbol. The cursor should snap to the link.

    ![Preparing to
    Insert](/images/PSSODMS_UserManual_2014-10-17114243_img_55.png)

5.  Left-click the mouse and the new Breaker will appear between the
    branch and the Busbar Section/Connectivity Node to which it was
    previously connected.

    ![Inserted
    Breaker](/images/PSSODMS_UserManual_2014-10-17114243_img_56.png)

6.  Repeat steps 4-5 to insert as many new Breakers as desired, then
    Click the Select command button on the Construction toolbar (or
    press the Esc key) to restore the default diagram interaction mode.

7.  Choose the **Diagram>Save Diagram** command on the main menu to save
    changes to the diagram.

### Adding an EnergyConsumer

This example illustrates how to add a new EnergyConsumer (load). The
same basic process applies to all single-Terminal (radial) equipment.

1.  Open a diagram and click the EnergyConsumer command button on the
    Construction toolbar to set the diagram interaction mode.

    ![EnergyConsumer
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_57.png)

2.  Select an EnergyConsumer type on the resulting dialog.

    ![EnergyConsumer Type](/images/C7_EnergyConsumerType.png)

3.  Position the cursor along a BusbarSection symbol (or on a
    ConnectivityNode symbol) until an empty connection port becomes
    visible and left-click to add the EnergyConsumer.

    ![New
    EnergyConsumer](/images/PSSODMS_UserManual_2014-10-17114243_img_58.png)

4.  Click the Select command button on the Construction toolbar (or
    press the Esc key) to restore the default diagram interaction mode.

5.  Choose the ***Diagram>Save Diagram*** command on the main menu to
    save changes to the diagram.

### Adding a 3-Winding Transformer

This example illustrates how to create a 3-Winding Transformer by adding
a third Winding to an existing (2-Winding) Transformer.

1.  Open a diagram containing a Transformer and click the Third Winding
    command button on the Construction toolbar to set the diagram
    interaction mode.

    ![Third Winding
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_59.png)

2.  Position the cursor over the Transformer symbol until an open
    connection port becomes visible. Left-click on the connection port
    and begin dragging the mouse to a BusbarSection or ConnectivityNode.
    Release the left mouse button when the cursor is positioned over an
    open connection port on the BusbarSection or ConnectivityNode.

    ![Adding a Third
    Winding](/images/PSSODMS_UserManual_2014-10-17114243_img_60.png)

3.  The original Transformer symbol will change to a 3-Winding
    Transformer symbol, with a third link representing the new Winding.

4.  Click the Select command button on the Construction toolbar (or
    press the Esc key) to restore the default diagram interaction mode.
    Reposition the 3-Winding Transformer symbol as desired.

    ![3-Winding
    Transformer](/images/PSSODMS_UserManual_2014-10-17114243_img_61.png)

5.  Choose the ***Diagram>Save Diagram*** command on the main menu to
    save changes to the diagram.

### Adding an ACLineSegment

ACLineSegments are 2-Terminal equipment and may be created similarly to
the \"Adding a Breaker\" example above. However, since an ACLineSegment
typically spans two different Substations, this example illustrates how
to create a new ACLineSegment using two Substation diagrams that are
open at once.

Note: A substation-spanning ACLineSegment (or other 2-Terminal
equipment) may be more easily created using a Worldview or Planning
diagram that includes the \"expanded\" layout detail for both
substations (refer to [Substation Diagrams](#section_fbb_nwj_xp)).

1.  Open both Substation diagrams and arrange the diagram windows so
    that both are visible within the main application window.

    ![Diagram
    Windows](/images/PSSODMS_UserManual_2014-10-17114243_img_62.png)

2.  Click the ***ACLineSegment*** command button on the Construction
    toolbar to set the diagram interaction mode.

    ![ACLineSegment
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_63.png)

3.  Select a Line association on the resulting dialog (optional).

4.  Position the cursor over a BusbarSection or ConnectivityNode on the
    first diagram until an open connection port becomes visible. Begin
    dragging the mouse until the cursor is inside the second diagram
    window.

    ![Dragging Across
    Substations](/images/PSSODMS_UserManual_2014-10-17114243_img_64.png)

5.  When the second diagram window becomes activated, release the mouse
    and left-click on a BusbarSection or ConnectivityNode symbol to
    select it and finalize the connection (the link can be moved to the
    exact desired connection port afterwards). Both diagrams will then
    automatically be updated to show the new ACLineSegment connected to
    the opposite substation symbol.

    ![New
    ACLineSegment](/images/PSSODMS_UserManual_2014-10-17114243_img_65.png)

6.  Choose the **Diagram>Save All** command on the main menu to save
    changes to both diagrams.

### Adding a MutualCoupling

This example illustrates how to add a mutual coupling between two
ACLineSegments.

Note: A MutualCoupling may be added using a Substation, a Worldview, or
a Planning diagram.

1.  Open a Substation diagram that has ACLineSegments.

2.  Select two ACLineSegments for which a MutualCoupling needs to be
    added.

3.  Click the **MutualCoupling** command button on the Construction
    toolbar.

    ![MutualCoupling command
    button](/images/PSSODMS_UserManual_2014-10-17114243_img_66.png)

4.  Click on the diagram to place the Mutual Coupling. Use the dialog
    box that appears to specify terminals and distance data of the
    Mutual Coupling. The MutualCoupling placed in the Substation diagram
    is shown in:

![New Mutual Coupling
parameters](/images/PSSODMS_UserManual_2014-10-17114243_img_67.png)

![Mutual Coupling placed in the Substation
diagram](/images/PSSODMS_UserManual_2014-10-17114243_img_68.png)

### Adding an HVDC Link

An HVDC link is modeled as a single DCLineSegment with a
RectifierInverter at each end. This example illustrates how to add an
HVDC link between two Substation diagrams.

1.  Open the diagram for each substation to which you are adding an HVDC
    link. Add BusbarSections and/or ConnectivityNodes as needed for the
    HVDC line.

    ![Substations for HVDC
    link](/images/PSSODMS_UserManual_2014-10-17114243_img_69.png)

2.  Click the DCLine command button on the Construction toolbar.

    ![DCLine command
    button](/images/PSSODMS_UserManual_2014-10-17114243_img_72.png)

3.  Select type of DCLine (CsConverter or VsConverter).

    ![DCLine command button](/images/C7_DCLineType.png)

4.  The procedure to add a DCLine is similar to the procedure of adding
    an ACLineSegment described in [Adding an ACLineSegment
    ](#section_hwd_nwj_xp). Connect the DCLineSegment between the two
    busbar sections (or connectivity nodes). PSS®ODMS will automatically
    create the necessary DCNode and DCConverterUnit instances at each
    end. The resulting DCLineSegment is shown below.

    ![DCLineSegment connected to
    RectifierInverters](/images/PSSODMS_UserManual_2014-10-17114243_img_73.png)

### Adding a Measurement

This example illustrates how to add a new Measurement to equipment.

1.  Open a diagram. In Select mode, right-click on an equipment symbol
    and choose the ***Measurement>New Measurement*** command.

    Note: Or right-click on an existing Measurement symbol to pre-select
    the same equipment Terminal for the new measurement.

    ![New Measurement
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_74.png)

2.  Fill in the attributes on the resulting New Measurement dialog.

    Note: Most of these attributes can be changed later using NTE or the
    CIM Properties window.

    ![New Measurement
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_75.png)

3.  Click **OK** to dismiss the dialog and add the measurement to the
    network model. A measurement symbol should be visible at the
    selected equipment.

    Note: If the measurement symbol is not immediately visible, verify
    that the **View>Measurements** command on the main menu is checked,
    then try the **View>Refresh** command.

    ![(Status) Measurement
    Symbol](/images/PSSODMS_UserManual_2014-10-17114243_img_76.png)

### Deleting Equipment

This example describes how to delete equipment from the network model.

1.  Open a diagram. In Select mode, right-click on an equipment symbol
    and choose the **Delete** command. (or select the symbol and click
    the **Del** key).

    ![Delete
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_77.png)

2.  Click **Yes** on the resulting message box prompt to delete the
    selected equipment from the model.

    Note:

    **Yes:** Deletes the equipment from the model. Deleting equipment
    from the model cannot be undone as the equipment is deleted from the
    diagram as well as from the model.

    **No:** Deletes the graphical symbol only. The equipment still
    exists in the model. Re-synchronizing the diagram with the model (by
    clicking **Menu Diagram>Synchronize with Model**) would add the
    graphical symbol back to the diagram.

    **Cancel:** Cancels the operation.

3.  Choose the **Diagram>Save Diagram** command on the main menu to save
    changes to the diagram.

Note: You can select multiple equipment items to delete.

Note: Deleting equipment also deletes all associated Terminals,
Measurements, Curve Schedules, etc.

Note: A BusbarSection or ConnectivityNode with existing connections to
other equipment can not be deleted.

### Reconnecting Equipment

This example illustrates how to reconnect an EnergyConsumer from a
BusbarSection to a ConnectivityNode. In general, any equipment may be
reconnected to a different BusbarSection or ConnectivityNode within the
same VoltageLevel.

1.  Left-click on a symbol link; the connection port on the
    BusbarSection or ConnectivityNode will become visible.

    ![Selecting a
    Link](/images/PSSODMS_UserManual_2014-10-17114243_img_78.png)

2.  Left-click on the visible connection port and drag the link away
    from the BusbarSection to the ConnectivityNode.

    ![Dragging the
    Link](/images/PSSODMS_UserManual_2014-10-17114243_img_79.png)

3.  Release the mouse to finalize the reconnection.

    ![Relink
    Complete](/images/PSSODMS_UserManual_2014-10-17114243_img_80.png)

### Importing/Exporting an Image File

Image files can be imported into any diagram. Once imported, an image
becomes an interactive graphical component and can be repositioned,
scaled, assigned to a different layer, etc.

Note: Before importing an image file, make sure it is located in the
image file directory specified in the Diagram Options dialog (General
page). When opening a saved diagram that contains an image file
reference, the program will only be able to reload the image if the file
is located in this directory.

To import an image file into the current diagram:

1.  Choose the **Edit>Import Image** command from the main menu.

    ![Import Image
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_81.png)

2.  Select the image file to import from the file selection dialog.

    Note: Supported image file formats include JPEG (.png), Bitmap
    (.bmp), GIF (.png), PNG (.png), TIFF (.tif), and Icon (.ico).

    ![Imported
    Image](/images/PSSODMS_UserManual_2014-10-17114243_img_82.png)

    Note: Image components are initially assigned to Layer 0 (the
    background layer).

    Note: Any number of image files may be imported into a given
    diagram.

3.  Choose the ***Diagram>Save*** Diagram command on the main menu to
    save changes to the diagram.

In contrast, diagram can be exported into image file, by choosing the
**View>Export Image** command from the main menu. Note: Supported image
file formats include JPEG (.png), Bitmap (.bmp), GIF (.png), PNG (.png),
and TIFF (.tif).

### Layers

Each graphical component is assigned to a Layer which determines
rendering order. Components on lower layers are rendered before
components on higher layers, making components on higher layers appear
\"on top\" and components on lower layers appear \"on bottom\" Layers
are managed via a dialog which is launched by choosing the
**Diagram>Layers** command on the main menu. Components can be
reassigned to different layers via context menu command or the Graphical
Component Properties dialog. Layers are diagram-specific and are saved
with the diagram.

### Groups

A Group is a mechanism for associating multiple graphical components
together such that when one component in the Group is selected, all
other components within the same Group are also selected. This can be
useful for moving components all at once. Groups are managed via a
dialog which is launched by choosing the **Diagram>Groups** command on
the main menu. Components can be grouped or ungrouped via context menu
commands or the Graphical Component Properties dialog. Groups are
diagram-specific and are saved with the diagram.

### Saved Views

A Saved View is a mechanism for preserving a specific zoom level and
center position. Saved Views are managed via a dialog which is launched
by choosing **View>Saved Views** command on the main menu. Saved Views
are diagram-specific and are saved with the diagram.

## Diagram Locking

Lock diagram function allows user to lock diagrams from editing so that
user does not accidentally change the diagram layout while navigating in
the diagram. Diagrams could be locked when the diagram layouts are
finalized and no immediate changes in the layout are required. A locked
diagram could be unlocked if user needs to update its layout.

### Mode-Independent Locking

Diagram could be locked with following steps:

1.  If necessary, switch to model maintenance mode by clicking **Tools>
    Model Maintenance.**

2.  Open a diagram which needs to be locked from editing.

3.  The diagram could be locked by clicking **Menu Edit> Lock Diagram.**

4.  Once it is selected, the diagram title indicates the locked status.
    In addition, **Diagram locked** text appears in the status bar which
    can be seen in the figure below indicating that user cannot change
    the layout of the diagram. Only diagram editing feature is locked
    for the diagram and user could still navigate, zoom or pan in the
    diagram.

    Note: A locked diagram could be unlocked by clicking **Menu
    Edit>Unlock Diagram.**

![Locked diagram indicator in the Diagram title and the Status
Bar.](/images/C7_DiagramLockedStatusBar.png)

### Mode-Dependent Locking

Diagrams could also be locked in network analysis mode only. In network
analysis mode, a lot of interactions occur with diagrams. In order to
prevent unwanted or accidental diagram changes in network analysis mode,
lock diagram feature can be enabled from Display Settings.

1.  Select display options by clicking on **Analysis>Display settings.**

    ![Lock diagram editing capability (only in Network Analysis
    Mode).](/images/C7_net analysis_lock diagram1.png)

2.  In **General** tab of the Display Settings window, enable **"Lock
    diagram editing capability"** checkbox and then click on **Apply**.
    This locks all the diagrams in the Network Analysis mode. Only
    diagram editing feature is locked and user could still navigate,
    zoom or pan in diagrams.

    Note: User can switch to Model Maintenance mode and change the
    diagram layout if necessary.

## Default System Overview Diagram

System Overview toolbox button provides a shortcut for opening a pre
assigned diagram (normally a world view or a planning diagram). Clicking
on the System Overview toolbox button opens up the pre assigned diagram.

![System Overview button. Shortcut for opening the default
diagram](/images/C7_SystemOverviewButton.png)

The diagram for System Overview shortcut could be set from Diagram
Options.

1.  Choose **Menu Diagram>Options** to open Diagram Options window.

2.  In **General** tab of the Diagram Options window, click on browse
    button next to the **"System Overview map".**

3.  Select a desired diagram (worldview or planning diagram preferred)
    from the Select Diagram window to assign the diagram for System
    Overview shortcut. Click **OK** to confirm selection.

4.  The name of the selected diagram will show in the System Overview
    map textbox (Mapboard in the figure). Clicking on the System
    Overview toolbox button will open this diagram.

    ![System Overview diagram (Diagram opened by clicking on the System
    Overview button).](/images/C7_SystemOverview.png)

## Custom Symbols

Custom symbols may be created and used in place of the default symbols
provided by the application. Custom symbols can be comprised of
\"primitive\" graphical shapes and/or imported /images. This example
illustrates how to create a circular symbol to use in place of the
default Breaker symbol. The same basic process applies to all custom
symbols.

Note: Custom Node symbols can be used to replace the default
ConnectivityNode symbol. Custom Branch symbols assume two connection
ports (to be used for 2-Terminal equipment types including all switch
types). Custom Radial symbols assume one connection port (to be used for
1-Terminal equipment types). Custom Generic symbols are generally used
for additional diagram annotation or navigational purposes.

1.  Choose the ***Diagram>Custom Symbol>New Branch Symbol*** command
    from the main menu to open the symbol editor window.

    ![New Branch Symbol
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_83.png)

    Note: The zoom level in the symbol editor window is initially set at
    to 500% to accommodate the required level of detail for designing a
    custom symbol.

2.  Click the **Circle** command button on the Construction toolbar to
    set the diagram interaction mode.

    ![Circle
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_84.png)

3.  Left-click, drag a box, and release the mouse to draw a circle.

    ![New Circle](/images/PSSODMS_UserManual_2014-10-17114243_img_85.png)

4.  Click the **Connection Port command** button on the Construction
    toolbar to set the diagram interaction mode.

    Note: In Select mode, double-click on any primitive shape component
    to customize its graphical attributes such as color, fill,
    thickness, etc.

    ![Connection Port
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_86.png)

5.  Left-click on the left and right sides of the circle to add the two
    required connection ports for a Branch symbol.

    ![New Connection
    Ports](/images/PSSODMS_UserManual_2014-10-17114243_img_87.png)

6.  Click the **Label** command button on the Construction toolbar to
    set the diagram interaction mode.

    ![Label
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_88.png)

7.  Position the cursor near the symbol and left-click to add a new
    Label.

    ![New Label](/images/PSSODMS_UserManual_2014-10-17114243_img_89.png)

    Note: An equipment symbol must have at least one Label position to
    be used when displaying the equipment name on the diagram.

8.  After completing all customizations, choose the **Symbol>Save**
    command on the main menu to save the custom symbol.

    ![Save
    Command](/images/PSSODMS_UserManual_2014-10-17114243_img_90.png)

9.  Enter a description for the symbol in the Description box in the
    dialog. Click the OK button when finished.

    ![Save Custom Symbol
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_91.png)

10. Close the symbol editor window.

11. Choose the ***Diagram>Diagram Options*** command on the main menu to
    launch the Diagram Options dialog, activate the Symbols page and
    select the Breaker equipment type.

    ![Diagram Options
    -Symbols](/images/PSSODMS_UserManual_2014-10-17114243_img_92.png)

12. Check the Use custom symbol option and select the custom symbol(s)
    by description.

    ![Custom Symbol
    Association](/images/PSSODMS_UserManual_2014-10-17114243_img_93.png)

    Note: For switch types, you can create and associate two separate
    custom symbols: one for the \"closed\" state and another for the
    \"open\" state.

13. Click **OK** when finished to set the association and dismiss the
    dialog.

14. Open a diagram containing Breakers. If necessary, use the
    **Diagram>Reset**Symbols command to convert all of the default
    breaker symbols to the selected custom symbol. Save and close the
    diagram.

    ![Diagram with Custom
    Symbols](/images/PSSODMS_UserManual_2014-10-17114243_img_94.png)

## Graphical Component Properties

To view the properties of any graphical component in a diagram,
right-click on the component and choose the Graphical Properties command
on the context menu. The table below describes some key editable
graphical properties.

  -----------------------------------------------------------------------
  Field Name             Description
  ---------------------- ------------------------------------------------
  Layer                  The layer to which the component is currently
                         assigned

  Group                  The group to which the component is currently
                         assigned

  Owner                  The owner of the component

  ID                     The graphical component ID

  Map                    Map string (generally an ODMS ID).

  Color                  The foreground/outline color of the component

  Selectable             Allows the component to be selected

  Movable                Allows the component to be repositioned

  Rotatable              Allows the component to be rotated

  AutoPosition           Enables/disables automatic positioning behavior

  AutoRotate             Enables/disables automatic rotation behavior

  Hidden                 Allows the component to be hidden

  Position X             The x-coordinate of the center point of the
                         component

  Position Y             The y-coordinate of the center point of the
                         component

  Rotation               The degrees of rotation of the component
  -----------------------------------------------------------------------

  : Graphical Component Properties

## Importing and Exporting Diagrams

Diagrams can be exported to the following file formats:

-   PSS®ODMS Slider (.sld)

-   PSS®E Slider (.sld) (bus-branch diagrams only)

-   CIM/XML Diagram (.xml) (requires Python)

-   AutoCad (.dxf)

-   Siemens Spectrum Graphics (.gml)

-   SNC Graphics (.dat)

-   Google Earth (.kml)

To export the currently open diagram, use the **Diagram>Export command**
on the main menu. To export multiple diagrams at once, use the special
\"Auto-export\" option on the Open Diagram(s) dialog.

Diagrams can be imported from PSS®ODMS binary (.sld) files via the
**Diagram>Import** Diagrams command. Use the \"Remap based on CIM
URI's\" option if the corresponding portion of the model has been
subsequently reimported or replaced via the Model Merge function (to
reset ODMS ID mappings which have become invalid).

The import/export diagram capability can also be extended by writing
custom Python scripts using the provided sliderPy interface to support
any graphical format.
