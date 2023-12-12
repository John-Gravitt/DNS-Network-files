<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>DNS and Network File Sharing Using Active Directory within Azure VMs (Part-2)</h1>
This project documents my lab practice for the CourseCareers IT Professional certification course covering the utilization of Active Directory for DNS and file sharing and permissions.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 

<h2>High-Level Deployment and Configuration Steps</h2>

- Inspect and create DNS A-records from the domain controller and observe on a client machine
- Observe changes when deleting records from the server and clearing the DNS cache 
- Create files with permissions on the server
- Grant access to files for various user types

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/ccefcf86-6ec0-4775-a46a-806b1221ffa3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use the virtual machines created in the previous lab, DC-1 and Client-1, to complete this project. Log into both VMs with the admin account that was created. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/cad6857c-34e8-4c7d-9652-bc22a055514f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From Client-1, ping and nslookup “mainframe” and notice that it fails.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/1797bb39-fa58-46aa-9bd9-36bb8113b098" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a DNS record for “mainframe” on DC-1 using a made up IP address. 
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/4f3443fb-fd9f-4898-bf8e-9b50b7f36283" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 and notice that “mainframe” is able to be pinged and in nslookup.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/46756fc9-8876-48e7-bb42-be8ca3ed04d4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to DC-1 and change mainframe’s record address to 8.8.8.8
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/7c54c1e0-975c-43bf-84d7-689ffc588b9e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address. Observe the local dns cache. (ipconfig /displaydns) Flush the DNS cache. (ipconfig /flushdns) In Client-1, ping “mainframe” again. Observe the address of the new record is showing up.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/2f524064-33a9-40d3-a6eb-a5f7f937c7d6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/7f040ec3-bb1e-4dee-8314-fb2c464a7c24" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/702d4ffe-3ce4-465e-ac0e-db91da9c232c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to DC-1 and locate the C:\ drive. Create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”. Set the following permissions (share the folder) for the “Domain Users” group:
Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/f230e839-3431-4816-ac27-27b7068e39a9" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 as <someuser> in the active directory and locate the file path via \\dc-1. Observe the folders that were created and the user’s access to each.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/1b736434-9de6-4bed-a087-319d1e9de805" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/ea9b5bcf-b93e-4a4a-86a6-fc9546e469c0" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the “accounting” folder created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/d7b2882a-f704-4385-b14d-9d11f658908e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, as  <someuser>, try to access the accountants folder. It should fail. Log out of Client-1.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/54b570f8-c388-4c2d-b7a4-e7a74f58b70a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/eeac08ec-e761-47df-a8a5-4ba48a4441b3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign back into Client-1 as <someuser> and try to access the “accounting”. Observe that the user has access to the folder now.
</p>
<br />

<p>
<img src="https://github.com/John-Gravitt/DNS-Network-files/assets/152338722/0f7c3331-875b-48bd-8847-15b35f4d4785" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Clean up the lab by deleting the resource groups.
</p>
<br />
