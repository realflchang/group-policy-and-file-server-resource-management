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

<p>9.	Right click on “Default Domain Controllers Policy”, and select “Edit..”.  We can take a look at some existing GPO policies and edit them if necessary:</p>
<img src="https://github.com/user-attachments/assets/253b7afc-725d-4115-8017-71c573e15f2e" alt="View some GPOs" /><br />

<p>10. The Group Policy Editor appears:</p>
<img src="https://github.com/user-attachments/assets/434d8ccf-bbd2-4a09-b7b1-0d19059d5b77" alt="Group Policy Editor appears" /><br />

<p>11.	Here we can browse some of the default GPOs:</p>
<img src="https://github.com/user-attachments/assets/29169eeb-3d87-4ad1-a950-47ecbb496502" alt="See some of the default GPOs" /><br />

<p>12. Let’s define some GPOs but they will not be implemented yet until later. Let’s set up a Password Policy GPO to enforce strong passwords and enhance internal security. </p>
   a.	Back in the GPM, right-click on the domain name, select “Create a GPO…”<br />
<img src="https://github.com/user-attachments/assets/b18226cb-7796-4b3b-bcd9-746f346017e7" alt="GPM Create" /><br />

   b. Enter "Password Policy":<br />
<img src="https://github.com/user-attachments/assets/ab031aa4-1d5c-449b-8fa8-58281a29f4df" alt="Enter Password Policy" /><br />

   c.	New policy appears in the domain:<br />
<img src="https://github.com/user-attachments/assets/39aa777c-b25c-4ea2-b4ad-8019a951bd15" alt="New policy appears" /><br />

   d.	Right-click on the new policy, and click “Edit…”:<br />
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

   a.	Back in GPM, right-click on the domain, click Edit…:<br />
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

























