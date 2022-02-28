# Nonlinear Tap Changers

# Introduction

Transformers are sometimes built with tap changers where the voltage
ratio changes between each step are not uniform. In most cases the ratio
difference between each step is small enough to have a negligible effect
in the power flow results. For those few transformers where the voltage
ratio change between each step is so inconsistent as to cause error in
the power flow results, a table must be constructed. The same non-linear
tap table may also be used to create a more accurate transformer model
by modifying the impedance of the transformer as the tap position
changes.

# Modeling Nonlinear Tap Changers

Nonlinear tap changers may be modeled using a RatioTapChangerTabular
instance. In CIMedit navigate to the appropriate RatioTapChanger item.
Right click on the RatioTapChangerTabular item and select the \"New
RatioTapChangerTabular\" context menu command.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_182.png)

Right-click on the new RatioTapChangerTabular item and select the \"New
RatioTapChangerTabularPoint\" context menu command. Repeat until the
number of data points equals the number of tap positions of the
TapChanger.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_183.png)

Individually select each RatioTapChangerTabularPoint and enter the step
(tap position) and ratio (in per unit of base voltage) values. Note that
the R and X deviation values are entered in percentage of their nominal
values (when tap is at neutral position), and the G and B values will
not be used by the Build Case function.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_184.png)

## Nonlinear Table Data Validity

If a RatioTapChangerTabularPoint ratio value is null or 0, the
corresponding turns ratio for that tap position will be defaulted to the
ratio of the PowerTransformerEnd Rated kV to its base voltage.
RatioTapChangerTabularPoint R values may be null or 0. X values must be
greater than zero.

# Nonlinear Tap Changers in Network Analysis

RatioTapChangerTabular data entered into the model via CIMedit as
described above will be included in subsequent case builds. The
corresponding Transformer will have an associated nonlinear data table.
Each record in the table corresponds to one of the
RatioTapChangerTabularPoints in CIMedit. This table may be viewed from
the Device Settings dialog or by double clicking a non-empty Nonlinear
Data Table cell in the far right hand column of the Transformers
spreadsheet view.

![](/images/PSSODMS_UserManual_2014-10-17114243_img_185.png)

When the Current Tap value changes (either manually or via State
Estimator), the corresponding Turns Ratio, Resistance and Reactance
values are updated accordingly from the table data. The updated values
affect the Power Flow and State Estimator results.
