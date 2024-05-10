<H1>SOC Lab at Home</H1>

<H2>Utilities</H2>

- Virtual Machine: Oracle VM. Great for testing in an isolated environment for security purposes.

- pfsense: open-source firewall and router. In this lab environment, can be used to simulate network traffic, enforce firewall rules, and monitor network acitivity.

- Active Directory(AD): Centralized Management directory service by microsoft. Great for managing users and groups.

- Sysmon: Service that logs system activity in Windows event log.

- CrowdSec: open-source security automation that helps to detect and respond to security threats in real-time.

<h2>Downloading pfSense</h2>

<p align="center">
<img src="https://imgur.com/av86i1W.png" height="80%" width="80%"/>

Download <a href="https://www.pfsense.org/download/">pfSense</a> ISO, you will need to sign up on the pfSense website and provide your email address, personal information, and phone number. After signing up, you'll be directed to the Netgate installer, where you can choose the installation image option. I elected to download the amd64.ISO.

If you downloaded the ISO, you'll need to follow a decompression method before you can use it. You can find instructions for this on the <a href="https://docs.netgate.com/pfsense/en/latest/install/prepare-installer-media.html">pfSense documentation website</a> 

<h2>Deploying pfSense on Virtual Box</h2>

<p align="center">
<img src="https://imgur.com/6jya4ob.png" height="80%" width="80%"/>

If you haven't, download <a href="https://www.virtualbox.org/wiki/Downloads">Oracle<a/> VirtualBox or your preferred virtualization software. Moving forward, I will be using Oracle. Set up a new instance, selecting "BSD" type and "FreeBSD (64-bit)" version. Allocate necessary resources, then in the pfSense settings, enable network adapters 2 and 3 with internal perferences, naming them as desired. In my case, I name adapter 2(Internal) and adapter 3(dmz). Note the MAC addresses and enable Promiscuous mode to allow the VM to view all network traffic on the segment.

<h2>Installing and Configuring pfSense</h2>

<p align="center">
<img src="https://imgur.com/AoaebXe.png" height="80%" width="80%"/>

Select install and follow the prompt, once finished, time to configure the interfaces. select 1 assign Interfaces. then select 2 to configure the IP address, leave the WAN interface as DHCP, select 2 to change the LAN interface, assign IP and subnet(your choice).


<h2>Installing Active Directory</h2>

<p align="center">
<img src="https://imgur.com/VE3ZCqv.png" height="80%" width="80%"/>

Download the <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022<a/> ISO from Microsoft's website, providing required personal information and a phone number. Create a new virtual machine instance, selecting "Windows" and "Version 2019 (64-bit)," and allocate resources accordingly. In the VM settings, set the network attachment to "internal" and choose the desired network. Launch the VM and mount the ISO onto it. Begin installation, selecting the "Windows Server 2022 Datacenter Evaluation (Desktop Experience) edition", opting for "Custom" installation, and installing the operating system only on the designated drive. Create a password during setup. Upon completion, the system will reboot automatically.

<h2>Configuring Windows</h2>

<p align="center">
<img src="https://imgur.com/e86Hwbn.png" height="80%" width="80%"/>

Connect to the administrator account and access the settings, then proceed to the "network and internet settings". Navigate to "Change adapter options" and select the desired network adapter's properties. Within the properties window, locate "Internet Protocol Version 4 (TCP/IPv4)" and assign a specific IP address. Ensure the assigned IP matches the gateway set in the LAN interface of pfSense. Optionally, rename the server, then restart the virtual machine (VM) to implement the changes.

<h2>Installation of Active Directory</h2>

<p align="center">
<img src="https://imgur.com/v2yGKM3.png" height="80%" width="80%">

To begin, log in to your administrator account and open the "Add roles and features" menu. Choose a role-based installation and select your server from the available options. Add "Active Directory Domain Services" as a role and leave other Windows settings at their default configurations. Once the installation is complete, proceed to "promote this server to a domain controller".

<h2>Adding new Active Directory Forest</h2>
A flag icon will be on the top, click on it and "add new active directory forest", leave default configurations and give a password, leave dns defaulf and check the netbios name, launch and restart.

<h2>Bad Blood</h2>

<p align="center">
<img src="https://imgur.com/BqqBYaj.png" height="80%" width="80%"/>

To populate the Active Directory (AD) server with misconfiguration for analysis, follow these steps: Download <a href="https://github.com/davidprowe/BadBlood">BadBlood</a> onto the AD server and extract the files. Launch PowerShell as an administrator and navigate to the BadBlood folder. Execute the script "Invoke-BadBlood.ps1" and allow it to run; this process may take several minutes.

<h2> Download and Install Windows 10</h2>

Download <a href="https://go.microsoft.com/fwlink/?LinkId=691209">Windows 10</a> iso, create a new virtual machine, allocate resources, then in setting, network configure adapter 1 as internal. then mount the iso on the vm.


Go through the installation process, install now, i dont have a product key, if you dont have one. select windows 10 pro version, accept license, and select custom install, select the only drive, then select i dont have internet and continue with limited set-up. name it and set your password and no to the other options.

<h2>Configuration of Windows 10</h2>

<p align="center">
<img src="https://imgur.com/HiXRSUX.png" height="80%" width="80%"/>

Access your administrator account and navigate to "Open Network & Internet Settings." Proceed to modify the adapter options and select your card properties. Then, navigate to "Internet Protocol Version 4" and open its properties to assign an IP gateway as your LAN Interface set-up in pfSense. Verify connectivity with ping. Next, rename the server as desired through the setting menu, then "About," and select "Rename this PC." Finally, restart your VM to apply the changes.

<h2>Add your windows 10 workstation to the domain</h2>

<p align="center">
<img src="https://imgur.com/QpU4VWJ.png" height="80%" width="80%"/>

Access the advanced system settings and choose "Change," Select "Domain," and input the NetBIOS domain obtained earlier. Enter your administrator domain account credentials, then restart the system.

<h2>Download and Configure Sysmon</h2>

<p align="center">
<img src="https://imgur.com/vgGdaYr.png" height="80%" width="80%"/>

Download <a href="https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon">Sysmon</a> and extract. 

If interested, you can download a <a href="https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml">configuration file</a> on github and lauch in powershell in administrator account. use the command "sysmon.exe -accepteula -i YOURFILE.xml".

<h2>Installing CrowdSec</h2>

<p align="center">
<img src="https://imgur.com/wAGHWlH.png" height="80%" width="80%"/>

To install CrowdSec on Windows, download the .msi installer from GitHub, then follow the installation prompts. 

<p align="center">
<img src="https://imgur.com/4BWqerm.png" height="80%" width="80%"/>
  
Next, in PowerShell, navigate to the CrowdSec folder and run .\cscli collections install crowdsecurity/windows-firewall to enable additional detection capabilities. Adjust the acquis.yaml file in "C:\ProgramData\CrowdSec\config" as needed, and reboot your system for the changes to take effect.

<p align="center">
<img src="https://imgur.com/5P6LYgT.png" height="80%" width="80%"/>

For Crowdsec to enable blocking, install the Windows Firewall Bouncer from GitHub, open it, and follow the installation process. Once done, you're all set!




