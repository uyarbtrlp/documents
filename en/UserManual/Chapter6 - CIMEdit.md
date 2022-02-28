# CIMedit Interface

## Introduction

CIMedit is a hierarchical model editing window with the following
attributes:

1.  The contents of each CIMedit \"view\" (including property
    description and tooltip text, ordering and layout, and tab-grouped
    property pages) are fully customizable via XML configuration file.

2.  CIMedit supports viewing and editing of user-extended data fields in
    the PSS®ODMS database schema.

3.  CIMedit supports context menu customization as well as the
    integration of custom windows or dialogs programmed in any .NET
    language with comprehensive read/write access to the database model
    provided by CIMdbNET.

4.  CIMedit supports custom data field validation.

The terminology displayed in CIMedit reflects the fact that PSS®ODMS is
based on the IEC CIM 61970 standard. The default attribute tooltips in
CIMedit are drawn directly from the standard UML. For more information
on related CIM classes, attributes and associations, refer to the
official CIM documentation, which can be obtained from
http://cimug.ucaiug.org. For additional information on PSS®E-specific
extensions, refer to the official PSS®E product documentation.

## Launching CIMedit {#section_uqq_jyf_xp}

To begin using CIMedit, a model must be currently open in PSS®ODMS. To
open a CIMedit window, select ***Model>CIMedit*** from the main menu and
choose the appropriate sub-menu command for the specific CIMedit view
you want to open.

![CIMedit Menu](/images/PSSODMS_UserManual_2014-10-17114243_img_26.png)

![CIMedit Window](/images/PSSODMS_UserManual_2014-10-17114243_img_27.png)

## Customizing CIMedit {#section_erq_jyf_xp}

CIM version-specific default CIMedit configuration files are provided
with each PSS®ODMS installation (under c:\\Program
Files\\PTI\\ODMS\\CIMedit) and can be used as a template for creating
additional CIMedit views. You can create as many views as you want
within the CIMedit directory and specify the default configuration file
for PSS®ODMS to use for each CIM version.

Refer to the related supplemental product documentation for details and
examples.

![CIMedit Configuration
File](/images/PSSODMS_UserManual_2014-10-17114243_img_28.png)

### Custom Data Conversion {#section_yrq_jyf_xp}

CIMedit allows custom data conversion through the interface IConverter
and the \<Converter> xml tag. The IConverter interface is defined in the
CIMedit.Extensibilty namespace and can be reference through the
CIMedit.Extensibility.dll. The \<Converter> xml tag is to be used in the
CIMedit configuration xml file to specify the dll and class that will be
use for data conversion. The class specified in the \<Converter> tag
must implement the IConverter interface Convert and ConvertBack methods.

``` c
            namespace CIMedit.Extensibility 
            { 
            public interface IConverter 
             {
             string Convert(string value, DataWindowContext parameter,
                System.Globalization.CultureInfo culture); 
             string ConvertBack(string value, DataWindowContext parameter,
                System.Globalization.CultureInfo culture); 
             } 
            } 
            <Property name="R (pu)" type="cim:Conductor.r"
                toolTip="Resistance in Per Unit"> 
             <Converter handlerAssembly="CIMeditExtensionSample" 
             handler="CIMeditExtensionSample.OhmPerUnitConverter"/> 
            </Property> 
```

The Convert method is called by CIMedit to convert the original value
stored in the ODMS database before displaying in the CIMedit text box.

The ConvertBack method is called when CIMedit needs to update the value
from the CIMedit text box to the ODMS database. ConvertBack will be
called to convert the value in the text box before updating it to the
database.

A common scenario for custom data conversion is that the ODMS database
stores resistance and reactance values in Ohms. To allow viewing and
editing of these values in per unit, define a class that implement the
IConverter interface to convert the original value from Ohms to per unit
in the Convert method and from per unit to Ohms in the ConvertBack
method (so that the value will be properly stored back in the database
in Ohms).

The example OhmPerUnitConverter class below can be found in the
CIMeditExtensionSample .NET solution delivered under \"C:\\Program
Files\\PTI\\ODMS\\CIMedit\\CIMeditExtensionSample.\"

