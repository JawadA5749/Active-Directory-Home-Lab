# Active Directory Home Lab

This lab is about setting up an Active Directory home lab on VirtualBox. For this lab, Windows Server 2016 has been used as the Domain Controller. 

### Things needed to do first:
- Download and install Windows Server 2016 on VirtualBox.
- By going into settings of "This PC", change the computer name into something simple i.e. Server2016 for convenience.

<img width="913" height="631" alt="Image" src="https://github.com/user-attachments/assets/181b617b-be73-421a-b9d3-ecdb51ed6469" />

- From the Server Manager, go to: 'Manage' -> 'add roles and features' -> 'role based or feature based installation' -> 'add active directory domain services'. Then click on 'promote this server to a domain controller'.

<img width="781" height="553" alt="Image" src="https://github.com/user-attachments/assets/6f5e2b32-c576-4a28-b484-f24df273deaf" />

- In the 'Deployment configuration', add a new forest and set the root domain name (agent.com in this case). Once finished, AD users and computers can be accessed.

<img width="948" height="643" alt="Image" src="https://github.com/user-attachments/assets/e978f2b3-8a8d-403b-a4a4-5671943b597e" />

### Users on AD users and computers:
- Any user can be found by right clicking, going into find option and searching in entire directory.
- To create a new user, simply right click on users and click on New, then Users.

<img width="803" height="558" alt="Image" src="https://github.com/user-attachments/assets/d8ccfad7-7797-4e94-af30-de3723c64b80" />

- Click on view and then click on advanced features --> helps to find out what folder or what OU or what path a user is part of. To verify, click on the user and go to object tab.

<img width="610" height="277" alt="image" src="https://github.com/user-attachments/assets/721ea5c5-56e8-482f-8a05-6c1848c6a0a2" />

<img width="688" height="580" alt="image" src="https://github.com/user-attachments/assets/bdbcbad4-4866-4ca3-9643-1a3b66a2ce92" />


- To make a copy of the Administrator account, go to AD users and computers, click on the Admin account, click on copy, and specify the name of the new account. Name it helpdesk.

<img width="630" height="396" alt="image" src="https://github.com/user-attachments/assets/393c3468-5908-4b77-9f9a-a7f7b65cb139" />


### Setting up Windows 2016 in a virtual environment: 
- To create a lab environment, give the machine a static IP with the following network settings:

  - IP address: 10.1.10.2
  -	Subnet mask: 255.0.0.0
  - Default gateway: 10.1.10.1
  - Preferred DNS server: 10.1.10.2
  - Alternate DNS server: 10.1.10.1

<img width="407" height="457" alt="image" src="https://github.com/user-attachments/assets/e3a09412-2477-4885-8b7e-2b9ba4896ccc" />


- On VirtualBox for server 2016, go to Devices -> Network settings -> and click on Host-only adapter

<img width="556" height="315" alt="image" src="https://github.com/user-attachments/assets/f279cbc3-9ea0-4034-83ce-2beece28e0e3" />


## Install a Windows 10 machine and add it to VirtualBox

- On the newly added windows 10 machine, go to file explorer and right click on 'this pc' and click on manage. Then go to local users and groups; then go to Users. Go to properties of the Administrator account and uncheck "account is disabled" option. Then set a password on it.

<img width="558" height="535" alt="image" src="https://github.com/user-attachments/assets/f1527400-ecaf-40b7-8f91-94bb938a63f9" />


- Go to add or remove programs, then optional features, then add a feature. Then click on the RSAT tools options and add them. RSAT allows to have access to AD users and computers on a windows 10 machine.

<img width="734" height="632" alt="image" src="https://github.com/user-attachments/assets/e21f1f4e-bca3-4fca-81ef-b5a0f59cd6e1" />


- Change the network settings on the Windows 10 machine with the following settings:
  
    - IP address: 10.1.10.3
	- Subnet mask: 255.0.0.0
	- Default gateway: 10.1.10.1
	- Preferred DNS server: 10.1.10.2
	- Alternate DNS server: 10.1.10.1
  - On virtual box for windows 10, go to Devices -> Network settings -> and click on Host-only adapter
 
