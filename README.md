<h1>Active Directory in Azure - Group Policy Management and File Server Resource Management</h1>
This tutorial supplements the previous Active Directory tutorial on how to manage Group Policy and manage basic file systems. 
These tools help manage the corporate network system on top of the features provided with Active Directory. 
The policies added here will be reflected in our Client machine(s) in the same virtual network.<br />

<!---
# (<h2>Video Demonstration</h2>

- ### [YouTube: How To Configure osTicket, post-installation](https://www.youtube.com) -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt or PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10</b> (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - have the same setup as the [previous tutorial on Active Directory](https://github.com/realflchang/configure-ad).
- Step 2 - install Group Policy Management and File Server Resource Manager
- Step 3 - set up some Group Policy Objects (GPOs) and test them
- Step 4 - set up some items in File Server Resource Manager

<h2>Deployment and Configuration Steps</h2>

<p>1. Set up DC1 VM and Client1 VM as before.</p>

<p>2. Begin setting up the Group Policy Management (GPM) and File Server Resource Manager (FSRM). In our DC1, Server Manager in the top right, click on Manage, Add Roles and Features:</p>
<img src="https://github.com/user-attachments/assets/a3542ce3-7bbf-4a97-9d0c-683fd5297fb0" alt="Add Roles and Features" /><br />
<img src="https://github.com/user-attachments/assets/f0d7d656-d527-4cae-a75a-fdd6a7bc1fcf" alt="Begin wizard" /><br />
<img src="https://github.com/user-attachments/assets/982a9d36-2f8e-43cf-a0e4-40cdc3b49722" alt="Select installation type" /><br />
<img src="https://github.com/user-attachments/assets/a01144cc-360d-4ff6-99a1-04475b46c721" alt="Select destination server" /><br / >

<p>3. Select File Server Resource Manager, then Next:</p>
<img src="https://github.com/user-attachments/assets/37a05c02-6eac-41d4-b8fc-cec5f11d060f" alt="Select File Server Resource Manager" /><br />
<img src="https://github.com/user-attachments/assets/10464d6f-afcb-49de-b919-9c73dc4817b5" alt="Add Features also" /><br />
<img src="https://github.com/user-attachments/assets/0ba8ac94-0e42-47fb-821f-3de313fa05b3" alt="Select server roles" /><br />

<p>4. Select Group Policy Management:</p>
<img src="https://github.com/user-attachments/assets/cd6787e3-93a3-40d6-97b7-b5d8aa6ebf6e" alt="Select Group Policy Management" /><br/>
<img src="https://github.com/user-attachments/assets/9983f6a1-1d27-42ec-b365-af9e8943a095" alt="Active Directory Domain Services" /><br />
<img src="https://github.com/user-attachments/assets/62d4f877-a856-4c82-b51e-f91ce1ec7cfe" alt="Custom installation selections" /><br />

<p>5. Wait for the installation to finish:</p>
<img src="https://github.com/user-attachments/assets/9764c3af-9a11-4c5f-9b4a-9db73c967a54" alt="Installation progress" /><br />

<p>6. Go to our Active Directory Users and Computers</p>
<img src="https://github.com/user-attachments/assets/dc061ec9-99ee-4e7d-a16d-c879e475e242" alt="Go to Active Directory Users and Computers" /><br />

<p>7. Set up Organizational Units (OUs) and Users. For example, an office in “NY” and an office in “Chicago”. I proceeded to add 2 users, NY Adam Apple (Domain Admin) and NY Maria Young (regular Domain User, also member of “NYSales” group):</p>
<img src="https://github.com/user-attachments/assets/de815394-5292-4dc4-ba60-da89c96cb9fc" alt="Set up Organizational Units" /><br />

<p>8. Let's set up some policies with Group Policy Management (GPM):</p>
<img src="https://github.com/user-attachments/assets/b9b926b3-9130-4c62-843c-5517fd0c6fe7" alt="Go to Group Policy Management" /><br />
<img src="https://github.com/user-attachments/assets/0187e453-7ab1-4bd6-a985-ef06e16ed8fb" alt="GPM screen" /><br />

<p>9.	Right click on “Default Domain Controllers Policy”, and select “Edit...”.  We can take a look at some existing GPO policies and edit them if necessary:</p>
<img src="https://github.com/user-attachments/assets/253b7afc-725d-4115-8017-71c573e15f2e" alt="View some GPOs" /><br />

<p>10. The Group Policy Editor appears:</p>
<img src="https://github.com/user-attachments/assets/434d8ccf-bbd2-4a09-b7b1-0d19059d5b77" alt="Group Policy Editor appears" /><br />

