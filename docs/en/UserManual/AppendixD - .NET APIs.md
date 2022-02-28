# .NET APIs

# Introduction

PSS®ODMS includes two publicly accessible .NET APIs - CIMdbNET and
PMdbNET - to facilitate scripting and integration with external systems.
Both of these APIs are also reused internally by the PSS®ODMS
application. CIMdbNET (upon which the CIMedit user interface is built)
provides low-level access to the CIM-based network model data,
abstracting the database implementation details. PMdbNET (upon which the
Manage Projects user interface is built) provides full access to Project
Modeling module specific data, including multi-phase projects and
scenarios. In some situations, use of CIMdbNET and PMdbNET can be
combined to build powerful integrated solutions.

# Deployment

The PSS®ODMS installer includes CIMdbNET.dll and PMdbNET.dll, which are
registered as .NET assemblies. The recommeded approach for developing
and deploying .NET applications using these APIs is to install the
PSS®ODMS application in development, test and production environments,
each of which should have network access to the PSS®ODMS database
server. Use of the CIMdbNET and PMdbNET APIs does not involve running
the PSS®ODMS application executable; instead, CIMdbNET.dll and/or
PMdbNET.dll are directly imported into your .NET solution, which
presumably has its own executable. However, installing PSS®ODMS is the
simplest and safest way to ensure that all dependent files are present,
consistent and up-to-date.

Alternately, CIMdbNET.dll and PMdbNET.dll may be used in an environment
which does not have PSS®ODMS installed; however, the following dependent
files must be copied from a PSS®ODMS installation directory:
CIMdbNET.dll, PMdbNET.dll, cim10db.dll, Interop.CIM10dbLib.dll,
Oracle.ManagedDataAccess.dll (for Oracle only) and the entire
\\DBTemplates subdirectory. Additionally, cim10db.dll must be registered
using the regsvr32 utility. Be sure to update these files with each
PSS®ODMS upgrade to avoid serious incompatibility issues.

# CIMdbNET Programming Reference

## CIMdb Class

### GetClassInstances

``` c
void GetClassInstances( 
      string sURI, 
      string[] sURIProperties, 
      out string[][] saValues); 
```

Given a CIM Class URI, e.g \"cim:Substation\", return all instances of
the class along with the list of CIM Properties specified in the
sURIProperties parameter.

sURI - specifies the CIM class rdf:ID. For example, \"cim:Substation\",
\"cim:VoltageLevel\", or \"cim:Bay\"

sURIProperties - specifies a list of CIM properties that will be
returned for each instances of the class specified by sURI.

Example:

sURIProperties\[0\] = \"daf:URI\" // get the unique identifier of each
instance

sURIProperties\[1\] = \"cim:Naming.name\" // get the name of each
instance

saValues - returns a two-dimensional array of the all instances in the
class specified in sURI paremeter and their corresponding properties
specified in the sURIProperties parameter

Example:

There are 3 Substations in the model named substation1, substation2,
substation3 and their respective URIs of sID1, sID2, and sID3. If sURI =
\"cim:Substation\" and sURIProperties\[0\] = \"daf:URI\" and
sURIProperties\[1\] = \"cim:Naming.name\", then the content of saValues
will be:

saValues\[0\]\[0\] = \"sID1\"

saValues\[0\]\[1\] = \"substation1\"

saValues\[1\]\[0\] = \"sID2\"

saValues\[1\]\[1\] = \"substation2\"

saValues\[2\]\[0\] = \"sID3\"

saValues\[2\]\[1\] = \"substation3\"

### GetAssociatedClassInstances

``` c
void GetAssociatedClassInstances( 
      string sURI, 
      string sRdfIdAssoc, 
      string[] sURIProperties, 
      out string sCIMClass, 
      out string[][] saValues, 
      out string[] saCIMClasses); 
```

Given an instance URI and CIM association