<img width="402" height="456" alt="image" src="https://github.com/user-attachments/assets/b4014236-9569-45bd-a71e-69b538c95036" />
<img width="558" height="507" alt="image" src="https://github.com/user-attachments/assets/27adefbe-57c5-4c37-a93f-19991bc71160" />



### Adding Windows 10 to the Domain:
- Right-click on 'this pc' and then properties -> Change settings -> Change (for changing name or adding it to a domain): In the 'member of' section, click on Domain and specify the name of the domain that was set up on the server 2016 machine (agent.com).

<img width="414" height="464" alt="image" src="https://github.com/user-attachments/assets/d4c1ea04-7c10-429c-995b-d43862a5119e" />


- To check, click on AD users and computers on the server 2016 box and go to Computers section, and the windows 10 machine should be right there.

<img width="747" height="276" alt="image" src="https://github.com/user-attachments/assets/3db7d739-bb03-49b6-ae14-5535d81de309" />


#### On Windows 10:
- Click on the AD users and computers and right-click on the domain. Go to new and then organizational unit and create a new OU called HR.

<img width="470" height="415" alt="image" src="https://github.com/user-attachments/assets/9c2479a5-977f-4c64-bc70-bd6a4c17642a" />

- Go to users and create a user account called "patty". Move this user to HR OU.

<img width="497" height="228" alt="image" src="https://github.com/user-attachments/assets/71725918-17ec-4bb8-bc2d-72d1f31dee11" />

- Create another OU called IT and add the helpdesk account to the IT OU.

<img width="532" height="235" alt="image" src="https://github.com/user-attachments/assets/78883ac9-45ef-4a32-9783-01f10977c496" />

- Make sure advanced features is enabled on AD users and computers so you can check the Attribute editor option in the properties section of the user (can achieve similar results by using the cmd command: net user 'name' /domain).

<img width="405" height="465" alt="image" src="https://github.com/user-attachments/assets/ec043718-4cb1-4c0d-9383-b94bc293baf7" />
<img width="792" height="604" alt="image" src="https://github.com/user-attachments/assets/6f4da3f5-eeb7-43d4-97f7-9dd80018e174" />


#### Checking policies:
- Right-click on a user and go to 'All tasks' and then click on 'Resultant Set of Policy (Logging)'. It shows the group policy of that user account.

<img width="839" height="429" alt="image" src="https://github.com/user-attachments/assets/9657d7ea-0a56-4284-9655-dc6b2b583171" />

- From the windows 10 machine, go to Server Manger, then 'Tools', then 'group policy management'. It shows the group policy of the domain controller.
- From the default domain policy, go to settings to see the policy settings.

<img width="755" height="525" alt="image" src="https://github.com/user-attachments/assets/b262f343-a933-488e-890b-6d84859ed865" />

- Right-click on default domain policy and go to Edit. Go to the security settings and then account policy then account lockout policy. Form there you can apply settings for things like account lockout duration, threshold, etc. From the password policy settings, you can apply the settings for password stuff. Can double check for the changes in the default domain policy.

<img width="787" height="345" alt="image" src="https://github.com/user-attachments/assets/dcf4b1f3-e888-44cf-ac76-0c54c137ff94" />
<img width="770" height="238" alt="image" src="https://github.com/user-attachments/assets/7bb02826-62c4-4c2f-ab79-776159e49a7b" />


### Add another Windows 10 (Desktop2) on VirtualBox and add it to the Domain:
- Set a static IP with the following network settings:
  
    - IP address: 10.1.10.4
	- Subnet mask: 255.0.0.0
	- Default gateway: 10.1.10.1
	- Preferred DNS server: 10.1.10.2
	- Alternate DNS server: 10.1.10.1

<img width="398" height="457" alt="image" src="https://github.com/user-attachments/assets/79b9b230-4790-4fe7-b298-12489b067da7" />

  - On virtual box for Desktop2, go to Devices -> Network settings -> and click on Host-only adapter

