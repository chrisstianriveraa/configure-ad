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


<h2>Deployment and Configuration Steps</h2>

<p>
In this lab we are going to create two machines in the same VNET. One of the machines will be a domain controller and the other will be a client machine. We are going to change the DC to a static IP because its offering Active Directory services to the client machine. The client VM will be joined to the domain. We'll control the DNS settings on the client machine and the machine will use the DC as its DNS server. 
</p>
<p>
<img src="https://i.imgur.com/t0Z1n3m.png"/>
</p>
<p>
DC-1 requires a static IP address. Initially, when Client one attempts to establish connectivity by pinging DC-1, the ping will not succeed. To resolve this issue, it is necessary to activate ICMPv4 on the DC-1 firewall. Once that is done, successful pinging of DC-1 from Client-1 becomes possible.
</p>
<p>
<img src="https://i.imgur.com/4cZiSAs.png"/>
<img src="https://i.imgur.com/Wfgnt54.png"/>
</p>
<br />

<p>
We'll log back into DC-1 to install Active Directory Users & Computers. Promote the VM to DC, setup a new forest as "mydomain.com" and restart then log back into DC-1 as user: mydomain.com\labuser". 
</p>
<p>
<img src="https://i.imgur.com/Yc6YW7Q.png"/>
</p>
<p>
We now can start creating the organizational units(OU). Create an OU named _EMPLOYEES and create another OU named _ADMINS. For this to happen right click on then domain area, select New->Organizational Unit and fill out the field. After click inside of the OU and right click, select new and select user and fill out the information of the new user. The user name is Jane Doe, she'll be an Admin and her username will be Jane_admin. Finally, ad jane to the domain security group.
</p>

<p>
<img src="https://i.imgur.com/IraCqSk.png"/>
<img src="https://i.imgur.com/xbyt2cW.png"/>
</p>
<br />

<p>
From here on out, you'll use Jane_admin as the admin account. Join client-1 to the domain from the azure portal, we'll change client-1's DNS settings to the DC's private IP address. After, you can restart client-1 within the azure portal. 
</p>
<p>
<img src="https://i.imgur.com/rlIfoHJ.png"/>
</p>

<p>
We have to join client-1 to the domain in order for this to happen go to system settings and on the right side of the select "rename this pc(advanced). From there change the domain and enter "mydomain.com" after input the information from mydomain.com\labuser. The machine will restart and client-1 will part of mydomain.com
</p>
<p>
<img src="https://i.imgur.com/9A0eD3B.png"/>   
</p>

<p>
Now that client-1 is part of the domain, we'll set up remote desktop for non-administrative users on client-1. Log into client-1 as admin and open system properties. Then click "remote desktop" allow domain users access to remote desktop.
</p>
<img src="https://i.imgur.com/DbXBdMf.png"/>

<p>
 Lastly we verify users can RDP into client-1, we'll use a script to generate users into the domain. We are going into the script in pwoershell. 
</p>
<img src="https://i.imgur.com/n6xKojz.png"/>
<img src="https://i.imgur.com/x5AshRO.png"/>
<br />
