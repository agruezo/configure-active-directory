<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (activedirectoryproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a manu additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Setup Resources in Azure</h3>
<br />
<p>
  Create the Domain Controller VM (Windows Server 2022) named “DC-1”:
</p>
<p>
  Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<p>
  Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
  Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher
</p>
<br />
<br />
<h3 align="center">Ensure Connectivity between the client and Domain Controller</h3>
<br />
<p>
  Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping):
</p>
<p>
  Login to the Domain Controller and enable ICMPv4 in on the local windows firewall:
</p>
<p>
  Check back at Client-1 to see the ping succeed:
</p>
<br />
<br />
<h3 align="center">Install Active Directory</h3>
<br />
<p>
  Login to DC-1 and install Active Directory Domain Services:
</p>
<p>
  Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is):
</p>  
<p>
  Restart and then log back into DC-1 as user: mydomain.com\labuser:
</p>
<br />
<br />
<h3 align="center">Create an Admin and Normal User Account in AD</h3>
<br />
<p>
  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”:
</p>
<p>
  Create a new OU named “_ADMINS”:
</p>
<p>
  Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”:
</p>
<p>
  Add jane_admin to the “Domain Admins” Security Group:
</p>
<p>  
  Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”:
</p>
<p>
  User jane_admin as your admin account from now on:
</p>
<br />
<br />
<h3 align="center">Join Client-1 to your domain (mydomain.com)</h3>
<br />
<p>
  From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address:
</p>
<p>
  From the Azure Portal, restart Client-1:
</p>
<p>
  Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart):
</p>
<p>
  Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain:
</p>
<p>
  Create a new OU named “_CLIENTS” and drag Client-1 into there:
</p>
<br />
<br />
<h3 align="center">Setup Remote Desktop for non-administrative users on Client-1</h3>
<br />
<p>
  Log into Client-1 as mydomain.com\jane_admin and open system properties:
</p>
<p>
  Click “Remote Desktop”:
</p>
<p>
  Allow “domain users” access to remote desktop:
</p>
<p>
  You can now log into Client-1 as a normal, non-administrative user now:
</p
<p>
  Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab):
</p>
<br />
<br />
<h3 align="center">Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>
<br />
<p>
  Login to DC-1 as jane_admin:
</p>
<p>
  Open PowerShell_ise as an administrator:
</p>  
<p>  
  Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1):
</p>
<p>
  Run the script and observe the accounts being created:
</p>
<p>
  When finished, open ADUC and observe the accounts in the appropriate OU and attempt to log into Client-1 with one of the accounts (take note of the password in the script):
</p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