<img width="621" height="333" alt="image" src="https://github.com/user-attachments/assets/aff67ca9-cd8f-4ed2-b300-3d3817860a7e" />


- Patty user account was created before. Log into Desktop2 as Patty.

<img width="761" height="601" alt="Image" src="https://github.com/user-attachments/assets/f81d9ede-4d82-41d4-a212-80ac99f7e844" />


### Account locked out scenario:
- To fix this, go to the server 2016 and then go to AD users and computers. Go to the properties of the locked user and click on Account and then click on unlock account.

<img width="406" height="408" alt="image" src="https://github.com/user-attachments/assets/83cd9ed8-8da8-4cc8-ba23-324ccb4a5e31" />

- The account can also be disabled by right clicking on the user. Can enable it in the same way. If it needs a password reset, then it can be done so in the same way.

<img width="379" height="367" alt="image" src="https://github.com/user-attachments/assets/add05b56-a0ff-4a5a-b019-773cf77b4c42" />

- If account has expired, you can click on 'Never' in the 'Account expires' setting.

<img width="375" height="92" alt="image" src="https://github.com/user-attachments/assets/0a99794c-5268-479c-9013-d743b4764f7b" />


### Computer somehow getting removed from Domain scenario:
- In this case, try to locally log in. On the login screen, in the username section, type: ".\administrator" and press enter.

<img width="511" height="492" alt="image" src="https://github.com/user-attachments/assets/b7bc170f-2b04-448b-8d62-5cab8c7681de" />

- Then once logged in, go to properties from 'This PC' and click on change settings. Put the computer on the "WORKGROUP" and then back on the domain with the specified domain name.
<img width="410" height="462" alt="image" src="https://github.com/user-attachments/assets/24378ea8-2ea3-44ae-b0a0-268827f5b653" />

<img width="412" height="464" alt="image" src="https://github.com/user-attachments/assets/649512cf-0a00-4ac7-aa5d-aa77ce24801d" />

### Shares:
- On the server 2016, go to Server Manager and then click on File and Storage Services. Then go to Shares and right click on Shares and click on new share. Keep clicking next and name the share "HR". Complete it by clicking on the next options. Create a "personal" share in the same way. In the C: drive by default it should have shares folder and inside you should see Personal and HR folders.

<img width="769" height="520" alt="image" src="https://github.com/user-attachments/assets/9bb2a5f6-7301-4fec-b536-a394c2905419" />
<img width="784" height="352" alt="image" src="https://github.com/user-attachments/assets/8ea29ede-b9c1-439a-bfea-34fb064a8cf3" />

- Go to AD users and computers. Right-click on users and then go to "New" and then "Group". The group type should be security and the name should be HR. If you double click on this HR group and then go to "managed by", you can put the name of "helpdesk" in that name section. Make a "personal" group in the same way. Now go to "This pc" and you can go to the properties of HR and personal folders and click on sharing. Copy the network path, and paste it in the description section of the properties of the groups that are in AD users and computers. This is just to label it. Now from AD users and computers, add patty to the "members" section of the HR and personal group.

<img width="727" height="464" alt="image" src="https://github.com/user-attachments/assets/aa50b31e-1ab1-4ec7-b76d-d264a194917e" />
<img width="401" height="480" alt="image" src="https://github.com/user-attachments/assets/97068961-b08c-4560-b4d7-1b6f0b446aae" />
<img width="359" height="333" alt="image" src="https://github.com/user-attachments/assets/16a0a9d3-adf6-453f-ac06-95a7e2226569" />
<img width="406" height="355" alt="image" src="https://github.com/user-attachments/assets/72935060-4a65-4cfa-bc6f-82f94350fed6" />
<img width="402" height="477" alt="image" src="https://github.com/user-attachments/assets/60b6bcdb-245a-4a3b-b401-e29fef7bcbda" />
<img width="403" height="478" alt="image" src="https://github.com/user-attachments/assets/7b373363-6dc7-4a8a-89e2-e8bd6253d0b2" />


