# Active Directory Home Lab

This lab is about setting up an Active Directory home lab on VirtualBox. For this lab, Windows Server 2016 has been used as the Domain Controller. 

### Things needed to do first:
- Download and install Windows Server 2016 on VirtualBox.
- By going into settings of "This PC", change the computer name into something simple i.e. Server2016 for convenience.

<p align="center">
Changing Computer name <br/>
<img src="https://imgur.com/UtPVhLj" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

- From the Server Manager, go to: 'Manage' -> 'add roles and features' -> 'role based or feature based installation' -> 'add active directory domain services'. Then click on 'promote this server to a domain controller'.
- In the 'Deployment configuration', add a new forest and set the root domain name. Once finished, AD users and computers can be accessed.

### Users on AD users and computers:
- Any user can be found by right clicking, going into find option and searching in entire directory.
- To create a new user, simply right click on users and click on New, then Users. 
- Click on view and then click on advanced features --> helps to find out what folder or what OU or what path a user is part of. To verify, click on the user and go to object tab.
- To make a copy of the Administrator account, go to AD users and computers, click on the Admin account, click on copy, and specify the name of the new account. Name it helpdesk.

### Setting up Windows 2016 in a virtual environment: 
- To create a lab environment, give the machine a static IP with the following network settings:

  - IP address: 10.1.10.2
  -	Subnet mask: 255.0.0.0
  - Default gateway: 10.1.10.1
  - Preferred DNS server: 10.1.10.2
  - Alternate DNS server: 10.1.10.1
- On VirtualBox for server 2016, go to Devices -> Network settings -> and click on Host-only adapter

## Install a Windows 10 machine and add it to VirtualBox

- On the newly added windows 10 machine, go to file explorer and right click on 'this pc' and click on manage. Then go to local users and groups; then go to Users. Go to properties of the Administrator account and uncheck "account is disabled" option. Then set a password on it.
- Go to add or remove programs, then optional features, then add a feature. Then click on the RSAT tools options and add them. RSAT allows to have access to AD users and computers on a windows 10 machine.
- Change the network settings on the Windows 10 machine with the following settings:
  
    - IP address: 10.1.10.3
	- Subnet mask: 255.0.0.0
	- Default gateway: 10.1.10.1
	- Preferred DNS server: 10.1.10.2
	- Alternate DNS server: 10.1.10.1
  - On virtual box for windows 10, go to Devices -> Network settings -> and click on Host-only adapter
 
### Adding Windows 10 to the Domain:
- Right-click on 'this pc' and then properties -> Change settings -> Change (for changing name or adding it to a domain): In the 'member of' section, click on Domain and specify the name of the domain that was set up on the server 2016 machine.
- To check, click on AD users and computers on the server 2016 box and go to Computers section, and the windows 10 machine should be right there.

#### On Windows 10:
- Click on the AD users and computers and right-click on the domain. Go to new and then organizational unit and create a new OU called HR.
- Go to users and create a user account called "patty". Move this user to HR OU.
- Create another OU called IT and add the helpdesk account to the IT OU.
- Make sure advanced features is enabled on AD users and computers so you can check the Attribute editor option in the properties section of the user (can achieve similar results by using the cmd command: net user 'name' /domain).
#### Checking policies:
- Right-click on a user and go to 'All tasks' and then click on 'Resultant Set of Policy (Logging)'. It shows the group policy of that user account.
- From the windows 10 machine, go to Server Manger, then 'Tools', then 'group policy management'. It shows the group policy of the domain controller.
- From the default domain policy, go to settings to see the policy settings.
- Right-click on default domain policy and go to Edit. Go to the security settings and then account policy then account lockout policy. Form there you can apply settings for things like account lockout duration, threshold, etc. From the password policy settings, you can apply the settings for password stuff. Can double check for the changes in the default domain policy. 

### Add another Windows 10 (Desktop2) on VirtualBox and add it to the Domain
- Set a static IP with the following network settings:
  
    - IP address: 10.1.10.4
	- Subnet mask: 255.0.0.0
	- Default gateway: 10.1.10.1
	- Preferred DNS server: 10.1.10.2
	- Alternate DNS server: 10.1.10.1
  - On virtual box for Desktop2, go to Devices -> Network settings -> and click on Host-only adapter
 
- Patty user account was created before. Log into Desktop2 as Patty.

### Account locked out scenario:
- To fix this, go to the server 2016 and then go to AD users and computers. Go to the properties of the locked user and click on Account and then click on unlock account. The account can also be disabled by right clicking on the user. Can enable it in the same way. If it needs a password reset, then it can be done so in the same way. If account has expired, you can click on never in the 'Account expires' setting. 

### Computer somehow getting removed from Domain:
- In this case, try to locally log in. On the login screen, in the username section, type: ".\administrator" and press enter. Then once logged in, go to properties and click on change settings. Put the computer on the "WORKGROUP" and then back on the domain with the specified domain name.


