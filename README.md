<H1>SOC Lab at Home</H1>

<H2>Utilities</H2>

- Virtual Machine: Oracle VM. Great for having a testing in an isolated environment for security purposes.

- pfSense: open-source firewall and router. In this lab environment, can be used to simulate network traffic, enforce firewall rules, and monitor network acitivity.

- Active Directory(AD): Centralized Management directory service by microsoft. Great for managing users, groups, and computers.

- Sysmon: Service that logs system activity in Windows event log.

- CrowdSec: open-source security automation that helps to detect and respond to security threats in real-time.

<h2>Downloading pfSense</h2>

<p align="center">
<img src="https://imgur.com/av86i1W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

To download <a href="https://www.pfsense.org/download/">pfSense</a> ISO, you'll now need to sign up on the pfSense website and provide your email address, personal information, and phone number. After signing up, you'll be directed to the Netgate installer, where you can choose the installation image option, select the amd64.iso, and download it.

Once you have downloaded the ISO, you'll need to follow a decompression method before you can use it. You can find instructions for this on the <a href="https://docs.netgate.com/pfsense/en/latest/install/prepare-installer-media.html">pfSense documentation website</a> 

<h2>Deploying pfSense on Virtual Box</h2>

<p align="center">
<img src="https://imgur.com/6jya4ob.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  If you haven't already, download <a href="https://www.virtualbox.org/wiki/Downloads">Oracle<a/> VirtualBox or your preferred virtualization software. Set up a new instance, selecting BSD type and FreeBSD (64-bit) version. Allocate necessary resources, then in the pfSense settings, enable network adapters 2 and 3, naming them as desired. Note their MAC addresses and enable Promiscuous mode to allow the VM to view all network traffic on the segment.

<h2>Installing and Configuring pfSense</h2>

select install and follow the prompt, once finished, time to configure the interfaces. select 1 assign Interfaces. then select 2 to configure the IP address, leave the WAN interface as DHCP, select 2 to change the LAN interface, assign IP and subnet(your choice) and gateway "none."


<h2>Installing Active Directory</h2>

Download <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022<a/>, requires personal information input and phone number, after download the iso. Create a new instance, type Window, Version 2019 (64-bit), then allocate your resources. Once completed, go to your Windows Server 2022 setting and in the network tab, change your attached to internal and select one(or name you chose). then launch your Windows Server VM and mount the Iso on the VM.





To begin, initiate the installation process for Windows. When prompted, select the Windows Server 2022 Datacenter Evaluation (Desktop Experience) edition. Opt for the "Custom" installation option, then choose "Install Microsoft Server operating system only" from the provided choices. Next, designate the specific drive where you want to install the operating system. Allow the installation process to complete, and the system will automatically reboot. During the setup, be sure to create a password that you will easily remember for future access and security purposes.

<h2>Configuring Windows</h2>