<p>11.	Here we can browse some of the default GPOs:</p>
<img src="https://github.com/user-attachments/assets/29169eeb-3d87-4ad1-a950-47ecbb496502" alt="See some of the default GPOs" /><br />

<p>12. Let’s define some GPOs but they will not be implemented yet until later. Let’s set up a Password Policy GPO to enforce strong passwords and enhance internal security. </p>
   a.	Back in the GPM, right-click on the domain name, select “Create a GPO...”<br />
<img src="https://github.com/user-attachments/assets/b18226cb-7796-4b3b-bcd9-746f346017e7" alt="GPM Create" /><br />

   b. Enter "Password Policy":<br />
<img src="https://github.com/user-attachments/assets/ab031aa4-1d5c-449b-8fa8-58281a29f4df" alt="Enter Password Policy" /><br />

   c.	New policy appears in the domain:<br />
<img src="https://github.com/user-attachments/assets/39aa777c-b25c-4ea2-b4ad-8019a951bd15" alt="New policy appears" /><br />

   d.	Right-click on the new policy, and click “Edit...”:<br />
<img src="https://github.com/user-attachments/assets/92eff0ed-f8f1-4fb7-9821-45470adc8d58" alt="Edit policy" /><br />

   e.	This will bring up our Editor, where we can specify our policy:<br />
<img src="https://github.com/user-attachments/assets/ce0e438a-7c5e-4d8e-94d8-aacb888a04fc" alt="Editor" /><br />

   f.	Since this policy is for the computers, we navigate to Computer Configuration, Policies, Windows Settings, Security Settings, Account Policy:<br />
<img src="https://github.com/user-attachments/assets/8dabf563-aea8-427c-95f6-164966f86e92" alt="Password Policy" /><br />

   g.	Here we can define some attributes, such as password length, age, password complexity (ie. need combinations of letters, numbers, symbols)<br />
<img src="https://github.com/user-attachments/assets/f4e1b4c8-ba93-4809-a5cc-7505ca4bc8b8" alt="Minimum password length Properties" /><br />
<img src="https://github.com/user-attachments/assets/90645eab-ac17-4bf6-beb3-9e4c27e4db02" alt="Must meet complexity Properties" /><br />
<img src="https://github.com/user-attachments/assets/60884b81-292e-4ff8-a7bd-8a6058915865" alt="Maximum password age Properties" /><br />
<img src="https://github.com/user-attachments/assets/997b72cf-7463-485b-9e74-123279460477" alt="Edited policies" /><br />

<p>13.	Let’s create a mapped network drive that all domain users will have access to once they log in:</p>

   a.	Back in GPM, right-click on the domain, click Edit...:<br />
<img src="https://github.com/user-attachments/assets/24d362f4-87af-46a0-8790-da946f90891c" alt="GPM Edit" /><br />

   b.	Provide a descriptive name:<br />
<img src="https://github.com/user-attachments/assets/4f72d85e-4590-4a96-af58-215787342735" alt="GPO Name" /><br />

   c.	Back in the GPM, right click on the GPO just created, and click Edit:<br />
<img src="https://github.com/user-attachments/assets/135dec16-12f5-463e-8925-a9c294b436ca" alt="Edit" /><br />

   d.	Here we navigate to User Configuration, Preferences, Windows Settings, Drive Maps:<br />
<img src="https://github.com/user-attachments/assets/ee7f2b58-ba01-4b64-affc-966df186ebd3" alt="Drive Maps" /><br />

   e.	Provide the Location (full network path to the shared folder), Label as, & drive letter:<br />
<img src="https://github.com/user-attachments/assets/56a0cca3-a839-448e-af8b-f333a49e1656" alt="New Drive Properties" /><br />
<img src="https://github.com/user-attachments/assets/537ee8c2-298b-4f4a-bcd6-15b5c8c3fd09" alt="Drive Properties filled" /><br />
<img src="https://github.com/user-attachments/assets/a0e2c79f-19b5-46e3-8693-d51fffe48ead" alt="Drive Maps S" /><br />

   f.	Shared drive now appears when logged into a Client VM machine after restarting:<br />
<img src="https://github.com/user-attachments/assets/c365943b-5f74-4740-9ec1-79e7ef54de23" alt="Client VM with mapped S drive" /><br />

<p>14.	Let’s define a GPO to set a default Desktop wallpaper for all users for a professional look:</p>

   a.	Back in GPM, right-click on domain name, click “Create a GPO...”:<br />