The value parameter in Convert method is the original value from the
database.

The DataWindowContext class contain 2 properties.

DataWindowContext.InstanceURI is the URI of the instance that the
property belong to.

DataWindowContext.Database is the CIMdbNet instance that CIMedit is
currently connected to.

The value parameter in ConvertBack method is the value from the CIMedit
text box.

``` c
            using System; 
            using System.Collections.Generic;
            using System.Text; 
            using CIMedit.Extensibility;
            using PTI.CIMdbNET; 
            namespace CIMeditExtensionSample 
            { 
             public class OhmPerUnitConverter : IConverter 
             { 
             public string Convert(string value, DataWindowContext parameter,
                System.Globalization.CultureInfo culture) 
             { 
             // convert ohm to per unit. 
             float fOhm; 
             bool bOK = float.TryParse(value, out fOhm); 
             if (!bOK) 
             return null; 
             string sURI = parameter.InstanceURI; 
             string[] saProp = {"cim:ConductingEquipment.BaseVoltage"}; 
             string[] saValue; 
             parameter.Database.GetClassProperties(sURI, saProp, out saValue); 
             string sBaseVoltageID = saValue[0]; 
             if (!string.IsNullOrEmpty(sBaseVoltageID)) 
             { 
             saProp[0] = "cim:BaseVoltage.nominalVoltage"; 
             parameter.Database.GetClassProperties(sBaseVoltageID, saProp, out saValue); 
             if (!string.IsNullOrEmpty(saValue[0])) 
             { 
             float fNominalVoltage; 
             bOK = float.TryParse(saValue[0], out fNominalVoltage); 
             if (bOK) 
             { 
             try 
             { 
             float fUnit = (fOhm * (float)100.0) / (fNominalVoltage * fNominalVoltage); 
             return fUnit.ToString(); 
             } 
             catch (Exception) 
             { 
             } 
             } 
            } 
             } 
             return null; 
             } 
            /////////////////////////////////////////////////////////////////////////////// 
             public string ConvertBack(string value, DataWindowContext parameter, 
            System.Globalization.CultureInfo culture) 
             { 
             // convert Per unit to Ohm. 
             float fPU; 
             bool bOK = float.TryParse(value, out fPU); 
             if (!bOK) 
             return null; 
             string sURI = parameter.InstanceURI; 
             string[] saProp = { "cim:ConductingEquipment.BaseVoltage" }; 
             string[] saValue; 
             parameter.Database.GetClassProperties(sURI, saProp, out saValue); 
             string sBaseVoltageID = saValue[0]; 
             if (!string.IsNullOrEmpty(sBaseVoltageID)) 
             { 
             saProp[0] = "cim:BaseVoltage.nominalVoltage"; 
             parameter.Database.GetClassProperties(sBaseVoltageID, saProp, out saValue); 
             if (!string.IsNullOrEmpty(saValue[0])) 
             { 
             float fNominalVoltage; 
             bOK = float.TryParse(saValue[0], out fNominalVoltage); 
             if (bOK) 
             { 
             try 
             { 
             float fOhm = fPU * (fNominalVoltage * fNominalVoltage) / (float)100.0; 
             return fOhm.ToString(); 
             } 
             catch (Exception) 
             { 
             } 
             } 
             } 
             } 
             return null; 
             } 
             } 
            } 
```

### Custom Data Validation {#section_isq_jyf_xp}

Currently, CIMedit provides default data validation based on the XML
schema file (oracleSchema.xml or mssqlSchema.xml). For example, if a
field is defined as integer in the XML schema file, CIMedit will
validate that the data entered is only integer. If a field is defined as
float, then only floats are allowed to be entered. CIMedit will also
check for precision if it is defined for a float field. If a field is
define as text field, CIMedit will check that the text data entered is
within the length specified in the XML schema file. This is to ensure
that there will be minimal problems when the data is updated to the
database.

