<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Establish resources in Azure
- Verify connectivity between Client-1 and Domain Controller
- Install Active Directory
- Create an Admin and user account within active directory
- Join Client 1 to the domain
- Set up remote desktop for non admin users on client-1
- Create dummy users on DC-1(Domain controller) to test login success from client-1

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/mK7Ls85.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Begin by creating a Domain Controller Virtual Machine using the "Windows Server 2022" option and name it "DC-1". Make sure to confirm that the resource group and Virtual Network are created as well.
</p>
<br />

<p>
<img src="https://i.imgur.com/r8c6vlr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Ensure that you set the Domain Controllers private IP address to "Static" instead of dynamic.
</p>
<br />

<p>
<img src="https://i.imgur.com/sZG2JPo.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Now you must create another VM titled "Client-1" but you must make sure to use the same resource group and Vnet that was automatically created in step 1. Also, dont forget to verify that both VM's are in the same Vnet. You can check using the "Network Watcher" feature.
</p>
<br />

<p>
<img src="https://i.imgur.com/a3hTWHW.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. The next step is to remote desktop into DC-1 and install Active Directory Domain Services. The server manager should already be open once youve signed into DC-1. Select "Add roles and features." From there make sure you add "Active Directory Domain Services" and proceed with the install.                                           
</p>
<br />

<p>
<img src="https://i.imgur.com/MLb6Hs6.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>                                                   
4a. There should now be an alert at the top right of the server manager screen. Once you click that you'll have the option to promote the server to a domain controller. Choose that option to offically have all of the proper features.                                                   
</p>
<br />

<p>
<img src="https://i.imgur.com/nfDDzru.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>                                                   
4b. You should now be brought to a new window titled "Deployment Configuration". Select the option to create a new forest. For the "Root domain name" option enter "mydomain.com" for this example. Make it an easy password that you can remember. DC-1 shouldve signed you out as well as terminated the remote desktop connection. Log back into DC-1 as the user you previously created during the setup process. The login will be "mydomain.com\" followed by your username as well as the password created. 
</p>
<br />

<p>
<img src="https://i.imgur.com/3fxDLnY.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>                                                                                                   
5. Create an organizational unit titled "_EMPLOYEES" by clicking the "Tools" option at the top right then selecting "Active Directory Users and Computers". Right click on your domain then select "New"->"Organizational Unit" and title accordingly. Repeat the same process and title the next one "_ADMINS".
</p>
<br />

<p>
<img src="https://i.imgur.com/mzwLh3P.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>                                                                                                      
6. Create an employee named "Jane Doe" using the same password you've already been using with the username "jane_admin". Similar to how you created the organization units, this time right click "_ADMINS"->"New"->"User". Make sure to add her to the "Domain Admins" security group as you will be using the jane_admin user as your main admin account to get an idea of a real world simulation. Again, use the same password you've been using for ease of access. Once created right click your newly created user and head to "Properties" then "Member Of". Select "Add.." then type "domain admin" and check names. Join her to the "Domain Admins" group.
6a- Log out of DC-1 and now sign back in with the "jane_admin" user and keep that on standby for now.
</p>
<br />

<p>
<img src="https://i.imgur.com/nzf5JKX.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>                                                    
7. Head back into the Azure portal and set Client-1's DNS settings to the same as DC-1's private IP address. Click on DC-1 and copy its private IP and paste it into the DNS server settings on Client-1. Once complete, restart Client-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/nzf5JKX.png" height=60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>        
8.   
  
  
  
  
  
