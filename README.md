<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h1>Environments and Technologies Used</h1>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h1>Operating Systems Used</h1>

- Windows Server 2022
- Windows 10 (21H2)

<h1>Steps Overview</h1>

- Install Active Directory Domain Services on domain controller
- Promote Server computer into a Domain Controller
- Create a Domain Admin user within the domain
- Join “Client-1” to the domain (mydomain.com)

The steps above are needed in order to successfully deploy Active Directory and make it functional for users. This tutorial will break down the installation of Active Directory as well as the steps to promote server computers into Domain Controllers and adding users to the Active Directory.  


<h1>Install Active Directory Domain Services on domain controller</h1>


To begin, Active Directory must be installed on the domain controller. This is necessary because the Domain Controller is the server role that is designed to host and manage AD DS(Active Directory Domain Services). This core service handles Authentication, Authorization, and the managing of domain objects. Within the domain controller, click the start button on the bottom left.

<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%201.png" width="600" height="400" />


Click on "Server Manager" then within the server manager click on "Add roles and features".

<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%202.png" width="600" height="600" />

<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%203.png" width="600" height="400" />


Within the “Before You Begin” section in the “Add Roles and Features Wizard” screen, click on “Next” on the bottom right corner. Within the “Installation Type” section, click on “Next” on the bottom right corner. Within the “Server Selection” section, the dc-1 server needs to be selected. Once it is selected, Click on “Next” on the bottom right corner.


<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%204.png" width="600" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%205.png" width="600" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/353a618b5b66c1356b15b7fdf6bc43ec6d8ef178/images/Active%20directory%205%20(1).png" width="600" height="400" />




Within the “Server Roles” section, select “Active Directory Domain Services” under the “Roles” section. 


<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%207.png" width="600" height="400" />



When the “Active Directory Domain Service” role is clicked, a pop-up screen will appear requesting to install services and features. Make sure the checkbox next to “Include management tools (if applicable)” is checked. Afterwards, Click on “Add Features” on the bottom right corner.  

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%208.png" width="600" height="400" />



Once “Add Features” is clicked, the previous screen will show back up with a checkmark next to “Active Directory Domain Services”. On this screen, Click on “Next” on the bottom right hand corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%209.png" width="600" height="400" />


Within the “Features” section, click on “Next” on the bottom right corner. Within the “AD DS” section, click on “Next” on the bottom right corner.

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2010.png" width="600" height="400" />


Within the “Confirmation” section, click on the checkbox next to “Restart the destination server automatically if required”. A pop-up screen will show up. Click on “Yes” on the bottom. Afterwards, click on “Install” on the bottom right hand corner.

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2012.png" width="600" height="400" />



A bar showing the installation progress will appear within the “Results” section. Once the installation is finished, click on “Close” on the bottom right hand corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2013.png" width="600" height="400" />


<h1>Promote Server machine into a Domain Controller</h1>
Now that “AD DS” has been installed, the server machine must be promoted to a Domain Controller. Some configurations must be made in order to do this. To begin, click the white flag icon on the top right within the server manager screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2014.png" width="600" height="400" />

Within this pop-up screen, Click on “Promote this server to a domain controller”

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2015.png" width="600" height="400" />


A “Active Directory Domain Services Configuration Wizard” screen will show up. Within the  “Deployment Configuration” section, click on the “Add a new forest” option. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2016.png" height="400" />


Once clicked, a “Root domain name” section will appear. A domain name must be typed in. The domain name typed in the box must follow Dns naming convention. Examples are (yourcompany.local, yourdomain.internal, yourdomain.com). For Private/ Internal Networks, .local, .internal, and .Lan can be used. For Public networks, .com can be used. For the purposes of this demonstration the root name “mydomain.com” will be used. Type in the domain name in the text box then click on “Next” on the bottom right hand corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%2017.png" height="400" />