Custom validation is supported so that more stringent validation can be
performed such as limiting the integer data to a specified range.
CIMedit will first check the data using custom validation if available.
If the data passes custom validation checking, then CIMedit will proceed
with the default validation. Therefore, custom validation does not need
to duplicate the checking that is done by default.

If custom data conversion is present, CIMedit with call custom
validation with the data entered in the text box and then call default
validation with the converted data (since this is the data that is
actually going into the database).

The IValidator interface and \<Validator> xml tag are provided to
support custom validation. The IValidator interface is defined in the
CIMedit.Extensibilty namespace and can be reference through the
CIMedit.Extensibility.dll. The \<Validator> xml tag is to be used in the
CIMedit configuration XML file to specify the DLL and class that will be
used for data validation. The class specified in the \<Validator> tag
must implement the IValidator interface IsValid method.

``` c
                namespace CIMedit.Extensibility
                {
                public interface IValidator
                {               
                bool IsValid(string value,DataWindowContext parameter,
                System.Globalization.CultureInfo cultureInfo);
                }
                }
                <Property name="R(pu)" type="cim:Compensator.r">
                <Validator handlerAssembly="CIMeditExtensionSample"
                handler="CIMeditExtensionSample.PerUnitValidator"/>
                </Property>
                
```

The following example PerUnitValidator class validates that the data
entered is between 0 and 1. The example can be found in the
CIMeditExtensionSample .NET solution delivered under \"C:\\Program
Files\\PTI\\ODMS\\CIMedit\\CIMeditExtensionSample.\"

``` c
            using System;
            using System.Collections.Generic;
            using System.Text; 
            using CIMedit.Extensibility;
            using PTI.CIMdbNET; 
            namespace CIMeditExtensionSample
            {
             public class PerUnitValidator : CIMedit.Extensibility.IValidator
            {
            public bool IsValid(string value, DataWindowContext parameter,
            System.Globalization.CultureInfo cultureInfo)
            {
            if (string.IsNullOrEmpty(value))
            return true;
            float fValue;
            bool bOK = float.TryParse(value, out fValue);
            if (bOK)
            {
            return (fValue >= 0 && fValue <= 1);
            }
            return false;
            }
            } 
            } 
            
```

### Extending CIMedit {#section_jsq_jyf_xp}

CIMEditODMSExtension.dll contains classes that can be used to create and
delete standard CIM classes supported by PSS®ODMS through context menu
configuration in CIMedit. Here is an example of how
CIMEditODMSExtension.dll is used in a CIMedit configuration file.