- From "This pc", go to the personal folder properties. Go to security and then advanced. Click on disable inheritance. Click on 'Convert inherited permissions into explicit permissions on this object'. Under Permissions, click on "add" and then 'Select a principle'. Type in "helpdesk". Click on "modify" for basic permissions. Type in "personal" in the same process. Now go to sharing in properties and the "personal" group should have permission level "read/write". Then click on share. Now do the same thing for the 'HR' network share folder. If this is done correctly, the shared folder should be accessed by patty on her computer (Desktop2) with the network share location. In the file explorer type: "\\server2016\hr". To create a shortcut, you can drag and drop it in the quick access location. To map it, right click on "this pc" and then go to map network drive. Paste the network drive location and the new drive should be there.

<img width="761" height="512" alt="image" src="https://github.com/user-attachments/assets/9a336659-3712-4a4b-ac6a-b8f1a854cefc" />
<img width="465" height="283" alt="image" src="https://github.com/user-attachments/assets/86ad4998-ad43-4dc4-a61d-05623853b2d7" />
<img width="915" height="593" alt="image" src="https://github.com/user-attachments/assets/2521d716-d781-4d9e-87ee-86251659337f" />
<img width="616" height="446" alt="image" src="https://github.com/user-attachments/assets/56e9f4f5-93b6-44a3-a660-af21f48cc291" />
<img width="630" height="451" alt="image" src="https://github.com/user-attachments/assets/4625d2bc-7c75-43c9-a528-85b17c038a26" />
<img width="784" height="137" alt="image" src="https://github.com/user-attachments/assets/21b6b1ea-f92d-48ed-a775-eada098529c6" />
<img width="789" height="416" alt="image" src="https://github.com/user-attachments/assets/fcd61674-15de-46e5-b711-9c1d96a5f258" />
<img width="783" height="585" alt="image" src="https://github.com/user-attachments/assets/2ca4bd9d-02d2-4650-831d-1d14237453dc" />
<img width="633" height="144" alt="image" src="https://github.com/user-attachments/assets/09dbc723-13fe-4bea-9b17-8f4133eab30d" />


- You can also map a drive from AD. On server 2016, go to AD users and computers and go to the properties of patty and click on profile. In the home folder, click on connect. Type in `\\Server2016\Personal\%username%`. Now it should create a folder for patty. 

<img width="408" height="566" alt="image" src="https://github.com/user-attachments/assets/0dc1170b-8372-4eb7-a960-2ff951dc47c1" />
<img width="701" height="193" alt="image" src="https://github.com/user-attachments/assets/2cfd3f07-83d1-4efc-ad8a-bd4d687253e9" />

### Remote settings:
- In Desktop2 computer, go to properties from "this pc" and then go to remote settings. Enter the helpdesk account's credentials. Click on Allow remote connections to this computer. Open up remote desktop connection on the windows 10 machine (Helpdesk's machine) and enter the IP of desktop2 or the name of the computer which is Desktop2. If the remote desktop doesn't work, may need to do "ipconfig /flushdns" in cmd.

<img width="327" height="492" alt="image" src="https://github.com/user-attachments/assets/d8d136cb-aaad-4003-bb1d-c33c07b221be" />
<img width="418" height="467" alt="image" src="https://github.com/user-attachments/assets/aa2ec65f-5859-40d5-ad35-5b109ae5d2f3" />
<img width="412" height="253" alt="image" src="https://github.com/user-attachments/assets/3c5971c2-932f-4034-be44-1ef7691bcfdf" />
<img width="995" height="755" alt="image" src="https://github.com/user-attachments/assets/ee894da0-4287-4931-bda1-0e3df10d7826" />
<img width="772" height="405" alt="image" src="https://github.com/user-attachments/assets/16cb639d-4ae0-4247-b2f1-fe1c057d0378" />
<img width="896" height="714" alt="image" src="https://github.com/user-attachments/assets/06bdccc6-0bc8-4c22-8180-c219d5efade4" />

