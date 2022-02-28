# OPCsync Setup

## Overview

This chapter provides instructions for deploying OPCsync, the OPC client
service that connects PSS®ODMS to an external OPC server interface using
DA, HDA or UA protocols.

## OPCsync

### Install OPCsync

1.  Install OPCsync by running SetupOPCsync.msi.

    (Note: Use OPCsync version 11.6.1 for PSS®ODMS versions 11.6 or
    later versions. Use OPCsync version 9 for PSS®ODMS versions earlier
    than 11.6.)

2.  Make sure PTI OPCsync is running in Windows services.

### Configuration

OPCsync configuration is stored in the config file "OPCsync.exe.config"
located in the installed OPCsync directory.

In the configuration file, host address associated with service name
should be correctly specified for any services required such as
(Simulation, OPC DA, OPC HDA or OPC UA). The host address as well as
port number should point to the correct measurement server. Normally,
OPCsync is installed in the measurement server and in such cases host
address is localhost.

Here are few examples of the config file entry for simulation and OPC DA
services.

``` XML
        <services>
            <service name="OPCsync.SimulationServer">
                <host>
                    <baseAddresses>
                        <add baseAddress="net.tcp://localhost:8001/OPCsync"/>
                    </baseAddresses>
                </host>
                <endpoint name="SimulationServer"
                          address="SimulationServer"
                          binding="netTcpBinding"
                          bindingConfiguration="NetTcpBinding_IOPCsync"
                          contract="OPCsync.IOPCsync">
                    <identity>
                        <dns value="localhost"/>
                    </identity>
                </endpoint>
            </service>
            <service name="OPCsync.OpcDaServer">
                <host>
                    <baseAddresses>
                        <add baseAddress="net.tcp://localhost:8001/OPCsync"/>
                    </baseAddresses>
                </host>
                <endpoint name="OpcDaServer"
                          address="OpcDaServer"
                          binding="netTcpBinding"
                          bindingConfiguration="NetTcpBinding_IOPCsync"
                          contract="OPCsync.IOPCsync">
                    <identity>
                        <dns value="localhost"/>
                    </identity>
                </endpoint>
            </service>
      
      
```

Other application settings such as (Timer intervals, Switch open/close
stings) are also defined in the configuration file. If you are upgrading
from OPCsync 9 to OPCsync 11, these values can also be found in the
OPCsync 9 GUI.

![OPCsync 9 GUI. The OPCsync 11 configuration file could be populated
from the entires of OPCsync 9 GUI settings.](/images/OPC9_GUI.PNG)

``` XML
    <applicationSettings>
        <OPCsync.Properties.Settings>
            <setting name="ProcessInterval" serializeAs="String">
                <value>300</value>
            </setting>
            <setting name="TriggerDelay" serializeAs="String">
                <value>20</value>
            </setting>
            <setting name="UpdateRate" serializeAs="String">
                <value>15</value>
            </setting>
            <setting name="StringOpen" serializeAs="String">
                <value/>
            </setting>
            <setting name="StringClosed" serializeAs="String">
                <value/>
            </setting>
            <setting name="BypassServerStatus" serializeAs="String">
                <value>False</value>
            </setting>
            <setting name="OPCDAServer" serializeAs="String">
                <value>opcda://localhost/Opc.DA.Server.1</value>
            </setting>
            <setting name="OPCHDAServer" serializeAs="String">
                <value>opchda://localhost/Opc.HDA.Server.1</value>
            </setting>
            <setting name="OPCUAServer" serializeAs="String">
                <value>opc.tcp://OPC:53530/OPCUA/SimulationServer</value>
            </setting>
            <setting name="OPCUAServerUseSecurity" serializeAs="String">
                <value>False</value>
            </setting>
        </OPCsync.Properties.Settings>
    </applicationSettings>
      
      
```

## PSS®ODMS configuration

The address of the OPCsync server and port number is specified in
ODMS.exe.config file located in the ODMS directory. Here are the
examples of the address entry for simulation server and OPC DA server.