(\"cim:EquipmentContainer.Contains_Equipments\"), return all instances
that satisfy the association along with the list of CIM Properties
specified in the sURIProperties parameter, the class of each instance,
and the base class of all the instance.

Example:

There is a VoltageLevel instance with a URI=\"vlID1\" in the model.

The VoltageLevel vlID1 contains a Fuse (name=\"fuse1\",

URI=\"fsID1\"), EnergyConsumer (name=\"Load1\" URI=\"ecID1\"), and a
Compensator (name=\"shunt1\" URI=\"cpID1\").

If sURI= \"vlID1\",

sRdfIdAssoc=\"cim:EquipmentContainer.Contains_Equipments\",

sURIProperties\[0\] = \"daf:URI\" and sURIProperties\[1\] =

\"cim:Naming.name\".

The result will be:

sCIMClass=\"cim:Equipment\"

saValues\[0\]\[0\] = \"fsID1\"

saValues\[0\]\[1\] = \"fuse1\"

saValues\[1\]\[0\] = \"ecID1\"

saValues\[1\]\[1\] = \"Load1\"

saValues\[2\]\[0\] = \"cpID1\"

saValues\[2\]\[1\] = \"shunt1\"

saCIMClasses\[0\] = \"cim:Fuse\"

saCIMClasses\[1\] = \"cim:EnergyConsumer\"

saCIMClasses\[2\] = \"cim:Compensator\"

### GetAssociatedClassInstancesByType

``` c
void GetAssociatedClassInstancesByType( 
      string sURI, 
      string sRdfIdAssoc, 
      string[] sURIProperties, 
      string sCIMClass, 
      out string[][] saValues);     
```

Given an instance URI, CIM association
(\"cim:EquipmentContainer.Contains_Equipments\") and CIM Class, return
all instances of the CIM Class specified by sCIMClass that satisfied the
association along with the list of CIM Properties specified in the
sURIProperties parameter.

Example:

There is a VoltageLevel instance with a URI=\"vlID1\" in the model.

The VoltageLevel vlID1 contains a Fuse (name=\"fuse1\",

URI=\"fsID1\"), EnergyConsumer (name=\"Load1\" URI=\"ecID1\"), and a

Compensator (name=\"shunt1\" URI=\"cpID1\").

If sURI= \"vlID1\",

sRdfIdAssoc=\"cim:EquipmentContainer.Contains_Equipments\",

sURIProperties\[0\] = \"daf:URI\" and sURIProperties\[1\] =

\"cim:Naming.name\", and sCIMClass=\"cimEnergyConsumer\"

The result will be:

saValues\[0\]\[0\] = \"ecID1\" saValues\[0\]\[1\] = \"Load1\"

### GetInstanceClassAndURI

``` c
void GetInstanceClassAndURI ( 
      long odmsID, 
      out string sClassURI, 
      out string sURI); 
```

Given an ODMS ID, return the CIM Class and URI for the corresponding
instance.

Note: Unlike URIs, ODMS IDs are neither globally unique nor persistent.
For example, 2 different PSS®ODMS database models imported from the same
CIM/XML will have consistent URIs but inconsistent ODMS IDs.

### GetClassProperties

``` c
void GetClassProperties( 
      string sURI, 
      string[] sPropertyURIs, 
      out string[] saProperties);     
```

Given an instance URI and a list of CIM Properties, return the values of
each property for the instance.

Example:

There is an EnergyConsumer instance with a URI=\"ecID1\",

name=\"Load1\", and Pnom=\"3.5\" in the model.

If sURI=\"ecID1\", sPropertyURIs\[0\] = \"cim:Naming.name\" and
sPropertyURIs\[1\] = \"cim:EnergyConsumer.pnom\"

The result will be:

saProperties\[0\]=\"Load1\"

saProperties\[1\]=\"3.5\"

### UpdateProperty

``` c
void UpdateProperty( 
        string sURI, 
        string sPropertyURI, 
        string sValue);
```

Given an instance URI, update the property specified by sPropertyURI
with the value in sValue.

Example:

There is an EnergyConsumer instance with a URI=\"ecID1\", name=\"Load1\"
in the model.

If sURI= \"ecID1\" and sPropertyURI=\"cim:Naming.name\" and
sValue=\"NewLoad1\", ecID1\'s name will be \"NewLoad1\" after the
update.

### AddResource

``` c
void AddResource( 
        string sCIMClass, 
        string[] saProperties, 
        string[] saValues, 
        out string sURI);
```

Add an instance of the class specified by sCIMClass; update the new
instance's properties specified the saProperties list with the
corresponding values in the saValues list and return the URI of the
newly created instance.

Currently only supports the following classes:

cim:CurveSchedData \-- requires property

\"cim:CurveSchedData.CurveSchedule\" in saProperties parameter and its
corresponding values in saValues parameter.

cim:LoadDemandModel \-- requires property

\"cim:LoadDemandModel.EnergyConsumer\" in saProperties parameter and its
corresponding values in saValues parameter.

cim:AreaLoadCurve \-- requires property

\"cim:AreaLoadCurve.LoadArea\" in saProperties parameter and its
corresponding values in saValues parameter.

cim:Measurement \-- requires property \"cim:Measurement.Terminal\" in
saProperties parameter and its corresponding values in saValues
parameter.

cim:LimitSet \-- requires property \"cim:LimitSet.Measurements\" in
saProperties parameter and its corresponding values in saValues
parameter.

cim:Limit \-- requires property \"cim:Limit.LimitSet\" in saProperties
parameter and its corresponding values in saValues parameter.

cim:MeasurementValue \-- requires property

\"cim:MeasurementValue.MemberOf_Measurement\" in saProperties parameter
and its corresponding values in saValues parameter.

Example:

To add a Limit instance to a LimitSet instance URI=\"lsID1\" and set
name of the new Limit

to \"NewLimit\" and value to 23.5, pass in the following parameter:

sCIMClass = \"cim:Limit\"

saProperties\[0\] = \"cim:Limit.LimitSet\"

saProperties\[1\] = \"cim:Naming.name\"

saProperties\[2\] = \"cim:Limit.value\"

saValues\[0\] = \"lsID1\"

saValues\[1\] = \"NewLimit\"

saValues\[2\] = \"23.5\"

sURI will be returned with the URI of the newly created Limit.

### AddExtendedResource

``` c
void AddExtendedResource( 
      string sExtendedClass, 
      string[] saProperties, 
      string[] saValues, 
      out string sURI);         
```

Add an instance of the extended class specified by sExtendClass; update
the new instance's properties specified the saProperties list with the
corresponding values in the saValues list and return the URI of the
newly created instance.

All extended classes must be a child (does not have to be direct) of the
Resources class. The table defined in the database for this class must
have a column name "OID" with data type RAW(16) for Oracle and
UniqueIdentifier for SQL Server.

Example:

To define a custom class that is a child of the cim:VoltageLevel class,
the schema xml for this class would look like this:

``` c
<xs:element name="My_VoltageLevel" msprop:superType="VoltageLevel">
<xs:complexType>
<xs:sequence>
<xs:element name="OID" type="xs:string" msprop:ddlType="RAW(16)" />
</xs:sequence>
</xs:complexType>
</xs:element>
```

Using the superType key, CIMdbNet will insert a record in the following
tables: My_VoltageLevel, VoltageLevel, EquipmentContainer,
PowerSystemResource, Naming, and Resources since VoltageLevel is a child
of EquipmentContainer and EquipmentContainer is a child of
PowerSystemResource and PowerSystemResource is a child of Naming and
finally Naming is a child of Resources.

The child relationship is enforced through database constraints. For
example on how this is done, look in the Oracle.sql and mssql.sql.

If an extended class has non-null columns then the data for those
columns must be passed in the saProperties and saValues parameters
during creation. An exception will be thrown if the necessary data is
not there.

### AddExtendedResources

``` c
void AddExtendedResources( 
    string sExtendedClass, 
    string[] saProperties, 
    string[][] saValues, 
    out string[] sURI);
```

Add new instances of the class specified by sExtendClass; update the new
instances' properties specified the saProperties list with the
corresponding values in the saValues list and return the URIs of the
newly created instances. The length of each row in saValues must be the
same and match the length of saProperties.

Example:

If saProperties is

``` c
[“cim:Naming.name”] 
[“cim:AreaLoadCurve.LoadArea”] 
[“cim:Naming.aliasName”] 
```

Then each row in saValues must have 3 columns:

``` c
[“name1”][“loadArea_uri1”][“alias1] 
[“name2”][“loadArea_uri2”][“”] 
[“name2”][“loadArea_uri3”][“alias3] 
```

The returned sURI array will have 3 URIs for the 3 newly created
instances.

``` c
sURI[0] = uri for “name1” 
sURI[1] = uri for “name2” 
sURI[2] = uri for “name3” 
```

### DeleteResource

``` c
void DeleteResource( 
      string sURI, 
      string sCIMClass);
```

Delete the instance specified by the sURI parameter.

Currently only supports the following classes:

``` c
cim:CurveSchedData 
cim:LoadDemandModel 
cim:Measurement 
cim:LimitSet 
cim:Limit 
cim:MeasurementValue             
```

### GetManyToManyAssociation

``` c
void GetManyToManyAssociation( 
      string sURI, 
      out Dictionary<string, 
      string[]> daValues);             
```

Return a many-to-many association.

Example:

-If sURI=\"cim:Measurement.LimitSets\" the Dictionary\'s key will be the
URI of the measurement and the string array will contains the list of
LimitSet URIs that are associated with the measurement in the key.

-If sURI=\"cim:LimitSet.Measurements\" then the Dictionary\'s key will
be the URI of the LimitSet and the string array will contains the list
of Measurements URIs that are associated with the LimitSet in the key.

### AddManyToManyProperty

``` c
void AddManyToManyProperty( 
      string sURI, 
      string sPropertyURI, 
      string sValues);            
```

Add an association to a many-to-many property.

Example:

-If sPropertyURI=\"cim:Measurement.LimitSets\" then sURI is the URI of
the measurement and sValue is the URI of the LimitSet.

-If sPropertyURI= \"cim:LimitSet.Measurements\" then sURI is the URI of
the LimitSet and sValue is the URI of the measurement.

### DeleteManyToManyProperty

``` c
void DeleteManyToManyProperty(
      string sURI, 
      string sPropertyURI, 
      string sValues);     
```

Delete an association to a many-to-many property.

-If sPropertyURI=\"cim:Measurement.LimitSets\" then sURI is the uri of
the measurement and sValue is the uri of the LimitSet.

-If sPropertyURI= \"cim:LimitSet.Measurements\" then sURI is the uri of
the LimitSet and sValue is the uri of the measurement.

### PropertyMetadata GetPropertyMetadata

``` c
PropertyMetadata GetPropertyMetadata( 
      string sURI);
```

Given CIM property (sURI=\"cim:Naming.name\" or

sURI=\"cim:PowerSystemResource.PSRType\"), return the corresponding
IValidator to perform client side validation based on the database type
of the property.

``` c
namespace PTI.CIMdbNET 
    { 
    public class PropertyMetadata
      {            

public bool IsReadOnly;
```

\- Return true if property is not updatable in the database. Right now
any field that is specified as a primary key is read only.

``` c
public IValidator Validator;
```

-Return an IValidator to perform client side validation

Based on the database type of the property define in the schema xml file
(oracleSchema.xml or Oracle and mssqlSchema.xml for SQLServer).

``` c
public bool IsOIDColumn;
```

-Return true if property is an OID column in the database.

msdata:DataType=\"System.Guid\" for SQLServer and

msprop:ddlType=\"RAW(16)\" for Oracle.

public bool IsNullable;

-Return true if the property allow null value in the database.
(minOccurs=\"0\" in the schema xml file)

``` c
} 
} 
namespace PTI.CIMdbNET 
{ 
public interface IValidator 
{ 
bool IsValid(object value, 
System.Globalization.CultureInfo cultureInfo);
```

-Return true if value is valid for updating to the database.

Example:

If \"cim:Naming.name\" property was use to obtain the PropertyMetadata.
Using the information store in the Resources table, which get populated
using the resources.sql file, the property is being store in table
Naming and column Name. Using the schema xml, the data type for the
property is

``` c
<xs:element name="name" type="xs:string" 
msprop:ddlType="NVARCHAR2(255)" minOccurs="0" />
```

For Oracle:

``` c
<xs:element name="name" type="xs:string" 
msprop:ddlType="nvarchar(255)" minOccurs="0" />    
```

For SQL Server:

-IsValid will return true if value is less than or equal to 255.

-For number type, IsValid will also check for invalid characters,
precision if specified, and whether the format is correct to the
specified cultureInfo.

-For OID type, IsValid only check if value is less than 255 since
CIMdbNet interface for this type is the URI and not the actual raw data.
User can call the CIMdbNet method IsValidResource(string sURI) for
validation instead.

``` c
     } 
    } 
void GetPropertyPossibleValues ( 
    string sURI, 
    out string[] saEnumList, 
    out string[] saEnumNames);
```

Return all the possible values of the specified property.

Example:

If sURI=\"cim:Measurement.Unit\", return all the units available in the
model. saEnumList contains an array of URIs of the Units and if Unit
class inherit from Naming class, saEnum-Names contains the array of
names property for the Unit, otherwise it contains the same information
as saEnumList (URIs).

### GetPropertyEnumeratedValues

``` c
void GetPropertyEnumeratedValues ( 
      string sURI, 
      out string[] saEnumList, 
      out string[] saEnumNames);         
```

Return all enumerated values defined by the CIM for this property.

Example:

sURI=\"cim:PowerTransformer.transformerType\", return all enumerated
transformer type define by the CIM. saEnumList contains the URI of the
enumeration, saEnumNames contains the RDFS_Label of the enumeration.

### UpdateProperties

``` c
void UpdateProperties ( 
      string[] saURI, 
      string[][] saPropertyURIs, 
      string[][] saValues);             
```

Update properties of instances in saURI with the values in saValues.
Each row in saPropertyURIs does not have to be the same length, but each
row length in saPropertyURIs must match the row length of saValues.

Example:

Updating various properties of 3 different instances

``` c
saURI = [“pti:_this_is_limit1”]
[“pti:_this_is_load1”]
[“pti:_this_is_substation1”]
saPropertyURIs =
[cim:Limit.value”] 
[“cim:EnergyConsumer.pFexp”][“ cim:EnergyConsumer.pfixed”] 
[“cim:Naming.name”][“ cim:Substation.MemberOf_SubControlArea”] 
saValues = 
[“12.3”] 
[“35.4”][“11.1”] 
[“New Sub Name”][“pti:_this_is_SCA1”] 
```

The example above updates the limit's value, load's pFexp and pfixed
values, and substation's name and SubControlArea parent association.

For faster performance, when creating new instances, pass in all
properties that need to be set in the create instance method. Do not
create an instance and then call update to update the properties.

When updating associations, only Child-to-Parent associations are
supported and NOT Parent-to-Child. For example,
cim:Substation.MemberOf_SubControlArea is supported but not
cim:SubControlArea.Contain_Substations.

Many-to-Many associations are not supported.

### CreateDifferenceModel

``` c
bool CreateDifferenceModel ( 
      string file1, 
      string file2, 
      string outfile);             
```

Create a difference (incremental) model from file1 to file2 into
outfile. The resulting incremental CIM/XML file can be imported into a
model containing file1 instances to create a model with only file2
instances.

### ConvertGeneratingUnitType

``` c
bool ConvertGeneratingUnitType ( 
      string sURI, 
      string newUnitType);     
```

Convert a GeneratingUnit from one type to another.

sURI is the URI of the generating unit.

newUnitType is the CIM type to convert to.

Possible values are: cim:GeneratingUnit,

cim:ThermalGeneratingUnit, cim:HydroGeneratingUnit,

cim:NuclearGeneratingUnit, cim:WindGeneratingUnit

### AddExtendedResource

``` c
void AddExtendedResource (
      string sURI, 
      string sExtendClass, 
      string[] saProperties, 
      string[] saValues);    
```

This function is for internal PSS®ODMS application use only (not
supported for external processes).

## ModelUtility Class

### ImportIncrementalXml

``` c
bool ImportIncrementalXml( 
      string filename, 
      string connect, 
      int phaseID = 0);     
```

Import an incremental CIM/XML file. Return true if the import is
successful.

filename -- full path name of the incremental CIM/XML file to be
imported.

connect -- OLEDB connection string used to connect to the database model
where the incremental changes are to be imported.

The examples below assume the model name and password is TEST and the
server name is ODMS.

Example 1 (Oracle):

``` c
connect = “Provider=MSDataShape;Data Provider=OraOLEDB.Oracle;Data Source=ODMS;User ID=TEST;Password=TEST;Extended Properties="PLSQLRSet=1;Reshape Name=1;OLE DB Services = -2"
```

Example 2 (SQL Server):

``` c
Connect = “Provider=MSDataShape;Data Provider=SQLOLEDB;Data Source=.\ODMS;Initial Catalog=TEST;Integrated Security=SSPI;Extended Properties="PLSQLRSet=1;Reshape Name=1;OLE DB Services = -2"
```

phaseID -- default is 0. If nonzero then the changes will be applied to
the specified phase, otherwise the changes will be applied to the base
model.

# PMdbNET Programming Reference

The PMdbNET assembly supports a set of API functions to access the
Project Modeling information in PSS®ODMS from external .NET programs. It
provides the ability to retrieve and modify phases, projects, and
scenarios as well as activating/deactivating a scenario and start/stop
recording.

## PMdb Class

### Class Overview

  -----------------------------------------------------------------------
  PMdb
  -----------------------------------------------------------------------
  Methods

  Connect - Establishes a connection to the database

  GetProjects - Retrieves a comprehensive list of projects

  GetScenarios - Retrieves a comprehensive list of scenarios

  GetPhases - Retrieves a comprehensive list of phases

  GetPhases - Retrieves a time-bound list of phases

  GetPhases - Retrieves a list of phases occurring prior to another phase

  GetScenario - Returns a scenario by ID

  GetActiveScenario - Returns the active scenario

  CreateScenario - Creates a new scenario

  DeleteScenario - Deletes a scenario

  ActivateScenario - Activates a scenario

  DeactivateScenario - Deactivates the currently active scenario

  GetRecordingPhase - Returns the phase currently recording changes

  GetRecordingPhaseID - Returns the ID of the phase currently recording
  changes

  SetModelRecording - Start/stop model change recording

  GetCim10Database - Returns a Cim10Database object reference

  CreateProject - Creates a new project

  CreatePhase - Creates a new phase

  SetPhaseCommissionDate - Changes the commission date of a phase
  -----------------------------------------------------------------------

### Connect Method

  ------------- ---------------------------------------------------------
  Description   The Connect method establishes a connection to the
                database.

  Syntax        void Connect(string username, string password, string
                server, string factory, string schemaDir)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetProjects Method

  ------------- ---------------------------------------------------------
  Description   The GetProjects method will return all the project
                instances.

  Syntax        void GetProjects(ArrayList projects)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetScenarios Method

  ------------- ---------------------------------------------------------
  Description   The GetScenarios method will return all the scenario
                instances.

  Syntax        void GetScenarios(ArrayList scenarios)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetPhases Method

  ------------- ---------------------------------------------------------
  Description   The (overloaded) GetPhases method returns a list of all
                phases with option to specify approved projects only.

  Syntax        void GetPhases(ArrayList phases, Boolean approved)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetPhases Method

  ------------- ---------------------------------------------------------
  Description   The (overloaded) GetPhases method returns a list of all
                phases by commission date with option to specify approved
                projects only

  Syntax        void GetPhases(ArrayList phases, DateTime commissionDate,
                Boolean approved)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetPhases Method

  ------------- ---------------------------------------------------------
  Description   The (overloaded) GetPhases method returns a list of all
                phases prior to a specific phase with option to specify
                approved projects only.

  Syntax        void GetPhases(ArrayList phases, Int32 phaseID, Boolean
                approved)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetScenario Method

  ------------- ---------------------------------------------------------
  Description   The GetScenario method returns a specific Scenario
                instance given a scenario id.

  Syntax        Scenario GetScenario(Int32 scenarioID)

  Return Type   Scenario instance (see below for definition)

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetActiveScenario Method

  ------------- ---------------------------------------------------------
  Description   The GetActiveScenario method will return the currently
                active scenario.

  Syntax        void GetActiveScenario()

  Return Type   Scenario instance (see below for definition)

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### CreateScenario Method

  ------------- ---------------------------------------------------------
  Description   The CreateScenario method will create a new scenario
                using the passed in data fields and return the instance
                to the user. A new entry will be created in the database
                model.

  Syntax        Scenario CreateScenario(string newScenarnioName, string
                newComment, Boolean shared, DateTime scenarioStartDate,
                DateTime scenarioEndDate)

  Return Type   Scenario instance (see below for definition)

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### DeleteScenario Method

  ------------- ---------------------------------------------------------
  Description   The DeleteScenario method will delete the scenario
                specified by the input scenario ID from the internal list
                and the database model.

  Syntax        void DeleteScenario(int scenarioID)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### ActivateScenario Method

  ------------- ---------------------------------------------------------
  Description   The ActivateScenario method will activate the scenario as
                specified by the passed in scenario ID.

  Syntax        void ActivateScenario(int scenarioID)

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### DeactivateScenario Method

  ------------- ---------------------------------------------------------
  Description   The DeactivateScenario method will deactivate the
                currently active scenario.

  Syntax        void DeactivateScenario()

  Return Type   None.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetRecordingPhase Method

  ------------- ---------------------------------------------------------
  Description   The GetRecordingPhase method will return a reference to
                the Phase that is currently recording changes.

  Syntax        Phase GetRecordingPhase()

  Return Type   Phase instance (see below for definition).

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetRecordingPhaseID Method

  ------------- ---------------------------------------------------------
  Description   The GetRecordingPhaseID method will return the ID of the
                Phase instance that is currently recording changes.

  Syntax        int GetRecordingPhaseID()

  Return Type   int - ID of the Phase currently recording changes

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### SetModelRecording Method

  ------------- ---------------------------------------------------------
  Description   The SetModelRecording method will start or stop model
                recording. void SetModelRecording(int scenarioID, int
                phaseID)

  Syntax        None.

  Return Type   If the phaseID passed in is 0 it will stop recording
                otherwise it will set recording active for the passed in
                phase ID assuming a match to the phase is found.

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### GetCim10Database Method

  ------------- ---------------------------------------------------------
  Description   The GetCim10Database method will return a reference to
                the Cim10Database owned by this PMdbNET instance.

  Syntax        IMOD GetCim10Database()

  Return Type   IMOD as Cim10Database

  Remarks       This method is intended to be called by a remote
                interface to PMdbNET.
  ------------- ---------------------------------------------------------

### CreateProject Method

  ------------- ---------------------------------------------------------
  Description   The CreateProject method will create a new project and
                return the new project ID.

  Syntax        int CreateProject(string projectName, string
                projectComment)

  Return Type   int - ID of created project

  Remarks       If 0 is returned then CreateProject did not complete
                successfully. Project state is defaulted to preliminary.
  ------------- ---------------------------------------------------------

### CreatePhase Method

  ------------- ---------------------------------------------------------
  Description   The CreatePhase method will create a new phase belonging
                to the specified project and return the new phase ID.

  Syntax        int CreatePhase(int projectID, string phaseName, string
                phaseComment, string commissionDate, string
                decommissionDate)

  Return Type   int - ID of create phase

  Remarks       If 0 is returned then CreatePhase did not complete
                successfully. commissionDate/decommissionDate format is
                yyyy/mm/dd.
  ------------- ---------------------------------------------------------

### SetPhaseCommissionDate Method

  ------------- ---------------------------------------------------------
  Description   The SetPhaseCommissionDate method will update the
                commission date of the specified phase.

  Syntax        bool SetPhaseCommissionDate(int phaseID, string
                commissionDate)

  Return Type   bool - true if update is successful or false if
                unsuccessful

  Remarks       commissionDate format is yyyy/mm/dd. No validation is
                performed on whether model changes in the phase are still
                valid with the new commission date.
  ------------- ---------------------------------------------------------

## ModelChange Class

  -----------------------------------------------------------------------
  ModelChange
  -----------------------------------------------------------------------
  Properties

  ProjectName

  ID

  ODMSID

  ElementType

  ElementName

  Action

  Property

  OriginalValue

  NewValue

  Substation

  ModelChange

  CreatedTime

  DeletedTime
  -----------------------------------------------------------------------

### ProjectName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectName property is used to return the
                ProjectName that this Model-Change belongs to

  C# Syntax     String ProjectName

  Return Type   Read/Write String

  Remarks       
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the model change.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This Property should be treated as read-only as the ID is
                managed internally.
  ------------- ---------------------------------------------------------

### ODMSID Property

  ------------- ---------------------------------------------------------
  Description   The ODMSID property is the internal ID of the resource.

  C# Syntax     Int32 ODMSID

  Return Type   Read/Write Int32

  Remarks       This property should be treated as read-only as the
                ODMSID is managed internally.
  ------------- ---------------------------------------------------------

### ElementType Property

  ------------- ---------------------------------------------------------
  Description   The ElementType property is the element type of the model
                change.

  C# Syntax     String ElementType

  Return Type   Read/Write String

  Remarks       
  ------------- ---------------------------------------------------------

### ElementName Property

  ------------- ---------------------------------------------------------
  Description   The ElementName property is the element name of the model
                change.

  C# Syntax     String ElementName

  Return Type   Read/Write String

  Remarks       
  ------------- ---------------------------------------------------------

### Action Property

  ------------- ---------------------------------------------------------
  Description   The Action property is the type of model change. This can
                be \'Added\', \'Changed\', or \'Deleted\'.

  C# Syntax     String Action

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### Property Property

  ------------- ---------------------------------------------------------
  Description   The Property property is an attribute of a model change.

  C# Syntax     String Property

  Return Type   Read/Write String

  Remarks       This property will only be set if Action = \'Changed\'
  ------------- ---------------------------------------------------------

### OrginalValue Property

  ------------- ---------------------------------------------------------
  Description   The OriginalValue property is the original value of a
                model change.

  C# Syntax     String OriginalValue

  Return Type   Read/Write String

  Remarks       This property will only be set if Action = \'Changed\'
  ------------- ---------------------------------------------------------

### NewValue Property

  ------------- ---------------------------------------------------------
  Description   The NewValue property is the new value of a model change.

  C# Syntax     String NewValue

  Return Type   Read/Write String

  Remarks       This property will only be set if Action = \'Changed\'
  ------------- ---------------------------------------------------------

### Substation Property

  ------------- ---------------------------------------------------------
  Description   The Substation property is the name of the substation
                where the model change resides.

  C# Syntax     String Substation

  Return Type   Read/Write String

  Remarks       
  ------------- ---------------------------------------------------------

### CreatedTime Property

  ------------- ---------------------------------------------------------
  Description   The CreatedTime property is the date/time the model
                change was created.

  C# Syntax     DateTime CreatedTime

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### DeletedTime Property

  ------------- ---------------------------------------------------------
  Description   The DeletedTime property is the date/time the model
                change was removed.

  C# Syntax     DateTime CreatedTime

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

## Phase Class

  -----------------------------------------------------------------------
  Phase
  -----------------------------------------------------------------------
  Properties

  PhaseName

  ID

  ProjectID

  ProjectName

  Description

  CreatedBy

  CreationDate

  CommissionDate

  DecommissionDate

  CommittedTime

  CommittedToModel

  CommittedToModelBool

  ChangeRef
  -----------------------------------------------------------------------

### PhaseName Property

  ------------- ---------------------------------------------------------
  Description   The PhaseName property is used to return the name of this
                Phase.

  C# Syntax     String PhaseName

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the phase.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This Property should be treated as read-only as the ID is
                managed internally.
  ------------- ---------------------------------------------------------

### Project ID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectID property is the internal ID of the project.

  C# Syntax     Int32 ProjectID

  Return Type   Read/Write Int32

  Remarks       This Property should be treated as read-only as the
                ProjectID is managed internally.
  ------------- ---------------------------------------------------------

### ProjectName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectName property is the name of the project for
                this phase.

  C# Syntax     String ProjectName

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### Description Property

  ------------- ---------------------------------------------------------
  Description   The Description property is the description of this
                phase.

  C# Syntax     String Description

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreatedBy Property

  ------------- ---------------------------------------------------------
  Description   The CreatedBy property is the name of the user that
                created the phase.

  C# Syntax     String CreatedBy

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreationDate Property

  ------------- ---------------------------------------------------------
  Description   The CreationDate property is the date the phase was
                created.

  C# Syntax     DateTime CreationDate

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CommissionDate Property

  ------------- ---------------------------------------------------------
  Description   The CommissionDate property represents the planned
                effective date for the model changes contained within the
                Phase.

  C# Syntax     DateTime CommissionDate

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### DecommissionDate Property

  ------------- ---------------------------------------------------------
  Description   The DecommissionDate property (End Date in the GUI) is an
                optional date for additional scenario creation
                flexibility, representing a planned date at which the
                changes contained within the Phase are no longer
                effective (assuming they are never actually committed to
                the model).

  C# Syntax     DateTime DecommissionDate

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CommittedTime Property

  ------------- ---------------------------------------------------------
  Description   The CommittedTime property is the date the phase was
                committed..

  C# Syntax     DateTime CommittedTime

  Return Type   Read/Write ObservableCollection\<Phase>

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CommittedToModel Property

  ------------- ---------------------------------------------------------
  Description   The CommittedToModel property is a \"Yes\" / \"No\"
                string indicating if the phase has been committed to the
                model or not.

  C# Syntax     String CommittedToModel

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CommittedToModelBool Property

  ------------- ---------------------------------------------------------
  Description   The CommittedToModelBool property is Boolean flag
                indicating if the phase has been committed to the model
                or not.

  C# Syntax     Boolean CommittedToModelBool

  Return Type   Boolean

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### ChangeRef Property

  ------------- ---------------------------------------------------------
  Description   The ChangeRef property contains a reference to a
                collection of ModelChange objects for this Phase.

  C# Syntax     ObservableCollection\<ModelChange> ChangeRef

  Return Type   Read/Write ObservableCollection\<ModelChange>

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

## Project Class

  -----------------------------------------------------------------------
  Project
  -----------------------------------------------------------------------
  Properties

  ProjectName

  ID

  Description

  CreatedBy

  CreationDate

  ProjectTypeName

  ProjectTypeID

  ProjectStateName

  ProjectStateID

  Owner

  PhaseRef
  -----------------------------------------------------------------------

### ProjectName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectName property is used to return the name of
                this project.

  C# Syntax     String ProjectName

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the phase.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This Property should be treated as read-only as the ID is
                managed internally.
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the project.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This Property should be treated as read-only as the
                ProjectID is managed internally.
  ------------- ---------------------------------------------------------

### Description Property

  ------------- ---------------------------------------------------------
  Description   The Description property is the description of this
                project.

  C# Syntax     String Description

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreatedBy Property

  ------------- ---------------------------------------------------------
  Description   The CreatedBy property is the name of the user that
                created this project.

  C# Syntax     String CreatedBy

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreationDate Property

  ------------- ---------------------------------------------------------
  Description   The CreationDate property is the date the project was
                created.

  C# Syntax     DateTime CreationDate

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectTypeName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectTypeName property is enumerated value name
                describing the type of project.

  C# Syntax     String ProjectTypeName

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectTypeID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectTypeID property is the internal ID of the
                associated ProjectType enumeration.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### ProjectStateName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectStateName property is enumerated value name
                describing the current state of the project.

  C# Syntax     String ProjectStateName

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectStateID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectStateID property is the internal ID of the
                associated ProjectState enumeration.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### Owner Property

  ------------- ---------------------------------------------------------
  Description   The Owner property is the name of the group that the user
                who created this project belongs to. The GROUPID field in
                the MODPROJECT table is a foreign key into the MODGROUP
                table containing the name of the group.

  C# Syntax     String Owner

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### PhaseRef Property

  ------------- ---------------------------------------------------------
  Description   The PhaseRef property contains a reference to a
                collection of Phase objects for this Project.

  C# Syntax     ObservableCollection\<Phase> PhaseRef

  Return Type   Read/Write ObservableCollection\<Phase>

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

## Scenario Class

  -----------------------------------------------------------------------
  Scenario
  -----------------------------------------------------------------------
  Properties

  ScenarioName

  ID

  Description

  CreatedBy

  CreationDate

  Owner

  Shared

  SharedBool

  ScenarioStartDate

  ScenarioEndDate

  PreviewProjectsRef
  -----------------------------------------------------------------------

### ScenarioName Property

  ------------- ---------------------------------------------------------
  Description   The ScenarioName property is used to return the name of
                this scenario.

  C# Syntax     String ScenarioName

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the project.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property should be treated as read-only as the ID is
                managed internally.
  ------------- ---------------------------------------------------------

### Description Property

  ------------- ---------------------------------------------------------
  Description   The Description property is the description of this
                phase.

  C# Syntax     String Description

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreatedBy Property

  ------------- ---------------------------------------------------------
  Description   The CreatedBy property is the name of the user that
                created this scenario.

  C# Syntax     String CreatedBy

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### Owner Property

  ------------- ---------------------------------------------------------
  Description   The Owner property is the name of the group that the user
                who created this scenario belongs to. The GROUPID field
                in the MODSCENARIO table is a foreign key into the
                MODGROUP table containing the name of the group.

  C# Syntax     String Owner

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### Shared Property

  ------------- ---------------------------------------------------------
  Description   The Shared property is a \"True/False\" string indicating
                if this scenario is shared or not.

  C# Syntax     String Shared

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### SharedBoolProperty

  ------------- ---------------------------------------------------------
  Description   The SharedBool property is a Boolean flag indicating if
                this scenario is shared or not.

  C# Syntax     Boolean Shared

  Return Type   Read/Write Boolean

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### ScenarioStartDate Property

  ------------- ---------------------------------------------------------
  Description   The ScenarioStartDate property is an optional date used
                for additional flexibility in creating more tightly
                time-constrained scenarios.

  C# Syntax     DateTime ScenarioStartDate

  Return Type   Read/Write ScenarioStartDate

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### ScenarioEndDate Property

  ------------- ---------------------------------------------------------
  Description   The ScenarioEndDate property (previously ScenarioDate) is
                the date planned for all phases in the scenario to be
                commissioned by. The scenario will contain no phases with
                a commission date greater than the scenario date. If the
                scenario date is changed the phases within the scenario
                will be updated appropriately (added or removed).

  C# Syntax     DateTime ScenarioEndDate

  Return Type   Read/Write ScenarioEndDate

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### PreviewProjectRef Property

  ------------- ---------------------------------------------------------
  Description   The PreviewProjectRef property contains a reference to a
                collection of PreviewProject objects for this Scenario

  C# Syntax     ObservableCollection\<PreviewProject> PreviewProjectRef

  Return Type   Read/Write ObservableCollection\<PreviewProject>

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

## PreviewProject Class

  -----------------------------------------------------------------------
  PreviewProject
  -----------------------------------------------------------------------
  Properties

  ProjectRef

  Name

  ID

  Description

  CreatedBy

  CreationDate

  ProjectTypeID

  ProjectTypeName

  ProjectStateID

  ProjectStateName

  PreviewPhasesRef

  SID
  -----------------------------------------------------------------------

### ProjectRef Property

  ------------- ---------------------------------------------------------
  Description   The ProjectRef property is used to return a reference to
                the Project instance contained in this wrapper.

  C# Syntax     Project ProjectRef

  Return Type   Read/Write Project

  Remarks       This property should be treated as read-only
  ------------- ---------------------------------------------------------

### NameProperty

  ------------- ---------------------------------------------------------
  Description   The Name property is used to return the name of this
                project.

  C# Syntax     String Name

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the project.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### Description Property

  ------------- ---------------------------------------------------------
  Description   The Description property is the description of this
                project.

  C# Syntax     String Description

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreatedBy Property

  ------------- ---------------------------------------------------------
  Description   The CreatedBy property is the name of the user that
                created this project.

  C# Syntax     String CreatedBy

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### CreationDate Property

  ------------- ---------------------------------------------------------
  Description   The CreationDate property is the date the project was
                created.

  C# Syntax     DateTime CreationDate

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### ProjectTypeName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectTypeName property is enumerated value name
                describing the type of project.

  C# Syntax     String ProjectTypeName

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectTypeID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectTypeID property is the internal ID of the
                associated ProjectType enumeration.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### ProjectStateName Property

  ------------- ---------------------------------------------------------
  Description   The ProjectStateName property is enumerated value name
                describing the current state of the project.

  C# Syntax     String ProjectStateName

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectStateID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectStateID property is the internal ID of the
                associated ProjectState enumeration.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the
                Project instance contained in this wrapper. This property
                should be treated as read-only
  ------------- ---------------------------------------------------------

### PreviewPhaseRef Property

  ------------- ---------------------------------------------------------
  Description   The PreviewPhasesRef property contains a reference to a
                collection of PreviewPhase objects for this
                PreviewProject.

  C# Syntax     ObservableCollection\<PreviewPhase> PreviewPhasesRef

  Return Type   Read/Write ObservableCollection\<PreviewPhase>

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### SID Property

  ------------- ---------------------------------------------------------
  Description   The SID property is the internal scenario ID that is the
                parent of this preview project.

  C# Syntax     Int32 SID

  Return Type   Read/Write SID

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

## PreviewPhase Class

  -----------------------------------------------------------------------
  PreviewPhase
  -----------------------------------------------------------------------
  Properties

  PhaseRef

  PreviewPhase

  Name

  ID

  ProjectID

  Description

  CreatedBy

  CreationDate

  CommissionDate

  DecommissionDate

  CommittedTime

  ChangeRef

  SID
  -----------------------------------------------------------------------

### PhaseRef Property

  ------------- ---------------------------------------------------------
  Description   The PhaseRef property is used to return a reference to
                the Phase instance contained in this wrapper.

  C# Syntax     Phase PhaseRef

  Return Type   Read/Write Phase

  Remarks       This property should be treated as read-only
  ------------- ---------------------------------------------------------

### Name Property

  ------------- ---------------------------------------------------------
  Description   The Name property is used to return the name of this
                Phase.

  C# Syntax     String Name

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### ID Property

  ------------- ---------------------------------------------------------
  Description   The ID property is the internal ID of the phase.

  C# Syntax     Int32 ID

  Return Type   Read/Write Int32

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### ProjectID Property

  ------------- ---------------------------------------------------------
  Description   The ProjectID property is the internal ID of the project.

  C# Syntax     Int32 ProjectID

  Return Type   Read/Write Int32

  Remarks       This property should be treated as read-only as the
                ProjectID is managed internally.
  ------------- ---------------------------------------------------------

### Description Property

  ------------- ---------------------------------------------------------
  Description   The Description property is the description of this
                phase.

  C# Syntax     String Description

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### CreatedBy Property

  ------------- ---------------------------------------------------------
  Description   The CreatedBy property is the name of the user that
                created the phase.

  C# Syntax     String CreatedBy

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### CreationDate Property

  ------------- ---------------------------------------------------------
  Description   The CreationDate property is the date the phase was
                created. DateTime CreationDate

  C# Syntax     Read/Write String

  Return Type   This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### CommisionDate Property

  ------------- ---------------------------------------------------------
  Description   The CommissionDate property represents the planned
                effective date for the model changes contained within the
                Phase.

  C# Syntax     DateTime CommissionDate

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### DecommissionDate Property

  ------------- ---------------------------------------------------------
  Description   The DecommissionDate property (End Date in the GUI) is an
                optional date for additional scenario creation
                flexibility, representing a planned date at which the
                changes contained within the Phase are no longer
                effective (assuming they are never actually committed to
                the model).

  C# Syntax     DateTime DecommissionDate

  Return Type   Read/Write String

  Remarks       This property should be treated as read-only.
  ------------- ---------------------------------------------------------

### CommittedTime Property

  ------------- ---------------------------------------------------------
  Description   The CommittedTime property is the date the phase was
                committed.

  C# Syntax     DateTime CommittedTime

  Return Type   Read/Write String

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------

### ChangeRef Property

  ------------- ---------------------------------------------------------
  Description   The ChangeRef property contains a reference to a
                collection of ModelChange objects for this Phase.

  C# Syntax     ObservableCollection\<ModelChange> ChangeRef

  Return Type   Read/Write ObservableCollection\<ModelChange>

  Remarks       This property internally uses the properties of the Phase
                instance contained in this wrapper. This property should
                be treated as read-only.
  ------------- ---------------------------------------------------------
