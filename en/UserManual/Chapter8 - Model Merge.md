# Model Merge

## Introduction

PSS®ODMS provides an interactive feature to merge two separate CIM10 or
CIM12 models into one. For CIM14 or higher version models, merging can
be accomplished via the Import Partial CIM/XML function. Model Merge
includes the ability to merge entire models together or to merge only
selected substations from one model into another. An important
consideration is that the merged model will initially have duplicate
and/or isolated tie lines. To insure data integrity, PSS®ODMS provides
convenient features to help resolve tie line connectivity subsequent to
the automated merge process.

## Model Merge Procedure

To merge two models:

Choose the ***Model>Operations>Merge Models*** command from the main
menu.

![Merge Models
Command](/images/PSSODMS_UserManual_2014-10-17114243_img_96.png)

1.  The Model Merge dialog window will appear. By default, the Base
    Model is the current database model that is open in PSS®ODMS. Click
    the **Select Model** button under the External Model heading to
    select the model to merge with the Base Model.

    ![Selecting an External
    Model](/images/PSSODMS_UserManual_2014-10-17114243_img_97.png)

2.  Expand the External Model and Base Model tree controls to select
    companies or substations from the External Model that you want to
    merge into the Base Model. Drag the selected items from External
    Model and drop them onto Base Model. The selected items be marked
    with a red 'X' in External Model and a green 'check' in Base Model
    (to indicate that they are marked to be merged from the External
    Model into the Base Model).

    ![Select From External
    Model](/images/PSSODMS_UserManual_2014-10-17114243_img_98.png)

3.  Right-click on items in Base Model that you do not want to include
    in the merged model and choose the ***Replace*** command on the
    resulting context menu. The selected items will be marked with a red
    'X' to indicate that they are to be excluded from the merged model.

    ![Selecting Areas to
    Replace](/images/PSSODMS_UserManual_2014-10-17114243_img_99.png)

    Note: You can change your selections by right-clicking on marked
    items and choosing the appropriate context menu command.

4.  If necessary, change the name of the Target Model. This will be the
    merged model, so it should be set to a unique name within the
    database.

    ![Target (Merged) Model
    Name](/images/PSSODMS_UserManual_2014-10-17114243_img_100.png)

5.  When your selections are complete, click the **Merge** button to
    begin the Merge process.

6.  After the automated merge process completes, PSS®ODMS should
    automatically connect to the new, merged model. The Tie Line
    Resolution dialog can be displayed by choosing the
    Model>Operations>Tie Line Resolution command on the main menu. This
    screen displays all the tie lines with unresolved connections. For
    example, there may be tie lines leaving a substation in the merged
    model with no defined destination because the original destination
    substation has been excluded from the merged model.

    The Model Merge process creates a fictitious substation (named
    \"AAATieLine\") to provide temporary connectivity for all these
    \"orphaned\" tie lines. So the Tie Line Resolution dialog displays
    all the tie lines entering and exiting the \"AAATieLine\"
    substation.

    ![Tie Line Resolution
    Dialog](/images/PSSODMS_UserManual_2014-10-17114243_img_101.png)

    Note: For convenience, the Tie Line Resolution dialog can be closed
    and reopened as needed subsequent to a merge.

7.  The tie lines that could not be matched appear in the lower left and
    right panes of the screen. Select the External tie lines and the
    Base tie lines that match and click the Add button to indicate that
    the two lines are in fact the same and should be consolidated.

    Note: Some tie lines may not match; it is up to the user to
    determine which ones should be kept. If an incorrect match is added,
    PSS®ODMS prompts the user that the tie lines do not appear to be
    related. If OK is selected by mistake, then the user will need to
    re-select the added line and select the Remove button.

8.  Once all tie lines have been resolved, click the OK button to accept
    the selections, close the window and proceed with the Merge process.

9.  A progress indicator is displayed until the tie line resolution
    process is complete.

10. Upon completion of the tie line resolution process, click OK.

If any tie lines cannot be resolved based on the input provided, they
are listed in a log file that is generated during the merge. This file
is displayed immediately following the process completion and may be
reviewed later using Notepad (or any other text editor).

![Tie Line Resolution
Log](/images/PSSODMS_UserManual_2014-10-17114243_img_102.png)

Alternately, tie line connectivity may be resolved using the OneLine
graphical editor, as described in the next section.

### Graphically Reconnecting Tie Lines

The Model Merge function does not make heuristic assumptions about how
to reconnect affected tie lines. Instead, it creates a fictitious
Substation (and related model hierarchy) named \"AAA-TieLine\" to
temporarily connect the ends of the \"unresolved\" ties. To resolve tie
line connectivity graphically, first auto-build and arrange the
\"AAATieLine\" substation diagram.

![Build AAATieLine
Diagram](/images/PSSODMS_UserManual_2014-10-17114243_img_103.png)

![Example AAATieLine
Diagram](/images/PSSODMS_UserManual_2014-10-17114243_img_104.png)

For each line temporarily connecting into the AAATieLine substation,
open the substation diagram where that end of the line should be
connected and reconnect it graphically by selecting and dragging it from
its ConnectivityNode within AAATieLine to a
BusbarSection/ConnectivityNode in the other substation.

Note: For detailed instructions on connecting branch equipment between
substations, refer to [???](#chapter_ll1_nwj_xp).

Repeat this process until there are no longer any lines connecting into
AAATieLine, at which point the AAATieLine SubControlArea can be deleted
from the model, effectively deleting the related Substation,
VoltageLevel and ConnectivityNode instances.