-  On windows 10 machine, type in \\desktop2\c$ and it should allow access to the contents of the C: drive of Desktop2. You can upload or delete files remotely that way. 

<img width="787" height="433" alt="image" src="https://github.com/user-attachments/assets/db76f02f-3f89-4475-a82a-267d47f7e75f" />

### Group Policy Management
- On server 2016, from the server manager, go to group policy management. Right-click on group policy objects and click on new. Name it task manager. Now click on the task manager and go to delegation. Add patty to it. Then right-click on the Task manager and click on edit. Under user configuration find System and under it, there should be 'Ctrl+Alt+Del'. From there, Task manager can be removed. Move the 'Task Manager' policy object that was created under Group policy objects to the HR OU under the domain. Now right click on the task manager policy and click on Enforced.

<img width="754" height="531" alt="image" src="https://github.com/user-attachments/assets/9a34606f-3752-4115-b13f-a39cad1c122f" />
<img width="742" height="325" alt="image" src="https://github.com/user-attachments/assets/3625b9ff-07e0-449f-85a1-d017dfbc04d0" />
<img width="789" height="431" alt="image" src="https://github.com/user-attachments/assets/f8bdfbea-4199-4337-8076-d10d72e374fa" />
<img width="689" height="209" alt="image" src="https://github.com/user-attachments/assets/0fbda88c-f0f7-48a3-8002-df1f9c09b9a5" />
<img width="754" height="383" alt="image" src="https://github.com/user-attachments/assets/b82ce4ea-bce6-44c7-8419-4cffd13b1d70" />


- In the Desktop2 machine, go to cmd and type in "gpupdate /force". You can run "gpresult /r" to see what policies are running on the machine (Task Manager group policy object should be listed there). Can try to double check that task manager is actually removed by typing 'taskmgr' in cmd on Desktop2. You can also generate a report by right clicking on the group policy results and then going to group policy results wizard. Type in the name of the computer and then select a specific user and it should generate a report. Another way to see report is to go to AD users and computers first. Then click on 'All tasks' by right clicking on patty. Click on resultant set of policy wizard. Type in the name of the computer and select patty for user and finish. Now in the resultant set of policy, the configurations or changes can be seen. 

<img width="470" height="196" alt="image" src="https://github.com/user-attachments/assets/a3989277-ec20-4e7a-bdb8-5be28ecbab7b" />
<img width="641" height="670" alt="image" src="https://github.com/user-attachments/assets/6760acff-3ba8-4b6a-b301-289390db6b83" />
<img width="445" height="260" alt="image" src="https://github.com/user-attachments/assets/09c21e3c-63a8-4c62-a4fd-f25c594da002" />


### Remote App Deployment
- Install PDQ Deploy and PDQ Inventory on Server 2016.
- Open up PDQ Inventory and go to 'All computers'. Right-click and click on add computers. Then Desktop2 can be added by name. After Desktop2 is added, you can right-click on it and then click on "Tools". From there, you can send remote commands if needed such as Reboot/Shutdown, Remote Assist, Remote Desktop, Run Command etc.

<img width="1019" height="646" alt="image" src="https://github.com/user-attachments/assets/619610df-45c6-460d-a53e-d03caee1feb7" />
<img width="1016" height="387" alt="image" src="https://github.com/user-attachments/assets/5805c3b1-fa45-4333-ab5b-0009a85c1982" />
<img width="526" height="159" alt="image" src="https://github.com/user-attachments/assets/e49471d2-0e36-45c9-9c48-a893372f7fc4" />
<img width="631" height="520" alt="image" src="https://github.com/user-attachments/assets/89bb2f38-5db1-4950-b3c0-f1ff03e6e001" />


- To deploy apps, rigtht-click on Desktop2, and go to "Tools". Then click on PDQ Deploy. That will open up the PDQ Deploy software. Packages can be downloaded from the Package library, and then you can deploy it by right clicking on the package and then clicking on 'Deploy Once'. Then you can add the computer by name (the target where apps will be deployed). After that, click on 'Deploy Now'. Once it's deployed, it should show up on the Desktop2 machine (PDFsam Basic was deployed as an example in this case). 