``` c
            <MenuItem label="New VoltageLevel"
            handlerAssembly="CIMEditODMSExtension"
            handler="CIMEditODMSExtension.AddVoltageLevelFacade"/> 
            The class AddVoltageLevelFacade must inherit from WindowFacade 
                class defined in the CIMEdit.Extensibility project. The code
                for CIMEdit.Extensibility is delivered as part of the 
                CIMEditExtensionSample C# solution installed in: 
            C:\Program Files\PTI\ODMS\CIMedit\CIMeditExtensionSample 
            Here is the definition for AddVoltageLevelFacade class (which is also delivered
                with the CIMeditExtensionSample solution): 
            using System; 
            using System.Collections.Generic;
            using System.Text; 
            using CIMedit.Extensibility;
            using PTI.CIMdbNET; 
            using System.Windows.Interop;
            namespace CIMeditExtensionSample
            {
             class AddVoltageLevelFacade : WindowFacade
            {
            public override Implementations Implemented
            {
            get { return Implementations.Modal | Implementations.RefreshItemOnSuccess;
                }
            }
            public override bool IsVisible
            {
            get
            {
            return false;
            }
            }
            public override void Close()
            {
            }
            public void OnClosed(object sender, EventArgs e)
            {
            ForwardClosedEvent(sender, e);
            }
            public override void Show(Context ctx)
            {
            if (ctx == null)
            throw new ArgumentNullException("ctx");
            }
            public override Nullable<bool> ShowDialog(Context ctx)
            {
            if (ctx == null)
            throw new ArgumentNullException("ctx");
             Nullable<bool> retVal = false;
            try
            {
            DataWindowContext dwctx = (DataWindowContext)ctx;
            string[ ] saProperties = { "daf:URI",
                "cim:BaseVoltage.nominalVoltage" };
             string[ ][ ] saValues; 
            dwctx.Database.GetClassInstances("cim:BaseVoltage", saProperties, out
                saValues);
            SelectDropDownDataList bvList = 
            new SelectDropDownDataList();
            for (int i = 0; i < saValues.Length; i++)
            {
            SelectDropDownData bv = new SelectDropDownData();
            bv.URI = saValues[i][0];
            if (string.IsNullOrEmpty(saValues[i][1]))
             bv.Name = bv.URI;
             else 
             bv.Name = saValues[i][1]; 
             bvList.Add(bv); 
             } 
             SelectDropDownWindow _wnd = new SelectDropDownWindow(); 
             _wnd.Title = "Select Base Voltage"; 
             _wnd.labelTxt.Content = "Select a Base Voltage:"; 
             _wnd.dropDownBox.ItemsSource = bvList; 
             WindowInteropHelper wih = new WindowInteropHelper(_wnd); 
             wih.Owner = new IntPtr(dwctx.WindowHandle); 
             _wnd.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterScreen; 
             _wnd.Closed += new EventHandler(ForwardClosedEvent); 
            if (_wnd.ShowDialog() == true) 
             { 
             string bvURI = _wnd.dropDownBox.SelectedValue.ToString(); 
             string sNom = string.Empty; 
             SelectDropDownData data = _wnd.dropDownBox.SelectedItem as SelectDropDownData; 
             if (data != null) 
             sNom = data.Name; 
             // create VoltageLevel. 
             string newURI; 
             string[ ] saVLProperties = { "cim:Naming.name",
                "cim:VoltageLevel.BaseVoltage", 
            "cim:VoltageLevel.MemberOf_Substation" }; 
             string[ ] saVLValues = {(string.IsNullOrEmpty(sNom) ? "$New$" : sNom +
                " kV"), bvURI, dwctx.InstanceURI }; 
            dwctx.Database.AddExtendedResource("cim:VoltageLevel", saVLProperties,
                saVLValues, out newURI); 
             retVal = true; 
             } 
             dwctx.Close();
            }
            catch (Exception)
            {
            }
            finally
            {
            }
            return retVal;
            }
            } 
            } 
```

There are 2 functions that are important:

``` c
            public override Implementations Implemented
            {
             get { return Implementations.Modal | Implementations.RefreshItemOnSuccess;
                }
            } 
```

And:

``` c
            public override Nullable<bool> ShowDialog(Context ctx)
```

When Implementations.Modal is specified, CIMedit will call the
ShowDialog function when the context menu is clicked and will pass in an
instance of DataWindowContext class to the ctx paramenter of the
ShowDialog function. The WindowHandle property of the DataWindowContext
instance will be set to the Windows handle of the main window in
PSS®ODMS that can be used to make any window that is launched by
ShowDialog modal to the application.

Example:

``` c
            WindowInteropHelper wih = new WindowInteropHelper(_wnd);
            wih.Owner = new IntPtr(dwctx.WindowHandle);
```

The InstanceURI property of the DataWindowContext instance will be set
to the URI of the instance of the class in the configuration file to
which the context menu belongs.

Example:

``` c
            <Class type="cim:Substation"
            associationType="cim:SubControlArea.Contain_Substations"
                icon="Substation.bmp">
            <PropertyGroup key="General"/>
            <ContextMenu> 
             <MenuItem label="New VoltageLevel"
                handlerAssembly="CIMEditODMSExtension"
                handler="CIMEditODMSExtension.AddVoltageLevelFacade"/>
            </ContextMenu> 
            </Class> 
```

In this case, the InstanceURI will contain the URI of a Substation
instance. Since this InstanceURI is expected in the ShowDialog function
of the AddVoltageLevelFacade class to create a Voltage- Level under a
substation, the location of where this class can be used in the
configuration file is crucial. It must be used only in the context menu
of Substation class.