``` XML
    <client>
      <endpoint address="net.tcp://localhost:8001/OPCsync/SimulationServer"
                binding="netTcpBinding" bindingConfiguration="OPCsyncServer"
                contract="OPCsync.IOPCsync" name="SimulationServer">
      </endpoint>
      <endpoint address="net.tcp://localhost:8001/OPCsync/OpcDaServer"
                binding="netTcpBinding" bindingConfiguration="OPCsyncServer"
                contract="OPCsync.IOPCsync" name="OpcDaServer">
      </endpoint>
      
      
```

The server name could be specified/changed in Analysis Options -- OPC
tab. The port number is taken from the port number specified in
ODMS.exe.config file.

![Analysis Option - OPC setting. The server name could also be specified
in the server field.](/images/Analysis_Option_OPC.PNG)

## Windows Firewall

The Windows Firewall in the OPCsync server and in the PSS®ODMS client
may block the connection between OPCsync and PSS®ODMS. For
troubleshooting purpose, Windows Firewall could be temporary turned off
to rule out blocking by the firewall if this is allowed by your
corporate security policy. In some cases where the machines are
sufficiently protected behind a corporate firewall, disable individual
firewall could be possible, please consult with your corporate network
security expert regarding possible firewall settings.

### Configuring the Firewall

Unblock OPCsync in the firewall of the OPCsync server and PSS®ODMS in
the client machine's firewall. To unblock a program in Windows Defender
Firewall, click on "Allow an app or feature through Windows Defender
Firewall" and click on "Allow another app" button. Add OPCsync program
(in the OPCserver) and PSS®ODMS program (in the machines where PSS®ODMS
clients is installed).

![Windows Defender Firewall.](/images/FirewallWindows.PNG)

![Adding OPCsync and PSS®ODMS as allowed app by the Windows Defender
Firewall.](/images/FirewallOPC_ODMS.PNG)

OPCsync server also connects to the measurement server (such as ICCP,
PI) to get the measurements. There might be additional firewall settings
required so that the OPCsync server can connect to these measurement
servers. Please refer to your OPC server vendor\'s installation guide
for any additional configuration needed.

## Testing Measurement updates

1.  Launch PSS®ODMS, open model and build a case by selecting Analysis-
    Build Case menu command. Make sure "Include measurements associated
    with enabled sources" is checked and both "Analog" and "Status" are
    checked

    ![Check "Include measurements associated with enabled sources" in
    build case option window to include measurements in the
    case.](/images/BuildCaseOption1.PNG)

2.  Check subscription ID in Measurement sheet (Menu option View --
    Measurements Sheet). Make sure \"Hide subscription ID prefixes\" is
    unchecked in operator Display setting. The subscription ID with the
    prefixes are used to determine the measurement from the measurement
    server.

    ![Measurement sheet.](/images/MeasurementSheet.PNG)

    ![Uncheck \"Hide subscription ID prefixes\" in Display Settings to
    view subscription ID prefixes in the Subscription ID column of the
    Measurement Sheet.](/images/DisplaySettings.PNG)

3.  Make sure Analysis-Measurement-Enable OPCsync is checked

    ![Enable OPCsync](/images/EnableOPCsync.PNG)

4.  In the Analysis Options dialog, OPC tab, specify the Server and
    click on the Connect button to test the OPC client-server
    connection. The Status box should indicate \"Connected to OPCsync\"
    and the button text should change to \"Disconnect.\"

    ![Testing the OPCsync Connection](/images/ServerConnect.PNG)

5.  Switch to real time mode (Analysis-Realtime mode) and check if the
    measurements are subscribed and updated.

Note: If there is issue connecting to measurement, please check the
windows event log of the OPCsync server for any error message from
OPCsync service.

In addition, switch to Simulation Method in Analysis Options and check
measurement updates. OPCsync sends simulated measurement values in this
mode which is good to troubleshoot the connection between PSS®ODMS and
OPCsync. This simulation method is only for testing purposes and should
not be used in Normal operations as measurement values are simulated and
not real measurement values.

![Use simulation (OPC DA) Method to test connection with OPCsync server
using simulated measurement.](/images/SimulationOPCDA.PNG)