<img src="https://github.com/user-attachments/assets/9f7491fb-82d7-4591-829c-46bd0edc2a5d" alt="GPM Edit" /><br />
<img src="https://github.com/user-attachments/assets/84f17859-66f5-468f-afa7-6e38f6ffa7f7" alt="Name GPO" /><br />

   b.	Right-click on the new GPO and click Edit...:<br />
<img src="https://github.com/user-attachments/assets/3ebcf3a4-88d8-49a1-8e9c-1710ea80d1db" alt="Click Edit" /><br />

   c.	Navigate to User Configuration, Policies, Admin…, Desktop, Desktop, Desktop Wallpaper:<br />
<img src="https://github.com/user-attachments/assets/c2685c8d-4d91-48bb-bf4d-5fc5c33067a7" alt="Define GPO Desktop Wallpaper" /><br />

   d.	Click Enable, provide full path to the wallpaper:<br />
<img src="https://github.com/user-attachments/assets/e881bd9e-7bcb-4dad-a5ce-6c3c0cb9fbdf" alt="Define wallpaper for GPO" /><br />

<p>15.	Let’s define a GPO to restrict access to Control Panel:</p>

   a.	Back in GPM, right-click on domain and click “Create a GPO...”:<br />
<img src="https://github.com/user-attachments/assets/54e9f116-f574-4ca4-a89a-da5cade128ff" alt="Create GPO" /><br />

   b.	Provide a descriptive name:<br />
<img src="https://github.com/user-attachments/assets/59a19de5-6756-4976-9961-507833b1ff03" alt="Name GPO" /><br />

   c.	Right-click on it, click Edit…:<br />
<img src="https://github.com/user-attachments/assets/b0759cc2-7b24-4f1f-a227-5145704fbcfe" alt="Click Edit" /><br />

   d.	Navigate to User Configuration, Policies, Admin…, Control Panel, Prohibit access…, Edit policy setting:<br />
<img src="https://github.com/user-attachments/assets/7b3a8f67-eb0c-4823-933d-81a825e7df4e" alt="Define GPO Access to Control Panel" /><br />

   e.	Click “Enabled” to allow the policy, ie. prohibit access to Control Panel:<br />
<img src="https://github.com/user-attachments/assets/d63da573-0700-4101-84be-b2e54613624c" alt="Click Enable to allow GPO" /><br />

<p>16.	Let’s define a GPO to disable USB storage:</p>

   a.	Back in GPM, right-click on domain name, then “Create a GPO...”:<br />
<img src="https://github.com/user-attachments/assets/f5435e8f-cf8d-4900-a6ff-b6f69e6583d3" alt="Create GPO" /><br />

   b.	Provide a descriptive name:<br />
<img src="https://github.com/user-attachments/assets/86172b66-3581-4c95-b98f-80eaba5b9c63" alt="Name GPO" /><br />

   c.	Right-click on it, and click Edit...:<br />
<img src="https://github.com/user-attachments/assets/c9a25503-242c-4926-8913-5729bcbfcd66" alt="Click Edit" /><br />

   d.	Navigate to Computer Configuration, Admin…, System, …Removable Storage Access:<br />
<img src="https://github.com/user-attachments/assets/8aa5c4a3-9207-4579-becc-4bf9f3c74026" alt="System menu" /><br />
<img src="https://github.com/user-attachments/assets/869bf5ed-fc0e-4d5b-9d5e-687fe192d241" alt="Removable Storage Access menu" /><br />

   e.	Here we click on All Removable Storage classes: Deny all access, Edit policy setting:<br />
<img src="https://github.com/user-attachments/assets/2907d5e0-344a-4c32-9f6e-c35a5037ed15" alt="Removable Storage Access settings" /><br />

   f.	Click Enable to allow the policy (ie. disable USB storage devices):<br />
<img src="https://github.com/user-attachments/assets/1623f83c-9623-4236-924d-789ec271a097" alt="Click Enable to allow policy" /><br />

<p>17.	At this point I have defined the following GPOs:</p>

<img src="https://github.com/user-attachments/assets/635d7e15-470e-4f93-a834-8e00bcf2d707" alt="Show defined GPOs" /><br />

<p>18.	If we want to Restrict Control Panel for … NY Users, we can drag the GPO into the NY\Users folder in GPM:</p>

<img src="https://github.com/user-attachments/assets/1e4afb17-b54c-4d11-8ca4-817b538ce58b" alt="Link the GPO?" /><br />

<p>19.	Click OK on the confirmation:</p>