### Shares
- On the server 2016, go to Server Manager and then click on File and Storage Services. Then go to Shares and right click on Shares and click on new share. Keep clicking next and name the share "HR". Complete it by clicking on the next options. Create a "personal" share in the same way. In the C: drive by default it should have shares folder and inside you should see Personal and HR folders.
- Go to AD users and computers. Right-click on users and then go to "New" and then "Group". The group type should be security and the name should be HR. If you double click on this HR group and then go to "managed by", you can put the name of "helpdesk" in that name section. Make a "personal" group in the same way. Now go to "This pc" and you can go to the properties of HR and personal folders and click on sharing. Copy the network path, and paste it in the description section of the properties of the groups that are in AD users and computers. This is just to label it. Now from AD users and computers, add patty to the "members" section of the HR and personal group.
- From "This pc", go to the personal folder properties. Go to security and then advanced. Click on disable inheritance. Click on 'Convert inherited permissions into explicit permissions on this object'. Click on "add" and then 'Select a principle'. Type in "helpdesk". Click on "modify" for basic permissions. Type in "personal" in the same process. Now go to sharing in properties and the "personal" should have permission level "read/write". Then click on share. Now do the same thing for the HR one. If this is done correctly, the shared folder should be accessed by patty on her computer (Desktop2) with the network share location. In the file explorer type: "\\server2016\hr". To create a shortcut, you can drag and drop it in the quick access location. To map it, right click on "this pc" and then go to map network drive. Paste the network drive location and the new drive should be there.
- You can also map a drive from AD. On server 2016, go to AD users and computers and go to the properties of patty and click on profile. In the home folder, click on connect. Type in `\\Server2016\Personal\%username%`. Now it should create a folder for patty. 

### Remote settings
- In Desktop2 computer, go to properties from "this pc" and then go to remote settings. Enter the helpdesk account's credentials. Click on Allow remote connections to this computer. Open up remote desktop connection on the windows 10 machine (Helpdesk's machine) and enter the IP of desktop2 or the name of the computer which is Desktop2. If the remote desktop doesn't work, may need to do "ipconfig /flushdns" in cmd.
-  On windows 10 machine, type in \\desktop2\c$ and it should let you in on that user's account. You can upload or delete files remotely that way. 

### Group Policy Management
- On server 2016, from the server manager, go to group policy management. Right-click on group policy objects and click on new. Name it task manager. Now click on the task manager and go to delegation. Add patty to it. Then right-click on the Task manager and click on edit. Under user configuration find System and under it, there should be 'Ctrl+Alt+Del'. From there, Task manager can be removed. Move the Task manager that was created under Group policy objects to the HR OU under the domain. Now right click on the task manager policy and click on Enforced.
- In the Desktop2 machine, go to cmd and type in "gpupdate /force". You can run "gpresult /r" to see what policies are running on the machine. Can try to double check that task manager is actually removed by typing taskmgr in cmd on Desktop2. You can also generate a report by right clicking on the group policy results and then going to group policy results wizard. Type in the name of the computer and then select a specific user and it should generate a report. Another way to see report is to go to AD users and computers first. Then click on 'All tasks' by right clicking on patty. Click on resultant set of policy wizard. Type in the name of the computer and select patty for user and finish. Now in the resultant set of policy, the configurations or changes can be seen. 

### Remote App Deployment
- Install PDQ Deploy and PDQ Inventory on Server 2016.
- Open up PDQ Inventory and go to 'All computers'. Right-click and click on add computers. Then Desktop2 can be added by name. After Desktop2 is added, you can right-click on it and then click on "Tools". From there, you can send remote commands if needed such as Reboot/Shutdown, Remote Assist, Remote Desktop, Run Command etc.
- To deploy apps, rigtht-click on Desktop2, and go to "Tools". Then click on PDQ Deploy. That will open up the PDQ Deploy software.
- Packages can be downloaded from the Package library, and then you can deploy it by right clicking on the package and then clicking on 'Deploy Once'. Then you can add the computer by name (the target where apps will be deployed). After that, click on 'Deploy Now'.

### Print Management
- On server 2016, in the server manager, go to manage, then 'add roles and features'. Select 'print and document services'. Now go to 'Tools' and then 'print management'. Right-click and click on add a printer. Then select install a new driver. Pick the right printer.
- When the printer shows up, right-click on it and go to properties and then 'Sharing'. Click on share this printer. Add the HR group to the printer by going to security and advanced settings and then principle. You can also list it in directory to make it appear in AD (it would be in users and computers printer section which can be found by right clicking on the domain).
- Now on Desktop2, patty can see the printer. It should show up automatically when adding the printer. 

### Limited Permissioning 
- On server 2016, go to AD users and computers. Right-click on users and click on new and make a new user. Name him Scott. Create a new OU called consultants and put Scott in there.
- Now right-click on the domain and then click on 'delegate control'. Add Scott and then give him permission to only 'reset user passwords and force password change at next logon'.
- To test it, log in as scott in the windows 10 machine. Then go to AD users and computers. Go to the properties of a user and when you go to account, everything should be greyed out except the password change settings. Resetting password is the only thing Scott can do and nothing else. 