The Database property of the DataWindowContext instance is set to the
CIMdbNET instance that CIMedit is currently using. This CIMdbNET
instance can be use to create new instances to the database or request
any information needed.

All code referenced by AddVoltageLevelFacade can be found in the
CIMeditExtensionSample solution. The following classes are defined in
CIMEditODMSExtension.dll. The name of the classes should be
self-explanatory. The location in the configuration determining where
they can be used is specified below:

AddMeasurementFacade - Must be used in context menu of Terminal class.

AddLimitSetFacade - Must be used in context menu of Measurement class.

AddMeasurementValueFacade - Must be used in context menu of Measurement
class.

AddLimitFacade -Must be used in context menu of LimitSet class.

AddCurveSchedDataFacade -Must be used in context menu of any
CurveSchedule derived class.

AddRegSchedFacade - Create a RegulationSchedule for an Equipment. Must
be used in context menu of Equipment that have association to
RegulationSchedule.

AddMvarCapCurveFacade - Create a MvarCapabilityCurve for a
SynchronousMachine. Must be used in the context menu of
SynchronousMachine class.

AddSubControlAreaFacade - Create a SubControlArea. This class can be
used anywhere in the configuration file since SubControlArea is at the
top of the network hierarchy.

AddSubstationFacade -Must be used in context menu of SubControlArea
class.

AddVoltageLevelFacade -Must be used in context menu of Substation class.

AddLoadDemandSchedFacade - Must be used in context menu of
EnergyConsumer class (or derived classes such as EquivalentLoad).

AddGrossToNetMWCurveFacade - Must be used in context menu of
GeneratingUnit class (or derived classes).

AddHeatRateCurveFacade -Must be used in context menu of
ThermalGeneratingUnit class.

AddWindingFacade - Must be used in context menu of PowerTransformer
class.

AddTapChangerFacade - Must be used in context menu of TransformerWinding
class.

AddTopologicalNodeFacade - Create a TopologicalNode. Can be used
anywhere class.

AddNodeToTopoFacade - Set the ConnectivityNode\'s TopologicalNode
association. Must be used in context menu of TopologicalNode class.

The following classes must be used in context menu of VoltageLevel
class:

AddACLineFacade

AddBusbarSectionFacade

AddShuntCompensatorFacade

AddSeriesCompensatorFacade

AddEnergyConsumerFacade

AddGeneratingUnitFacade

AddHydroGeneratingUnitFacade

AddThermalGeneratingUnitFacade

AddGroundFacade

AddTransformerFacade

AddStaticVarCompensatorFacade

AddBreakerFacade

AddDisconnectorFacade

AddManualDisconnectorFacade

AddMotorDisconnectorFacade

AddFuseFacade

AddGroundDisconnectorFacade

AddLoadBreakSwitchFacade

AddBayFacade

DeleteCurveScheduleFacade - Must be used in context menu of a
CurveSchedule derived classes.

DeleteEquipmentFacade - Must be used in context menu of any Equipment
derivedclasses, e.g. Breaker, Compensator, EnergyConsumer, etc.

DeleteSubControlAreaFacade - Must be used in context menu of
SubControlArea class.

DeleteSubstationFacade -Must be used in context menu of Substation
class.

DeleteVoltageLevelFacade -Must be use in context menu of VoltageLevel
class.

DeleteBayFacade - Must be used in context menu of Bay class.
DeleteTopologicalNodeFacade - Must be used in context menu of
TopologicalNode class.

### Implementing Drag-and-Drop {#section_ssq_jyf_xp}

CIMedit supports Drag-and-Drop capabilities through the DragDropFacade
and DragDropData Classes defined in the CIMedit.Extensibilty namespace
and can be referenced through the CIMedit.Extensibility.dll. The
\<DropHandler> and \<DropItem> xml tag and \"allowDrag\" xml property is
also used in the CIMedit configuration file to specify which tree items
can be dragged and which tree items can accept a dropped item and what
to do when the the data is dropped.

