
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory Infrastructure in Azure (Azure)</h1>
This tutorial outlines the process of setting up a domain controller and a client virtual machine in Azure, which will be used to deploy and test Active Directory Domain Services (AD DS) within a virtualized environment.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Windows PowerShell
- Windows Firewall Defender

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro

<h2>High-Level Deployment and Configuration Steps</h2>

- Deploy Domain Controller (DC-1) in Azure
- Deploy Client Virtual Machine (Client-1) in Azure
- Configure and Test Network Connectivity Between Client-1 and DC-1
- Verify Network and DNS Settings

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%201.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%202.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Before creating the virtual machines, it's best to start by creating a resource group. A resource group in Azure helps organize and manage all resources associated with your virtual machines.
</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%203.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%204.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%205.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%206.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%207.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This virtual machine will serve as a domain controller and will be named DC-1.
To create the virtual machine, first ensure it is attached to the previously created resource group. Then, fill in the required configuration details, including:

- Name: Set the VM name to DC-1.


- Region: Choose the appropriate Azure region based on your location or organizational requirements.


- Availability Zone (if prompted): Select a zone for high availability, if required.


- Image: Use the Windows Server 2022 image.


- Size: A VM size with at least 2 vCPUs is recommended to maintain stable performance, especially during Remote Desktop sessions.


- Administrator account: Set a username and password for RDP (Remote Desktop Protocol) access.


- Virtual Network: I used Active-Directory-vnet as the primary virtual network to enable communication between the domain controller and the client VM.
</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%208.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%209.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After deploying the virtual machine (DC-1), it will be assigned a dynamic private IP address by default. However, domain controllers require a static IP address to ensure consistent network communication and DNS resolution.
To change the IP address to static:
- Navigate to the network interface (NIC) associated with the VM.


- In the IP configurations settings, locate the private IP address.


- Change the allocation method from Dynamic to Static.


- Save the changes.
</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2010.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2011.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2012.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2013.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2014.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
At the end of the setup, we’ll test connectivity between the domain controller (DC-1) and the client VM (Client-1). For lab purposes only, it may be necessary to temporarily disable the firewall to allow unrestricted communication between the two machines.
To disable the Windows Defender Firewall on DC-1:

- Connect to DC-1 via Remote Desktop.


- Right-click the Start menu (bottom-left corner) and select Run.


- Type "wf.msc" and press Enter. This opens the Windows Defender Firewall with Advanced Security console.


- In the left pane, click Windows Defender Firewall Properties.


In the window that appears, set the Firewall State to Off for the following profiles:


- Domain Profile


- Private Profile


- Public Profile


Click Apply, then OK to save the changes.
</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2015%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2016%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2017%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2018%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2019%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we’ll create a second virtual machine named Client-1, which will act as the client in this domain environment.
Most of the configuration settings will mirror those used for DC-1, including:

- Resource Group: Use the same resource group created earlier.


- Availability Zone: Use the same zone (if applicable).


- Size: Choose the same VM size (e.g., 2 vCPUs) for consistency.


- Virtual Network: Use Active-Directory-vnet to ensure the two VMs are on the same network.


The key differences are:

- Name: Set the VM name to Client-1.


- Image: Use Windows 10 Pro as the operating system, which supports domain joining.
</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2020%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2021%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After completing the initial setup of Client-1, we need to update its DNS settings to ensure it can locate and communicate with the domain controller (DC-1).
By default, Azure virtual machines use Azure’s internal DNS servers, which do not recognize your custom domain environment. To fix this, we need to point Client-1 to the private IP address of DC-1 as its DNS server.
To do so follow these steps:

- Navigate to the network interface (NIC) of Client-1 in the Azure portal.


- Under DNS servers, select Custom.


- Enter the private IP address of DC-1 (the domain controller).


- Save the settings.


This change ensures that Client-1 queries DC-1 for DNS resolution, allowing it to find and join the Active Directory domain.

</p>
<br />

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2022%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2023%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2024%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://github.com/SamuelC233/configure-ad-vm/blob/main/Screenshot%2025%20c1.jpg?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, we will test network connectivity between Client-1 and the domain controller (DC-1).

- To do so remote into Client-1, open PowerShell, and run the following command: "ping 10.0.0.4"

⚠️ Note: 10.0.0.4 will need to be replaced with the actual private IP address of DC-1, as it may vary depending on your setup.
A successful ping response indicates that Client-1 can reach DC-1 over the network and that the network settings are configured correctly.


- To further verify DNS configuration, run: "ipconfig /all"

- Then, look under the DNS Servers section. It should list the private IP address of DC-1 as the DNS server.


This confirms that Client-1 is using the domain controller for DNS resolution, which is a required step before joining it to the domain.
</p>
<br />

