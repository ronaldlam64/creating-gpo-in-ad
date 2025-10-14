<p align="center">
<img src="https://i.imgur.com/RgTEis3.png" alt="Active Directory logo"/>
</p>

<h1>Active Directory Lab - How to create and apply a GPO</h1>
This tutorial will outline how to create a Group Policy Object and how to apply the GPO in an Active Directory Domain. 

A Group Policy Object (GPO) is a set of rules in Windows Server environments used to manage and control user and computer settings across a network.

GPOs let administrators centrally configure things like security settings, software installations, and desktop configurations for multiple devices or users. 
They’re applied through Active Directory, ensuring consistent policies across the organization.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- VMWare (or Oracle Virtualbox)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Windows Server 2022

<h2>List of Prerequisites</h2>

- Microsoft Azure
- Azure Virtual Machine
- VMWare or Oracle Virtualbox (To configure the Azure VMs)
- <a href="https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html" target="_blank">Download link for VMWare</a>
- <a href="https://www.virtualbox.org/wiki/Downloads" target="_blank">Download link Oracle Virtualbox</a>
- <a href="https://drive.google.com/file/d/1gyYBmOUnoNJiZQi3vncEkILpBNRA1fHU/view?usp=sharing" target="_blank">Windows 10 Pro Download link</a>
- <a href="https://github.com/ronaldlam64/active-directory-deployment" target="_blank">Active Directory Installation and Setup</a>
  - **Please go through this tutorial first if you haven't setup an Active Directory lab yet.**
 
<h2>Implementation Steps</h2>

1. For this tutorial, we will create a GPO that locks a user account when they fail to sign in a certain number of times. First, type Group Policy Object in the search function in the task bar
   and open Group Policy Object. Then click the dropdown next to Domains -> dropdown next to your domain name -> Right click domain name -> Select "Create a GPO in this domain, and Link it here..."

   <img src="https://i.imgur.com/F7Lb7i8.png" alt="Open GPO" />

   Name the GPO that tells what the GPO is for. In this case, we want to create a GPO that locks out an account when they fail to sign in a certain number of times.
   I'll name this "Account Lockout."

   <img src="https://i.imgur.com/FkvNbGo.png" alt="Name GPO" />

2. Right click on the newly created GPO -> Click Edit > Click on dropdown next to Computer Configurations -> Windows Settings -> Security Settings -> Account Policies

   <img src="https://i.imgur.com/HH5WEBb.png" alt="Navigating GPO settings" />

   - In Group Policy Object (GPO), there are two main sections: Computer Configuration and User Configuration, and they differ in who or what the settings apply to:

     - Computer Configuration applies settings to computers, regardless of who logs in. It takes effect when the computer starts up and they are commonly used for security policies, software installations, or system-wide settings.

     - User Configuration applies settings to users, regardless of which computer they log into. It takes effect when the user logs on and often used for desktop backgrounds, mapped drives, or folder redirections.
    
3. Click on each Policy setting (in this case, Account lockout duration) -> Check the box for "Define this policy setting" -> set the number of minutes the account will be locked out for -> Click Apply and OK

   <img src="https://i.imgur.com/GoHZsx5.png" alt="Set Account policy setting" />

   When first defining the policy, GPO will suggest values for the other Policy settings. I'll go with these recommended values but these values can be manually changed depending on company policy.

   <img src="https://i.imgur.com/eXIxAy1.png" alt="Suggested value settings" />

   <img src="https://i.imgur.com/d7fFanz.png" alt="Defined policy settings" />

   With this GPO, a user account will lock out after the user fails to sign in 5 times and will have to wait 3 minutes before they can sign in again.
   The Account lockout threshold will reset back to 5 after 3 minutes according to the "Reset account lockout" policy.

4. The GPO will take effect and apply to users in the domain after 90 minutes, but we can make it take effect immediately by going into the client VM -> Open either Powershell or Command Line -> type and run gpupdate /force

   <img src="https://i.imgur.com/J0rPsUd.png" alt="gpupdate /force" />