Example

``` c
            <Class type="cim:LoadArea" icon="LoadArea.bmp"> 
             <DropHandler> 
             <DropItem type="cim:EnergyConsumer"
                handlerAssembly="CIMEditODMSExtension" 
            handler="CIMEditODMSExtension.MoveLoadToLoadAreaFacade"/> 
            <DropItem type="cim:CustomerMeter"
                handlerAssembly="CIMEditODMSExtension" 
            handler="CIMEditODMSExtension.MoveLoadToLoadAreaFacade"/> 
             <DropItem type="cim:EquivalentLoad"
                handlerAssembly="CIMEditODMSExtension" 
            handler="CIMEditODMSExtension.MoveLoadToLoadAreaFacade"/> 
             </DropHandler> 
            </Class>
```

The example above specifies that you can drop EnergyConsumer,
CustomerMeter, and Equivalent-Load into a LoadArea. If any other type is
dragging over a LoadArea, the cursor will reflect that the data will not
be accepted.

``` c
<Class type="cim:EnergyConsumer"
                associationType="cim:LoadArea.EnergyConsumers" icon="Load.bmp"
                enableLocateOnDiagram="true" allowDrag="true"> 
            </Class> 
            The "allowDrag" tag above shows that a EnergyConsumer item can be
                dragged in CIMedit.      
```

When an item is dropped, CIMedit will call the DoDrop function of the
class defined in the handler property of the \<DropItem> xml tag. This
class must inherit from the abstract DragDropFacade class defined in
CIMedit.Extensibility and implement the DoDrop function.

Here is the definition of DragDropFacade and DragDropData.

``` c
            using System;
            using System.Collections.Generic;
            using System.Text; 
            namespace CIMedit.Extensibility
            {
             public abstract class DragDropFacade 
            {
            public abstract bool DoDrop(DragDropData data);
            } 
            } 
            namespace CIMedit.Extensibility
            { 
             public class DragDropData
            {
            string _dragType;
            string _dragURI;
            string _dropURI;
            private CIMdb _db;
            private long _winHandle;
            public DragDropData()
            {
            }
            public string DragType
            {
            get { return _dragType; }
            set { _dragType = value; }
            }
            public string DragURI
            {
            get { return _dragURI; }
            set { _dragURI = value; }
            }
            public string DropURI
            {
            get { return _dropURI; }
            set { _dropURI = value; }
            }
            public CIMdb Database
             {
            get
            {
            if (_db == null)
            throw new InvalidOperationException("Database is not
                initialized");
            return _db;
            }
            set
            {
            if (value == null)
            throw new InvalidOperationException("Database cannot be set to
                null");
            _db = value;
            }
            }
            public long WinHandle
            {
            get { return _winHandle; }
            set { _winHandle = value; }
            }
            } 
            } 
```

A DragDropData instance will be passed to the DoDrop function and
contain the type of the drag item, the URI of the drag item, the URI of
the drop item, a CIMdbNET instance that CIMedit is currently using, and
the Windows Handle of the ODMS application. If for some reason, the move
cannot be completed in the DoDrop function, return false to notify
CIMedit that the move did not occur.

Here is an example of how to drop an EnergyConsumer into a LoadArea.

``` c
            using System; 
            using System.Collections.Generic;
            using System.Text; 
            using CIMedit.Extensibility;
            using PTI.CIMdbNET; 
            using System.Windows.Interop; 
            using CIM10dbLib; 
            using System.Windows; 
            namespace CIMEditODMSExtension 
            {
            class MoveLoadToLoadAreaFacade : DragDropFacade
            {
            public override bool DoDrop(DragDropData data)
            {
            bool retVal = false;
            if (data == null)
            throw new ArgumentNullException("data");
            try
            {
            data.Database.UpdateProperty(data.DragURI,
                "cim:EnergyConsumer.LoadArea", 
            data.DropURI);
            retVal = true;
            }
            catch (Exception)
            {
            }
            return retVal;
            }
            } 
            }             
```