<img width="847" height="629" alt="image" src="https://github.com/user-attachments/assets/bbf16bfe-d18e-4d65-961d-069b98e11ebc" />
<img width="886" height="529" alt="Image" src="https://github.com/user-attachments/assets/4741e906-9e48-4002-a1e5-9e784e307c20" />
<img width="487" height="198" alt="image" src="https://github.com/user-attachments/assets/becb842f-2467-4430-9580-2c975ec137ec" />
<img width="956" height="675" alt="image" src="https://github.com/user-attachments/assets/53597cbb-ecbd-40f1-83bd-00907016fda6" />


### Print Management
- On server 2016, in the server manager, go to manage, then 'add roles and features'. Select 'print and document services'. Now go to 'Tools' and then 'print management'. In the 'Printers' section under the 'Print Servers', right-click and click on 'Add a printer'. Then select install a new driver. Pick the right printer.

<img width="782" height="569" alt="image" src="https://github.com/user-attachments/assets/b91c8bd4-cf22-47a2-b2b1-a178e0bf39ff" />
<img width="420" height="203" alt="image" src="https://github.com/user-attachments/assets/4d013806-9d5c-4941-b208-b1b81039193f" />
<img width="583" height="448" alt="image" src="https://github.com/user-attachments/assets/9603cc9c-5828-4a8d-9c9c-33d40709199f" />
<img width="576" height="413" alt="image" src="https://github.com/user-attachments/assets/7028c3b1-7f83-449a-9251-7c4d9c82b53a" />
<img width="572" height="403" alt="image" src="https://github.com/user-attachments/assets/1bbebd1b-43f2-4a15-8a2d-69c78784edd8" />
<img width="556" height="140" alt="image" src="https://github.com/user-attachments/assets/54f78f75-560e-428a-b381-62a9a751dd60" />


- The printer should show up now; right-click on it and go to properties and then 'Sharing'. Click on share this printer. Add the HR group to the printer by going to the 'Security' tab. You can also list it in directory to make it appear in AD (it would be in users and computers printer section which can be found by right clicking on the domain).

<img width="464" height="507" alt="image" src="https://github.com/user-attachments/assets/ca7a6096-d724-42db-b21b-0b94f612c2da" />
<img width="464" height="511" alt="image" src="https://github.com/user-attachments/assets/94e4f951-cb7b-4799-9340-6a6a91a43adf" />

- Now on Desktop2, patty can see the printer. It should show up automatically when adding the printer.

<img width="608" height="246" alt="image" src="https://github.com/user-attachments/assets/1aa4ea95-f3ec-4379-be6c-4f12665846b7" />


### Limited Permissioning 
- On server 2016, go to AD users and computers. Right-click on users and click on new and make a new user. Name him Scott. Create a new OU called consultants and put Scott in there.

<img width="584" height="261" alt="image" src="https://github.com/user-attachments/assets/39843f8a-6362-4c2c-929c-61408381203e" />

- Now right-click on the domain and then click on 'delegate control'. Add Scott and then give him permission to only 'Reset user passwords and force password change at next logon'.

<img width="602" height="510" alt="image" src="https://github.com/user-attachments/assets/f4c87b40-74da-4bd1-bb57-5da23249ba9a" />

<img width="501" height="388" alt="image" src="https://github.com/user-attachments/assets/318954b4-8895-41d7-ac3d-faa6ee4384af" />
<img width="498" height="388" alt="image" src="https://github.com/user-attachments/assets/7abeaac6-f8a6-4779-8dbd-7b59c59659a0" />


- To test it, log in as scott in the windows 10 machine. Then go to AD users and computers. Go to the properties of a user and when you go to account, everything should be greyed out except for the password change settings. Resetting password is the only thing Scott can do and nothing else.

<img width="402" height="493" alt="image" src="https://github.com/user-attachments/assets/19ac4d4e-b586-4fbd-8f89-3e32b88bc623" />