<img src="https://github.com/user-attachments/assets/fb783438-0492-4a3f-9383-8ce2ba59d971" alt="Click OK" /><br />

<p>20.	To test these policies, I go back to my Client VM:</p>

<img src="https://github.com/user-attachments/assets/f4f54e7f-5cf9-4bc0-9708-86280ac0fa7b" alt="Control Panel still showing" /><br />

<p>21.	Note that the policy still has not been enforced yet. Normally it may take about 90 minutes. </p>

<p>22.	To force the policy, we go to the client VM command prompt, and enter “gpupdate /force”:</p>

<img src="https://github.com/user-attachments/assets/cba585be-ee58-4b3e-a5e6-c2114c234186" alt="Run gpupdate /force" /><br />

<p>23.	Now when trying to reopen Control Panel, we get a message indicating it is restricted:</p>

<img src="https://github.com/user-attachments/assets/744f9275-be9f-4968-a245-c6d665ab6f9c" alt="Command Prompt cancelled" /><br />

<p>24.	To remove the GPO policy, I edit the GPO to disable, and then reapplied the policy back to NYSales, and redo gpupdate /force in the client VM command prompt. </p>

<p>25.	To have the Start Drive Mapping GPO policy applied to an OU, back in GPM drag the GPO into the OU:</p>

<img src="https://github.com/user-attachments/assets/f9531bda-7dc4-4025-af58-0ba75b5d007f" alt="Apply a GPO to an OU" /><br />

<p>26.	This GPO policy will apply to Users in the NY OU.</p>

<p>27.	Implement quotas on the SHARED drive. Since hard drive space is limited, we do not want users too much access to it, as it will affect performance. For this, we will use the File Server Resource Manager (FSRM).  </p>

<img src="https://github.com/user-attachments/assets/7c2b9a86-0726-4666-adbf-41831fd334c8" alt="File Server Resource Manager menu" /><br />
<img src="https://github.com/user-attachments/assets/4fbb7eec-e94e-40a4-a180-52800efbf1cc" alt="File Server Resource Manager" /><br />

<p>28.	In FSRM, Quota Management, Quotas, right-click and select Create Quota...:</p>

<img src="https://github.com/user-attachments/assets/58392d0d-d959-4691-bd38-dff5d62b312e" alt="Create Quota" /><br />

<p>29.	Browse the Quota path to our SHARED folder, and specify the limit:</p>

<img src="https://github.com/user-attachments/assets/e526dba6-0bf7-4fbb-9113-aaaa74a1bcd9" alt="Before setting quota" />
<img src="https://github.com/user-attachments/assets/00c53210-8ecf-4f19-a7d3-ab9996c5855c" alt="After setting quota" /><br />

<p>30.	Quota now set for our SHARED folder:</p>

<img src="https://github.com/user-attachments/assets/4a8a5f6f-b34e-4cd3-894e-e2c68803ce36" alt="FSRM After Setting Quota" /><br />

<p>31.	Next, we can limit the file types allowed in our SHARED folder. While still in the FSRM, go to File Screening Management, File Screens</p>

<img src="https://github.com/user-attachments/assets/fdc8beb2-32b2-48b5-a0f3-69b302f4daa0" alt="File Screen Templates" /><br />

<p>32.	Let’s block all Audio and Video files. Right-click and select Create File Screen...:</p>

<img src="https://github.com/user-attachments/assets/5173afa3-aaef-4801-a7c8-0dc3fc827260" alt="Create File Screen" /><br />

<p>33.	Provide the File screen path (to our SHARED folder), select the types to block:</p>

<img src="https://github.com/user-attachments/assets/88b978aa-4469-4ed1-a6d4-8391f93f4d2b" alt="Create File Screen options" /><br />
<img src="https://github.com/user-attachments/assets/bd083114-d590-4c2c-8240-d53c6f498804" alt="Created File Screen" /><br />

<p>34.	Let’s test it at our client VM. For example the following appears when trying to copy an audio file:</p>

<img src="https://github.com/user-attachments/assets/f00499f0-478c-41f2-831c-a1dfe50878b1" alt="Need permission" /><br />

<p>35.	Here are a few other options for File Screening:</p>

<img src="https://github.com/user-attachments/assets/435802e1-41e9-4112-9a28-baf00cd365b6" alt="Other File Screen options" /><br />

<p>36.	Once I remove the File Screen restriction, I can copy the test audio file to our SHARED folder from our client VM:</p>

<img src="https://github.com/user-attachments/assets/3998e979-6047-409f-b593-7d364b5fde4f" alt="Copied audio file to SHARED drive" /><br />

