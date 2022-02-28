# PSS®ODMS Licensing

## CodeMeter Method (NEW)

PSS®ODMS 12.0 introduces a new CodeMeter-based software licensing
mechanism, consistent with the technology used in current versions of
PSS®E. For further information on obtaining a CodeMeter license, please
contact Siemens PTI Software Support and refer to the supplemental \"PTI
License Manual\" document.

## Traditional Method

PSS®ODMS uses an encrypted file-based software licensing mechanism to
register the application and enable specific features corresponding to
the modules authorized for delivery. Each PSS®ODMS workstation needs to
be registered accordingly. There are two different deployment approaches
for traditional licensing: Individual Workstation and Network.

### Individual Workstation Licensing

Individual workstation licensing is recommended for PSS®ODMS Single-user
Edition (or a demo version). It involves the following steps:

1.  Obtaining a license file from Siemens PTI which is configured with
    the REG ID of one or more individual workstations. The REG ID for
    each workstation must be provided to Siemens PTI Software Support.

2.  Registering each PSS®ODMS workstation with the obtained license
    file. Whenever a workstation is added or replaced, an updated
    license file must be requested from Siemens PTI Software Support.

### Network Licensing

Network licensing recommended for PSS®ODMS Standard or Enterprise
Edition and is required when deploying a PSS®ODMS application server. It
provides the flexibility to install and register PSS®ODMS on an
unlimited number of machines (physical or virtual) and to add or replace
workstations as often as needed without having to obtain a new license
file from Siemens PTI. For occasional off-network use of PSS®ODMS, the
license Check Out feature can be used as needed. Setting up network
licensing is a one-time process involving the following steps:

1.  Installing the Siemens License Server and PTI License Tool software
    on a networked Windows server (potentially also hosting the PSS®ODMS
    database) and testing the client-server connection.

2.  Obtaining a network license file from Siemens PTI which is
    configured with the MAC ID of this server.

3.  Registering all PSS®ODMS workstations with the network license file,
    which is fully reusable for registering additional workstations at
    any time going forward.

#### Network Licensing Setup

The Siemens License Server (a Windows service) enables network licensing
for multiple running instances of PSS®ODMS on the same network. The
Siemens PTI License Tool (a standalone application) is used for
configuration and testing.

**Installation Procedure**

1.  Designate a Windows server machine on your network to host the
    Siemens License Server software. This machine must be accessible to
    all PSS®ODMS workstations via LAN connection. The same Windows
    server which hosts the PSS®ODMS database is often used for
    convenience (although it is important to note that license server
    and database connections are completely independent).

2.  Download SetupLicenseServer.msi and SetupLicenseTool.msi from the
    PSS®ODMS support website (www.usa.siemens.com/odms-support) and copy
    both files to the server machine.

3.  Run SetupLicenseServer.msi and follow the installation prompts to
    install the Siemens License Server.

4.  Locate \"Siemens License Server\" in the Windows Services list and
    verify that the service is started.

5.  Run SetupLicenseTool.msi and follow the installation prompts to
    install the Siemens PTI License Tool.

**Testing the Connection**

1.  Install and run the Siemens PTI License Tool on any PSS®ODMS
    workstation.

2.  Select the Server tab and enter the name of the designated network
    license server machine.

3.  Click the Test Connection button and observe the status information
    displayed in the box below, which should indicate a successful
    connection.  
    ![](/images/Server_Lic6.png)

**Obtaining and Using a Network License**

1.  Run the Siemens PTI License Tool on the designated license server
    machine.

2.  Copy the MAC ID and Computer Name displayed in the Computer
    Information section of the System tab into an email request to
    pti.support.energy\@siemens.com along with your company information.
    ![](/images/Server_Lic7.png)

3.  Copy the provided network license (.bin) file to a local directory
    on each PSS®ODMS workstation.

4.  Follow the steps in the next section to register each PSS®ODMS
    workstation.

**License Server Redundancy**

To deploy a high-availability network licensing environment, simply
install the Siemens License Server on two different server machines and
provide the information for both servers when requesting a network
license file.

### Registering PSS®ODMS

Each PSS®ODMS workstation or application server must be registered with
a valid license (.bin) file to enable the features of the product.

1.  Run PSS®ODMS using the desktop icon or Start menu command.

2.  A message box may indicate that a license file could not be found.
    Click the OK button to dismiss the message box.

3.  Choose the Help>Register menu command to launch the PSS®ODMS License
    Management dialog. ![](/images/LicMang.png)

4.  FOR INDIVIDUAL WORKSTATION LICENSING ONLY: To obtain an individual
    workstation license file, copy and paste the displayed REG ID string
    into an email to pti.support.energy\@siemens.com along with your
    company information. Upon receipt of the license file, copy it to a
    local directory.

5.  Click the Locate button and select the network or individual
    workstation license (.bin) file provided by Siemens PTI Software
    Support.

6.  After restarting PSS®ODMS, choose the Help>Register menu command to
    again launch the PSS®ODMS License Management dialog and verify that
    the displayed license file and enabled modules information is
    correct.

**Additional Considerations**

After successful registration, be aware that certain PSS®ODMS commands
may still be disabled for a variety of reasons unrelated to licensing
such as an open database connection to a valid PSS®ODMS model, the CIM
version of the database model, role-based user privileges, whether a
study case is in memory, currently active mode(s), etc. Refer to the
PSS®ODMS User Manual for further information.
