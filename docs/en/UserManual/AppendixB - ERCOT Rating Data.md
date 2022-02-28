# ERCOT Rating Data

# Introduction

The Electric Reliability Council of Texas (ERCOT) publishes a redacted
version of its model in CIM/XML format to its utility members. Although
redacted to exclude other data, this model contains custom extensions
for rating data which is organized by weather zones and temperatures.
These data extensions are supported in the CIM/XML import functions
(full model and incremental), Compare Models feature, CIMedit interface
and Build Case function. A case built with ERCOT rating data can be
subsequently exported to PSS®E RAW format.

# Viewing/Editing ERCOT Rating Data

After importing a redacted ERCOT CIM/XML model, open CIMedit and
navigate to any ACLineSegment. Expand its OwnerShareRating item and
RatingLimitSet item, respectively. Observe the individual Rating
instances associated with different temperature points. Expand any
Rating item to view its associated AnalogLimit instances. This data is
all editable in CIMedit.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_187.png)

# Selecting Temperature Sets

In order to apply the desired rating data to a case build/PSS®E export,
it is first necessary to verify and/or adjust the special WeatherZone
temperature extended attribute of the corresponding
Sub-GeographicalRegion. The Weather Zone temperature values can be
edited directly in CIMedit as needed prior to case builds.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_188.png)

# Building a Case

The ability to map the ERCOT rating data to a case is integrated into
the Build Case function. When an ERCOT model is open, PSS®ODMS
recognizes it and displays a customized Limits page in the Build Case
wizard dialog. Simply set the Rating type and RATEC mapping options as
desired along with the other case build options.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_189.png)

Additionally, for consistency with the ERCOT Topology Processor, some
special options are available on the second (Options) page of the Build
Case wizard.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_190.png)

-   ZBR override PSS®E ID - allows designated switching devices to
    bypass the standard zero-impedance branch logic (which affects the
    resulting topological configuration of the case)

-   Line reduction PSS®E ID - allows designated SeriesCompensators and
    Equivalent-Branches to be excluded from Multi-section Lines

After the case is built, the mapped rating data can be verified in the
Network spreadsheet view(s) and Device Settings dialog. The same MVA
limit values will be included in any subsequent export of the case to
PSS®E RAW format.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_191.png)
