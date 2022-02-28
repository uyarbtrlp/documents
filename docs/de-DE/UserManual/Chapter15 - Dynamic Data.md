# PSS®E Dynamics Data Modeling

## Overview

As an alternative to detailed CGMES Dynamics profile-based modeling,
Dynamics data in PSS®E DYR format associated with individual equipment
instances can be managed generically in PSS®ODMS. Using CIMedit,
right-click on any GeneratingUnit or EnergyConsumer item to add a new
Dynamic Model. When prompted, select any dynamics data file (such as a
PSS®E DYR file) you would like to associate with the equipment item.
Note: multiple Dynamic Models can be added to the same equipment
instance and the same dynamics data file can be associated with
different equipment instances.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_178.png)

![](/images/PSSODMS_UserManual_2014-10-17114243_img_178_1.png)

Once the Dynamic Model has been added to the PSS®ODMS database, CIMedit
provides commands to view (in the user\'s default text editor), update
and export its associated data. As with all other data in PSS®ODMS,
Dynamic Model data is shared by all users connected to the same
data-base model. PSS®ODMS remembers the original dynamics data file name
for viewing and exporting purposes.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_179.png)

For convenience, a new command is provided to export all dynamics data
at once into the selected directory, using the stored file name of each
Dynamic Model. A message box displays if user want to export from CIM
data tables, select \"No\" to export from the text based dyr Data from
multiple Dynamic Models in a model are automatically aggregates to a
single dyr file by the export function.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_180.png)

![](/images/PSSODMS_UserManual_2014-10-17114243_img_180_1.png)
