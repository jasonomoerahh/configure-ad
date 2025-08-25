<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com/playlist?list=PLAnyL2H5UDKJMvD8S6Tw0vygNQYxSWuRe)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory Domain Services on DC-1, promote it to a Domain Controller with a new forest (e.g., mydomain.com), and log in using domain credentials.
- Create Organizational Units (_EMPLOYEES and _ADMINS) in Active Directory and add a new Domain Admin user jane_admin to the “Domain Admins” group.
- Log in as jane_admin and use it as the main admin account going forward for managing your domain environment.
- Join Client-1 to the domain by logging in as the local admin, connecting it to mydomain.com, restarting it, and moving it into a new “_CLIENTS” Organizational Unit in Active Directory Users & Computers.
- Enable Remote Desktop access for Domain Users on Client-1 to allow non-administrative users to log in remotely.
- Use a PowerShell script on DC-1 to create multiple employee accounts in the “_EMPLOYEES” OU and test login with one of the new user accounts on Client-1.
- Verify that all newly created user accounts appear in Active Directory, and confirm successful domain logins and access permissions on Client-1.
  
<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/user-attachments/assets/1e9a93d0-b6de-4304-8756-f4ccd8926c44" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/d3031e7f-da26-4476-a250-f931040dc401" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To begin configuring your on-premises Active Directory infrastructure, log into the DC-1 virtual machine and install the Active Directory Domain Services (AD DS) role. After installation, promote the server to a Domain Controller by creating a new forest (e.g., mydomain.com). Once the server restarts, you can log in using your domain credentials (e.g., mydomain.com\marc) to manage your new AD environment.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/420a5df8-32d9-49f8-9b85-0b790f6cd2ca" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/29ddecf9-1b06-45d2-8c1d-f56beff5d678" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/9dad8d34-5aed-46e0-8a34-02624deb9fa2" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Active Directory Users and Computers (ADUC), creating Organizational Units (OUs) like _EMPLOYEES and _ADMINS helps organize user accounts based on their roles or access levels. Within the _ADMINS OU, you create a new user account called jane_admin and assign it a secure password. After creating the account, you add jane_admin to the “Domain Admins” security group, granting it administrative privileges across the domain.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/ce82cbd1-d032-4f9a-84ad-c654f899e9a4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After creating the jane_admin account and adding it to the Domain Admins group, log out of DC-1 and log back in using the domain credentials for jane_admin. This account will now have administrative privileges across the domain and should be used for managing domain resources and configurations. Using a dedicated domain admin account improves security and separates administrative tasks from regular user activity.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/664c55bd-4216-4b6a-99e2-04a40479dd34" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/10155ba5-95df-44c5-998e-45dba054b600" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To join Client-1 to the domain, first log into the Client-1 VM as the local administrator and connect it to your domain (e.g., mydomain.com**) through the system settings. Once the computer restarts and successfully joins the domain, log into DC-1 and open **Active Directory Users and Computers (ADUC). In ADUC, create a new Organizational Unit called **\_CLIENTS** and move *Client-1* into it to organize and manage client machines more effectively.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/d55a74ae-d31c-4fed-933c-6a7ea06f7968" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To enable Remote Desktop access for Domain Users on *Client-1*, log in as **mydomain.com\jane\_admin** and open the system properties. Navigate to the **Remote Desktop** settings and allow connections from users in the **Domain Users** group. This configuration permits standard domain users to access the machine remotely, which is useful for testing logins and supporting end users in a real-world environment.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/ad5a310c-3ec9-4f69-9802-7c7c5faec083" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/9d5d224c-dd75-42a6-9459-913000b87903" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, launch PowerShell ISE as an administrator and use a script to automatically generate multiple employee user accounts in the _EMPLOYEES Organizational Unit. Once the script runs, verify the new accounts in Active Directory Users and Computers (ADUC). Then, switch to Client-1 and attempt to log in using one of the newly created accounts to confirm proper domain authentication. 

</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/b948aa62-373f-4035-a8a3-229b94573d0c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/659e7858-c497-4b3a-83a4-a42cf69a3336" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After running the PowerShell script to create user accounts, open Active Directory Users and Computers (ADUC) on DC-1 to ensure all accounts are correctly listed under the _EMPLOYEES OU. Then, on Client-1, test logging in with several of the new accounts to verify that they are recognized by the domain. Confirm that each user can log in successfully and that appropriate access permissions are applied.

</p>
<br />
