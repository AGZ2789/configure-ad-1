<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

![](https://i.imgur.com/waxVImv.png)

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
- [<b>Simple List</b>](https://docs.google.com/document/d/1qlQqPEWBcLb1zf4SHhA6phyO9269GnuP8oIXJFi7hsc/edit)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<h2>Setup Resources in Azure</h2>
  
- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
  - Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
- Set Domain Controller’s NIC Private IP address to be static
- Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create Resource Group (AD-Lab) + Virtual Machine (DC-1)</h2>

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_16-53-01](https://github.com/AGZ2789/configure-ad-1/assets/84995125/f76dc298-595b-464c-b0de-0ff7f284be7d)

![Snipaste_2024-05-18_16-55-51](https://github.com/AGZ2789/configure-ad-1/assets/84995125/95e70684-8579-4398-80a0-5bdbedb2d52a)

![Snipaste_2024-05-18_16-58-54](https://github.com/AGZ2789/configure-ad-1/assets/84995125/cbb09554-2018-49e3-9e6f-084d65f07f4a)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create the Client VM (Windows 10) named “Client-1”. 
  
  - Use the same Resource Group and Vnet that was created
</h2>

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_17-07-36](https://github.com/AGZ2789/configure-ad-1/assets/84995125/a6b2779d-9baa-4ceb-9e46-06668add1749)

![Snipaste_2024-05-18_17-08-55](https://github.com/AGZ2789/configure-ad-1/assets/84995125/4af4331b-21ad-4a8b-ba1e-5d7dbeb37a5d)

![Snipaste_2024-05-18_17-12-39](https://github.com/AGZ2789/configure-ad-1/assets/84995125/43925ebf-5f7b-497f-862e-cc5468d80134)

![Snipaste_2024-05-18_17-21-44](https://github.com/AGZ2789/configure-ad-1/assets/84995125/e81b2395-2c9d-4881-9f09-1315cacb0c50)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

- Example of deployed Virtual Machines + essential details

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_17-26-50](https://github.com/AGZ2789/configure-ad-1/assets/84995125/82bcdb1a-65f4-4302-802c-0703e1b9ef1d)

![Snipaste_2024-05-18_17-27-36](https://github.com/AGZ2789/configure-ad-1/assets/84995125/119659b0-0f41-4e27-88a6-f1b2179163c9)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Ensure Connectivity between the client and Domain Controller (DC-1)</h2>

- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with 
ping -t <ip address> (perpetual ping)
- Login to the Domain Controller and enable ICMPv4 on the local Windows firewall
- Check back at Client-1 to see the ping succeed

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_17-40-15](https://github.com/AGZ2789/configure-ad-1/assets/84995125/62ea1d1b-2aa0-4f63-99c0-d23fbfe8e14a)

![Snipaste_2024-05-18_17-44-28](https://github.com/AGZ2789/configure-ad-1/assets/84995125/7cf0f9f9-ad6a-4727-8926-a9d1294c725b)

![Snipaste_2024-05-18_17-47-23](https://github.com/AGZ2789/configure-ad-1/assets/84995125/7a36f95f-ff21-4779-9067-212cb099b017)

![Snipaste_2024-05-18_18-01-11](https://github.com/AGZ2789/configure-ad-1/assets/84995125/4bf6ed8a-86ac-465a-8ff6-2d13aba0adab)

![Snipaste_2024-05-18_18-13-37](https://github.com/AGZ2789/configure-ad-1/assets/84995125/6ad588ba-c133-4895-9946-ce64bded30ec)

![Snipaste_2024-05-18_18-18-19](https://github.com/AGZ2789/configure-ad-1/assets/84995125/4da1cd3e-a213-4c36-bed3-f26a7f63c8d9)

![Snipaste_2024-05-18_18-22-54](https://github.com/AGZ2789/configure-ad-1/assets/84995125/7c525ec4-a001-4dda-838c-57aa98a4e946)

![Snipaste_2024-05-18_18-24-58](https://github.com/AGZ2789/configure-ad-1/assets/84995125/6a992c48-20f1-414e-8ec3-c96b607cc14d)

![Snipaste_2024-05-18_18-27-51](https://github.com/AGZ2789/configure-ad-1/assets/84995125/6aea483f-dbf8-4e90-930f-0829f29e6709)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Install Active Directory</h2>

- Login to DC-1 and install Active Directory Domain Services
- Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
- Restart and then log back into DC-1 as user: mydomain.com\labuser

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻






🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create an Admin and Normal User Account in AD</h2>

- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group
- Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
- User jane_admin as your admin account from now on

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻






🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Join Client-1 to your domain (mydomain.com)</h2>

- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
- Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes. I guess I skipped this in the lab!)


🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻





🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Setup Remote Desktop for non-administrative users on Client-1</h2> 

- Log into Client-1 as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now
- Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻





🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create a bunch of additional users and attempt to log into client-1 with one of the users</h2>

- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it 
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
- Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻






<h2>Finish</h2>

<h2></h2>

<h2></h2>

<h2></h2>

<h2></h2>





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
