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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<h2>Setup Resources in Azure</h2>
  
- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
  - Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
- Set Domain Controller’s NIC Private IP address to be static
- Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher)

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

![Snipaste_2024-05-18_18-52-04](https://github.com/AGZ2789/configure-ad-1/assets/84995125/37d44d51-4447-4f8f-be76-c7243f18860c)

![Snipaste_2024-05-18_18-37-05](https://github.com/AGZ2789/configure-ad-1/assets/84995125/9ecf7c58-a281-4bf6-9d80-0567bad9d448)

![Snipaste_2024-05-18_18-40-06](https://github.com/AGZ2789/configure-ad-1/assets/84995125/6e552840-9348-4e07-a9c9-171ff48adbd8)

![Snipaste_2024-05-18_18-41-00](https://github.com/AGZ2789/configure-ad-1/assets/84995125/699464a7-04d3-495c-90fc-014487ffc51f)

![Snipaste_2024-05-18_18-41-34](https://github.com/AGZ2789/configure-ad-1/assets/84995125/0bb0f2c1-421d-4fa7-9cfe-8c1a28769247)

![Snipaste_2024-05-18_18-42-10](https://github.com/AGZ2789/configure-ad-1/assets/84995125/1aa86999-73ce-461d-9568-68486da7150e)

![Snipaste_2024-05-18_18-42-40](https://github.com/AGZ2789/configure-ad-1/assets/84995125/9c2a805d-fa47-45d8-9c6b-510c94ec9a25)

![Snipaste_2024-05-18_18-53-40](https://github.com/AGZ2789/configure-ad-1/assets/84995125/100700ee-43d4-4102-868b-a57f148a68b5)

![Snipaste_2024-05-18_18-58-21](https://github.com/AGZ2789/configure-ad-1/assets/84995125/eed09063-552d-4f8d-afd7-dd8073079803)

![Snipaste_2024-05-18_18-59-39](https://github.com/AGZ2789/configure-ad-1/assets/84995125/e2289e57-9f34-470b-af0a-ba3b0e84a7bd)

![Snipaste_2024-05-18_19-02-05](https://github.com/AGZ2789/configure-ad-1/assets/84995125/58b771f1-ac9d-422f-911c-ff9cd368b631)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create an Admin and Normal User Account in AD</h2>

- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group
- Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
- User jane_admin as your admin account from now on

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_19-13-20](https://github.com/AGZ2789/configure-ad-1/assets/84995125/4be9cd99-07cc-4fbc-8c3a-a427d7a2984d)

![Snipaste_2024-05-18_19-16-03](https://github.com/AGZ2789/configure-ad-1/assets/84995125/538c797a-1646-4248-a720-96507768e783)

![Snipaste_2024-05-18_19-19-21](https://github.com/AGZ2789/configure-ad-1/assets/84995125/c6dbae5a-a63e-4e50-ad05-4f3f17207024)

![Snipaste_2024-05-18_19-22-10](https://github.com/AGZ2789/configure-ad-1/assets/84995125/2bec6e08-446d-463d-9191-2f97f7736cf1)

![Snipaste_2024-05-18_19-23-21](https://github.com/AGZ2789/configure-ad-1/assets/84995125/72772089-98eb-4ba6-9581-1302681c5f79)

![Snipaste_2024-05-18_19-23-54](https://github.com/AGZ2789/configure-ad-1/assets/84995125/43385b80-cba3-4b80-9169-b153c7e78cb1)

![Snipaste_2024-05-18_19-28-57](https://github.com/AGZ2789/configure-ad-1/assets/84995125/ba7844a3-488f-4abd-9c92-3457de33a52f)

![Snipaste_2024-05-18_21-01-05](https://github.com/AGZ2789/configure-ad-1/assets/84995125/0bef6d97-054a-4585-abb1-33b8f04356d8)


🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Join Client-1 to your domain (mydomain.com)</h2>

- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
- Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes.)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_21-08-46](https://github.com/AGZ2789/configure-ad-1/assets/84995125/50470790-b6ee-4db5-b53f-d2aa645cef72)

![Snipaste_2024-05-18_21-10-45](https://github.com/AGZ2789/configure-ad-1/assets/84995125/e913f2b7-7332-44ef-9d11-dfcabe682311)

![Snipaste_2024-05-18_21-24-38](https://github.com/AGZ2789/configure-ad-1/assets/84995125/36cf490b-53bc-4dd5-8e68-b60aaeb09445)

![Snipaste_2024-05-18_21-25-23](https://github.com/AGZ2789/configure-ad-1/assets/84995125/2fe3f2ff-eddc-42c7-9e5d-3513ee5a8360)

![Snipaste_2024-05-18_21-27-43](https://github.com/AGZ2789/configure-ad-1/assets/84995125/29148aa0-ed1f-4f45-81a8-85f18fe034e3)

![Snipaste_2024-05-18_21-43-40](https://github.com/AGZ2789/configure-ad-1/assets/84995125/c44896d3-b31f-46a3-a889-bf6c758efa36)



🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Setup Remote Desktop for non-administrative users on Client-1</h2> 

- Log into Client-1 as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now
- Normally you’d want to do this with Group Policy that allows you to change MANY systems at once.

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_21-54-01](https://github.com/AGZ2789/configure-ad-1/assets/84995125/4b8a7283-017a-4b42-ae28-8218a44e8b49)

![Snipaste_2024-05-18_21-54-44](https://github.com/AGZ2789/configure-ad-1/assets/84995125/6519b939-5250-46ed-aacd-b2f0c5d58bb1)

![Snipaste_2024-05-18_21-59-45](https://github.com/AGZ2789/configure-ad-1/assets/84995125/805ea378-4e1d-4d66-9c3b-503b8685a8eb)

![Snipaste_2024-05-18_22-12-48](https://github.com/AGZ2789/configure-ad-1/assets/84995125/f628650d-60d1-48c8-82b3-62135bcd1c61)

![Snipaste_2024-05-18_22-13-29](https://github.com/AGZ2789/configure-ad-1/assets/84995125/d363af64-6c00-406a-884d-476fafbf5320)

![Snipaste_2024-05-18_22-17-05](https://github.com/AGZ2789/configure-ad-1/assets/84995125/bb365c0f-97f4-4b93-b233-24019d2d8c7f)


🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Create a bunch of additional users and attempt to log into client-1 with one of the users</h2>

- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it 
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
- Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

![Snipaste_2024-05-18_22-20-47](https://github.com/AGZ2789/configure-ad-1/assets/84995125/d6e51bf4-e1d6-4ee7-988d-7b2c3647c4a9)

![Snipaste_2024-05-18_22-22-10](https://github.com/AGZ2789/configure-ad-1/assets/84995125/617462f2-f668-493a-8ff8-fe3d1a9eb642)

![Snipaste_2024-05-18_22-24-25](https://github.com/AGZ2789/configure-ad-1/assets/84995125/8695216a-21e2-483e-8850-a863145dfd0f)

![Snipaste_2024-05-18_22-26-35](https://github.com/AGZ2789/configure-ad-1/assets/84995125/451ad882-0606-4cd2-af02-d4757e087afb)

![Snipaste_2024-05-18_22-27-46](https://github.com/AGZ2789/configure-ad-1/assets/84995125/5cea647b-230e-4be9-b088-7292e286b1ea)

![Snipaste_2024-05-18_22-32-17](https://github.com/AGZ2789/configure-ad-1/assets/84995125/c7d0e384-b2d0-4ef7-b24e-3b71a165448d)

![Snipaste_2024-05-18_22-36-58](https://github.com/AGZ2789/configure-ad-1/assets/84995125/9852491b-07f6-4802-ade8-f8e343253fbb)

![Snipaste_2024-05-18_22-37-17](https://github.com/AGZ2789/configure-ad-1/assets/84995125/7b3453bd-0f50-431d-bc8c-e99523509ba3)

![Snipaste_2024-05-18_22-42-40](https://github.com/AGZ2789/configure-ad-1/assets/84995125/1b239030-5015-4870-bd3d-2fb89475241d)

🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻🔻

<h2>Lab Cleanup (DON’T FORGET THIS)</h2>

- Close your Remote Desktop connection
- Delete the Resource Group(s) created at the beginning of this lab
- Verify Resource Group Deletion

<h2>Finish</h2>
