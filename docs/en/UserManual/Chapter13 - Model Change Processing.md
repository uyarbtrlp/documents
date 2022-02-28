# Model Change Processing

## Compare CIM Models

The Compare CIM Models function of PSS®ODMS automates model change
processing and synchronization by comparing two complete CIM models and
extracting the differences between the two models (i.e. the changes)
into an incremental CIM/XML file which can then be used as needed (for
example, published to an external system or organization or applied
directly to the current PSS®ODMS model), thus eliminating duplication of
manual effort and its implied risks and inefficiencies.

### Example Use Case 1

This simple use case (reflected in the above diagram) assumes that
PSS®ODMS is only being used to create incremental CIM/XML files for data
exchange among different systems or organizations.

1.  The current full network model is exported from the source system in
    CIM/XML format.

2.  After model changes are made in the source system, an updated full
    CIM/XML model is exported.

3.  The Compare CIM Models function is used to extract the differences
    between the updated and original CIM/XML files into an incremental
    CIM/XML file.

4.  The resulting incremental CIM/XML file is then published to the
    appropriate parties.

With some scripting, this process can be automated within an integrated
solution.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_165.png)

### Example Use Case 2

This slightly more complex use case assumes that PSS®ODMS is being used
for network model analysis and export to PSS®E.

1.  The original full CIM/XML model is imported into PSS®ODMS.

2.  After model changes are made in the source system (e.g. EMS), an
    updated full CIM/XML model is exported.

3.  The Compare CIM Models function is used to extract and apply the
    changes to the current PSS®ODMS model.

4.  The updated PSS®ODMS model is validated, solved and exported to
    PSS®E.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_166.png)

### Assumptions and Restrictions

URI\'s must be consistent between the two models being compared. The
model comparison is comprehensive and exact; equipment that is manually
added in PSS®ODMS instead of the source system (contrary to the implied
business process) will be treated as a delete event by the next model
comparison. Similarly, if an originally null CIM field is manually set
to a non-null value in PSS®ODMS but remains null in the updated CIM/XML
model, then it will revert back to null in PSS®ODMS when applying the
changes. However, PTI or user-defined schema extensions (such as
PSS®E-specific identifier fields) are disregarded by the model
comparison process and thus the values of these fields are always
preserved in the PSS®ODMS model when applying changes.

### Compare CIM Models Walkthrough

The Compare Models menu command is shown below.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_167.png)

Fill in the desired options in the resulting dialog and click the OK
button to extract the incremental CIM/XML file and (optionally) apply
the changes to the current PSS®ODMS model.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_168.png)

If the import option was selected, then the applied changes should now
be visible in the PSS®ODMS interface.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_169.png)

The incremental CIM/XML file is saved in the user-selected directory.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_170.png)

A detailed log file is saved in the PSS®ODMS log directory for
validation and troubleshooting purposes.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_171.png)

## Compare PSS®E Models

The Compare PSS®E Models function of PSS®ODMS is used to extract
relevant differences between two sets of PSS®E RAW and SEQ files into a
PSS®E format-based incremental "project" file, using Menu Command
***Model>Operation>Compare PSS®E models***. The project file can then be
imported directly into PSS®ODMS using the "Import PSS®E Project"
function.

## Import PSS®E Project

The Import PSS®E Project function is used to import a PSS®E project file
into the current PSS®ODMS model, using Menu Command
***Model>Import>PSS®E Project***. The model changes contained in the
project file are either applied directly to the base PSS®ODMS model or
optionally, imported as a new project (this option requires the Project
Modeling add-on module).