Within the “Domain Controller Options” section, there is place to type and confirm a password for the “Directory Services Restore Mode”. This password is important as it will be utilized in recovering or troubleshooting Active Directory issues. Type in a unique password in the textbox next to “Password”. For the purposes of this demonstration the password “password1” will be used. Retype the same password in the textbox next to “Confirm password”. Afterwards, Click on “Next” on the bottom right hand corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/588631cd5fc4175f15a02fa46442b2d97d624252/images/Active%20directory%20%2018.png" height="400" />


Within the “DNS Options” section, make sure the checkbox next to “Create DNS delegation” is unchecked. Afterwards, click on “Next”. 

<img src="https://github.com/JosephRC777/configure-ad/blob/5c338183535a07c26c02fb42d01716b0eb8dae14/images/Active%20directory%2019.png" height="400" />


Within the “Additional Options” section, click on “Next” on the bottom right corner. Within the “Paths” section, click on “Next” on the bottom right corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/5c338183535a07c26c02fb42d01716b0eb8dae14/images/Active%20directory%2021.png" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/5c338183535a07c26c02fb42d01716b0eb8dae14/images/Active%20directory%2022.png" height="400" />


Within the “Review Options” section, click on “Next” on the bottom right corner. Within the “Prerequisites Check” section, click on “Install” on the bottom right corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/5c338183535a07c26c02fb42d01716b0eb8dae14/images/Active%20directory%2023.png" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/5c338183535a07c26c02fb42d01716b0eb8dae14/images/Active%20directory%2024.png" height="400" />



Once the installation is complete and the server computer has been turned into a Domain Controller, the following pop-up will appear.

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/active%20directory%2025.JPG" height="400" />


Once “Close” is clicked on the bottom right hand corner, the computer will  restart. After these configurations are made, a Domain admin user can be created within the domain. 


<h1>Create a Domain Admin user within the domain</h1>


The next step is to create a domain admin user for the Domain controller. This user is necessary in order to manage User and group accounts, Group Policy Objects (GPOs), Domain Trusts, and DNS configuration within the DC. It is also needed for security reasons. Open “Active Directory Users and Computers” by using the Windows search bar on the bottom left corner of the screen and typing “Active Directory” and clicking on the application.


<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%201.png" height="400" />


Within this application, right click the “mydomain.com” section and select “New” then click on “Organizational Unit”. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%202.png" height="400" />



A “New Object - Organizational Unit” screen will show up. Within this screen, in the textbox under “Name” the organizational unit can be given a name. For compatibility with scripts and tools, using a underscore (_) for naming is suggested. For the purposes of this demonstration the name “_EMPLOYEES” will be used for this organizational unit. The naming of the OU’s is case sensitive. After typing the name of the OU, Click on “OK” on the bottom of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%203.png" height="400" />


Now an “_ADMINS” OU must be created. Within “Active Directory Users and Computers” right click the “mydomain.com” section and select “New” then click on “Organizational Unit”. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%202.png" width="600" height="400" />


In the textbox under “Name”, type in the name  “_ADMINS” then click on “OK” on the bottom of the screen.

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%204.png" width="600" height="400" />


Now that these OUs have been created, a user within “_ADMINS” folder will be created. This will be the admin user account. Right click the “_ADMINS” folder and select the “New” option, then click on “User”.   

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%205.png" width="600" height="400" />


A “New Object - User” screen will appear. Within this screen, a first and last name as well as a logon name can be assigned to the user. For the purposes of this demonstration the name “Jane Doe” will be used as well as the logon name “jane_admin”. After these credentials are typed in, click on “Next” on the bottom right hand corner. 


<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%206.png" width="600" height="400" />



Within the next section, a password will need to be assigned to this user. There are 4 options listed for password security options. These are “User must change password at next logon”, “User cannot change password”, “Password never expires”, and “Account is disabled”. Select the option that is best suited for this user. For the purposes of this demonstration the password “Cyberlab123!” will be used and the “Password never expires” option will be selected. Once the password has been typed in, click on “Next” on the bottom right hand corner of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%207.png" width="600" height="400" />


