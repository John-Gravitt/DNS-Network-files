<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Part-1)</h1>
This project documents my lab practice for my CourseCareers IT Professional certification course covering the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a resource group within Azure subscription including two virtual machines, one VM running Windows Server 2022 and the other Windows 10.
- Install Active Directory on the Windows Server and promote to a domain controller.
- Create organizational units, admin accounts and user accounts.
- Join the Windows 10 virtual machine to the domain and enable user access.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/6d7d9595-524d-43ca-a825-e3608d0bfd9a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two virtual machines in Microsoft Azure. Setup one VM to be the domain controller (DC-1) and the other VM to be a domain user (Client-1). DC-1 should be imaged as a Windows Server 2022 and Client-1 should be imaged as a Windows 10 OS. Ensure that DC-1 and Client-1 are using the same virtual network. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/ea36dd19-3a7d-45ec-8c37-cae85fe5f341" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Change the domain controller’s NIC Private IP address from dynamic to static. This will be essential later on when changing the DNS server of Client-1 to the domain controller. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/a45dabdf-bf1e-4ddf-af05-c0c31f627f06" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with perpetual ping. Notice that the ping fails. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/083f1b85-6a97-45f6-ba73-a587a3c7b468" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to DC-1 with Remote Desktop and open Windows Defender Firewall with advanced security. Enable the ICMPv4 echo request in the local Windows firewall. Observe that the ping request from Client-1 succeeded.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/8927c558-a086-485f-af9e-da2ecce8f8ad" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1, open Server Manager to install Active Directory. Click add roles and features to begin installation and follow the steps. After installation, promote the server as a domain controller.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/b96866af-c1a8-4eff-9bb6-72211573a30d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Under tools, search for Active Directory Users and Computers then set up a new forest as mydomain.com and set a password. The server will then need to be reset.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/4eec3ed5-42fc-4e81-a208-d1d53e7c2a3b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1, open Active Directory Users and Computers. Then create two new organizational units and a new admin account. Logout of server and rejoin as the new admin account. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/5ccf105a-63c9-4ec8-8a03-7ad85db7bf70" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address and restart Client-1. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/feec8ac7-6a95-4390-9030-a5c1a78dffbe" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 and join it to the domain. Then restart the VM. Add domain users to romote desktop.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/cc430c05-7f98-48f3-9c45-9c16bbfbf283" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1, open PowerShell ISE as an administrator. Create a new file and use a downloaded script to generate thousands of user accounts on the domain. Observe that the new user accounts are now in Active Directory.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/configure-ad/assets/152338722/9723dff2-7add-4588-9b1b-966edf0dcc78" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Attempt to log into Client-1 with one of the generated user accounts. Clean up the lab by deleting the resource groups or proceed to the next lab.
</p>
<br />
