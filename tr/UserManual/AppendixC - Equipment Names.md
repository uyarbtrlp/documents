# Equipment Names

# Introduction

To facilitate network model data integration between PSS®E and other
systems which require additional equipment names which the PSS®E RAW
file format does not support, PSS®ODMS provides two functions that make
use of the standard CIM naming attributes. The complete set of equipment
Names and Descriptions can be imported into and exported from PSS®ODMS
in a special CSV-based format which uses standard PSS®E identifiers and
has a similar basic structure to the PSS®E RAW file.

# Editing Equipment Names

Default equipment names may be created by import functions such as the
PSS®E model import function. The CIMedit interface can be used to edit
the Name and Description fields of individual equipment instances.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_193.png)

# Exporting Equipment Names

Use the command below to export equipment names to the specified .nam
file.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_194.png)

The exported .nam file can be viewed and/or edited in any text editor.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_195.png)

The .nam file is similar to the PSS®E RAW file and uses the same PSS®E
bus-based identifiers. It contains the following sections:

-   Buses - TopologicalNode names

-   Loads -EnergyConsumer names

-   Fixed Shunts -ShuntCompensator names

-   Generators - GeneratingUnit names

-   Branches - ACLineSegment names

-   Transformers - PowerTransformer names

-   Two-Terminal DC Lines -DCLineSegment names

-   FACTS - FACTS names

-   SwitchedShunts - ShuntCompensator names

# Importing Equipment Names

An edited or newly-created .nam file can be imported using the command
below; this will update the corresponding equipment name fields in the
current PSS®ODMS model. Note that consistent PSS®E identifiers
(including TopologicalNode-mapped bus numbers and 2-character equipment
ID's) in the PSS®ODMS model are required.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_196.png)