Within the next screen, Click on “Finish”

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%208.png" width="600" height="400" />


Now that the user Jane Doe has been created, the user can be made into an admin by adding it to the “Domain Admin” security group. Right click on “Jane Doe” within the “_ADMINS” folder then click on “Properties”.

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%209.png" width="600" height="400" />


A “Jane Doe Properties” screen will appear. Within this screen, click on the “Member Of” tab on the top left corner of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%2010.png" width="600" height="400" />


Click on “Add…” on the middle of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%20%2011.png" width="600" height="400" />


A “Select Groups” screen will appear. Within this screen under the “Enter the object names to select” section, type in “domain admins” then click on “Check Names” on the right side of the screen. This will confirm if there are any groups that match the given name. Afterwards, click on “OK” on the bottom right hand corner of the screen.  

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%2012.png" width="600" height="400" />


Once completed, you will be taken back to the "Member Of” tab. On this screen, Click on “Apply” on the bottom right corner of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/27c01ff2210d72923a01220b2acd11682d9e3690/images/Active%20Directory%20DC%20ADmin%2013.png" width="600" height="400" />

Now that we created an admin user and the Active Directory has been deployed and its in the cloud, we can add a computer to this network. 


<h1>Join Client-1 to your domain (mydomain.com)</h1>


A computer can now be added to the domain. For the purposes of this demonstration a virtual machine named “Client-1” will be added. The computer joining the domain has to have its DNS settings changed to the Private IP address of the Domain Controller. This has already been done for the “Client-1” virtual machine that will connect to the DC. 


Within “Client-1”, Access “Settings” by using the windows search bar on the bottom left corner. 

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%201.png" width="600" height="400" />


Within the “Settings” screen, click on “About” on the bottom right hand corner. Afterwards, click on “Rename this PC (advanced)” on the right hand side of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%202.png" width="600" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%203.png" width="600" height="400" />

A “System Properties” screen will show up. Within this screen, click on “Change…” in the middle of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%204.png" width="600" height="400" />


A “Computer Name/Domain Changes” screen will show up. Select “Domain:” on the bottom of the screen, then type in the name of the domain that was setup earlier in the text box. The name “mydomain.com” will be used. Afterwards, click on “OK” on the bottom right corner of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%205.png" width="600" height="400" />



A “Windows Security” screen will show up. Within this screen, the credentials of the admin that was set up for the domain controller must be provided. For the purposes of this demonstration, the user name “mydomain.com\jane_admin” and the password “Cyberlab123!”. After the credentials are imputed, click on “OK” on the bottom left corner of the screen. 

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%206.png" width="600" height="400" />



A confirmation message will pop-up afterwards if the credentials matched. Click “OK”. The computer will then need to be restated. Once it boots up again it will officially be a member of the domain controller. Now an organizational unit named “_CLIENTS” will be created within the domain controller and “Client-1” will be put within this folder. To begin, go to the “Active Directory Users and Computers” application with the Domain Controller. Within the app,  right click the “mydomain.com” section and select “New” then click on “Organizational Unit”. Name this organizational unit “_CLIENTS” then click “OK” on the bottom right hand corner of the screen.


<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%207.png" width="600" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%208.png" width="600" height="400" />



“Client 1” can now be dragged into this folder. Within the “mydomain.com” drop down, click on the “Computers” folder and select “client-1”. Drag “client-1” into the “_CLIENTS” folder.

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%209.png" width="600" height="400" />

<img src="https://github.com/JosephRC777/configure-ad/blob/a0043bd7b5ce928660dadb65cdae0c11bffb572c/images/Active%20Directory%20Client%2010.png" width="600" height="400" />


This concludes all the steps. Now Active Directory has been deployed and configured and a computer has been added to the domain. 


































































