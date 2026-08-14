# Enterprise-Active-Directory-Infrastructure-and-Group-Policy-Management

## Introduction
This project demonstrates the design and deployment of a **centralized Windows enterprise environment** using Windows Server 2022 and Active Directory Domain Services (AD DS). The lab simulates the IT infrastructure of a small organization, where users, computers, security groups, and security policies are centrally managed from a Windows Server domain controller.

The project focuses on practical **system administration, identity management, endpoint management, and Group Policy administration**, providing hands-on experience with technologies commonly used in enterprise Windows environments.

## Project objectives
The main objective is to build a functional and manageable Windows domain environment while demonstrating the ability to:

- Deploy and configure **Windows Server 2022** as a Domain Controller.
- Install and configure **Active Directory Domain Services (AD DS)** and DNS.
- Design an organized **Active Directory structure** using OUs.
- Create and manage **users and security groups**.
- Join Windows client machines to the domain.
- Configure and apply **Group Policy Objects (GPOs)**.
- Manage Active Directory remotely using **RSAT**.
- Implement centralized security and workstation management.
- Test domain authentication, policy application, and administrative access.
- Troubleshoot common Active Directory and domain connectivity issues.

## Technologies & Requirements
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy Management (GPO)
- Remote Server Administration Tools (RSAT)
- Windows 10/11
- VMware Workstation 17 Pro
- PowerShell
- Windows Event Viewer

**NOTE:** Before we begin this lab, make sure you have downloaded and installed VMware workstation 17 Pro, we'll use it to host guest operating systems. Also make sure to download the ISO versions of both Windows Server 2022 and Windows 10/11. Using ISO files eliminates the need to create bootable USB drives or burn installation media to a CD/DVD.

---
### Step 1: Setting up Windows Server 2022
Open the VMware workstation and click "Create a New Virtual Machine"
![](images/server/Installation/Capture1.PNG)

Select "Typical (recommended)" and click Next
![](images/server/Installation/Capture2.PNG)

 Select "I will install operating system later option, to avoid troubles of other options"
![](images/server/Installation/Capture3.PNG)

Next, select "Microsoft Windows" as guest operating system, and Window server 2022 version. Select Next
![](images/server/Installation/Capture4.PNG)

Then give your virtual machine a name, or leave the default "Windows server 2022". You can also browse a different location for the machine installation if you wish, then click Next.
![](images/server/Installation/Capture5.PNG)

Next, specify disk capacity. The recommended maximum disk size is 60.0GB, but in this lab I will go with minimum, 20.0GB, because we're not going to install many applications. Select "split virtual disk into into multiple disk" and click Next
![](images/server/Installation/Capture6.PNG)

Review the virtual machine specifications, and click 'Finish', to create the virtual machine
![](images/server/Installation/Capture7.PNG)

Up to this stage, you have your window server 2022 virtual machine template created, and the remaining step is to select the ISO image, boot it and install the operating system. But before that, we can review and adjust configurations based on your system’s capabilities, to improve performance of our virtual machine.
You may increase CPU, RAM, and storage allocations if your machine has sufficient resources to ensure better performance. Alternatively, you can leave them at the minimum or recommended system requirements. One of the key advantages of using virtualization tools is flexibility, which means we can easily modify CPU, RAM, and storage allocations even after creating the virtual machines.
![](images/server/Installation/Capture7.5.PNG)

From the CD/DVD (SATA) tab under Connection, click on "Use ISO image file" then Browse. Select the Windows Server 2022 (ISO) that was downloaded. From the Network Adapter tab, uncheck "Connect at power on" option. This prevents Windows from attempting to download updates during installation, which will speed up the installation. Of course, updates are essential for security, but since this is a home lab environment, Windows can update itself later when we turn on the Network. Click on "Close" then "Finish".
![](images/server/Installation/Capture8.PNG)

The final template now looks like below.
Once the environment is created, click on "Power on this Virtual Machine" to begin the Operating System (OS) installation.
![](images/server/Installation/Capture9.PNG)

Quickly press "any key" when prompted to boot from the CD/ISO. If you are late to press any key to initiate the setup, you need to restart the Virtual Machine. You can do this action via VMware Workstation's menu bar: VM > Power > Restart Guest.
![](images/server/Installation/Capture9.5a.PNG)
![](images/server/Installation/Capture9.5b.PNG)

Now, go through below steps with screenshot reference to install the operating system.
Select "Language, Time and currency format, Keyboard" then click Next.
![](images/server/Installation/Capture10.PNG)

Click on "Install Now". Select an operating system with the Desktop Experience option, "Windows Server 2022 Standard Evaluation (Desktop Experience)" in our case, then Next. 
![](images/server/Installation/Capture11.PNG)
![](images/server/Installation/Capture12.PNG)

Accept the Software License Agreement and click Next. Click on "Custom: Install Microsoft Server Operating System only (advanced)" as we are installing Windows for the first time. Click Next, as it will automatically find the disk location that we created before. Once the installation finishes, it will ask us to type a password for the Administrator Account.
![](images/server/Installation/Capture13.PNG)
![](images/server/Installation/Capture14.PNG)
![](images/server/Installation/Capture15.PNG)
![](images/server/Installation/Capture16.PNG)
![](images/server/Installation/Capture17.PNG)

Now, it is ready! We have to press Ctrl+Alt+Del to enter our password for the Administrator Account. However, pressing Ctrl+Alt+Del as usual does not work in a virtual environment. To progress, click VM on the menu bar, then "Send Ctrl+Alt+Del".
![](images/server/Installation/Capture18.PNG)
![](images/server/Installation/Capture21.PNG)
![](images/server/configuration/Capture0.PNG)

### Step 2: Changing the Computer's Name
To make our work easy while working with installed window server 2022, we're going to rename our server to DC01, but it's optional.
Right click on the **window start menu** > **system** > **Rename this PC** > give the name **DC01**, Then "Next". You may be required to restart your machine for the changes to take place, just restart.
![](images/server/Installation/Capture2020.PNG)

### Step 3: Install Active Directory and Promote DC01 to Domain controller
Now that Windows Server 2022 is installed and the server has been renamed to DC01, the next step is to install **Active Directory Domain Services (AD DS)**. AD DS provides the centralized identity and resource management capabilities required for our Windows domain environment.
Open **Server Manager**. From Server Manager's menu bar, click on **Manage**, then **Add Roles and Features** to begin installing the required server role.
![](images/server/configuration/Capture2.PNG)

"Add Roles and Features Wizard" will start. Click Next to begin.
![](images/server/configuration/Capture3.PNG)

Select Role-based or feature-based installation, then click Next.
![](images/server/configuration/Capture4.PNG)

Select DC01 as the destination server and click Next.
![](images/server/configuration/Capture5.PNG)

From the available server roles, select Active Directory Domain Services (AD DS). When prompted, click Add Features to include the required management tools and dependencies.
![](images/server/configuration/Capture6.PNG)

Review the selected role and features, then click Next.
![](images/server/configuration/Capture7.PNG)

If "Group Policy Management" is unchecked, check it, then click Next.
![](images/server/configuration/Capture8.PNG)

Click Next
![](images/server/configuration/Capture9.PNG)

Click the check box "Restart the destination server automatically if required" and "Install" to begin.
![](images/server/configuration/Capture10.PNG)

Once the installation is completed, before closing the wizard, click on "Promote this server to a domain controller".
If accidentally closed the wizard, select Promote this server to a domain controller from the Server Manager notification flag to begin configuring the domain.
![](images/server/configuration/Capture12.PNG)

Under Deployment Configuration, select Add a new forest because this is the first Domain Controller in our lab environment. Enter the desired domain name, such as RoundTech.local, and click Next.
![](images/server/configuration/Capture13.PNG)

Configure the Domain Controller Options, including the forest and domain functional levels. Ensure Domain Name System (DNS) server and Global Catalog (GC) are selected, then create a secure Directory Services Restore Mode (DSRM) password.
![](images/server/configuration/Capture14.PNG)

Review the DNS configuration. A warning may appear because DNS delegation is not being configured in this isolated home lab. This can be safely acknowledged before continuing.
![](images/server/configuration/Capture15.PNG)

Review or configure the default NetBIOS domain name, then click Next.
![](images/server/configuration/Capture16.PNG)

Review the default paths for the Active Directory database, log files, and SYSVOL. For this lab, the default locations are sufficient.
![](images/server/configuration/Capture17.PNG)

Review the configuration summary to ensure the domain and Domain Controller settings are correct. Click Next to proceed.
![](images/server/configuration/Capture18.PNG)

The Prerequisites Check will verify that DC01 meets the requirements for Domain Controller promotion. Once the checks complete successfully, click Install.
![](images/server/configuration/Capture19.PNG)

The promotion process will begin. DC01 will install and configure Active Directory, DNS, the Global Catalog, and other required domain services. The server will automatically restart when the process is complete.
![](images/server/configuration/Capture20.PNG)

After successfully promoting DC01 to a Domain Controller, the server restarts to complete the configuration. Once it boots back up, the login screen will display the newly created domain context, confirming that DC01 is now part of the new Active Directory domain.
![](images/server/configuration/Capture21.PNG)

Now, one final step step to take to ensure our server is perfectly working, is to give it a static IP address, and the DNS address to point to itself, to avoid future troubles.
First, open the server CMD, and type **ipconfig*, then press enter. Note the IPV4 address (192.168.xx.xx), we'll set it as static.

![](images/server/configuration/Capture23.PNG)

To set a static IP to our server, Right click the Network icon in the tool bar, click **Open Network and Internet Settings** > **Ethernet** tab, **Change adapter options** > Right click the Network adapter you're connected with, then **Properties**. See below screenshots.
![](images/server/configuration/Capture24.PNG)
![](images/server/configuration/Capture25.PNG)
![](images/server/configuration/Capture26.PNG)

Double click "Internet Protocol Version 4 (TCP/IPV4)"
![](images/server/configuration/Capture27.PNG)

Here, select the option "Use the following IP address". In IP address, add the server IP address we've just noted in the previous step in the server CMD. Subnet mask will autofill, and also leave alone default gateway.
Proceed below and select "use the following DNS server addresses". For preferred DNS server, add loop back address that points to its IP address (127.0.0.1), and DNS server for Google (8.8.8.8), then click "OK" to save changes
![](images/server/configuration/Capture28.PNG)

### Step 4: Creating Organizational Units, Users, and Groups
To establish a structured Active Directory environment, the organization is divided into three branches: **Nairobi, Mombasa, and Kisumu**. Each branch is organized into separate **Users, Computers, and Servers OUs** to simplify administration and management.

User accounts are created within their respective branch Users OU, while security groups are created to organize users according to their roles or access requirements. The appropriate users are then assigned to these groups, providing a structured approach to **role-based access control and centralized user management**.
To start with, click on window search tool, search and open "Active directory users and computers".
![](images/server/users%20%26%20groups/Capture0.PNG)
![](images/server/users%20%26%20groups/Capture1.PNG)

To create OUs (Nairobi, Mombasa, Kisumu), right click on the domain name **RoundTech.local** > **New** > **Organizational Unit**
![](images/server/users%20%26%20groups/Capture2.PNG)

Give the OU Name, e.g Nairobi, and click OK.
![](images/server/users%20%26%20groups/Capture3.PNG)
Repeat the process to create Mombasa and Kisumu OUs, within the RoundTech.local domain.

Note that it is possible to create OUs inside another OU. In this regard, lets create **Users, Computers and Servers** OUs inside Nairobi, Mombasa and Kisumu OUs.
![](images/server/users%20%26%20groups/Capture41.PNG)
![](images/server/users%20%26%20groups/Capture42.PNG)
![](images/server/users%20%26%20groups/Capture43.PNG)

At end You should have below structure of folders.
![](images/server/users%20%26%20groups/Capture44.PNG)

We'll go ahead and create groups, but before that lets learn some concepts we'll encounter while creating groups, **Group Scope & Group Type**
- **Group** Scope: Determines where the group can be used and who can be a member.
    1. **Domain Local**: Mainly used to assign permissions to resources such as folders, files, printers, and shares within a domain. It can contain members from other domains.
    2. **Global**: Used to group users with similar roles or responsibilities within the same domain, such as **GG-Finance* or **GG-IT-Admins*.
    3. **Universal**: Used when groups need to contain members from or be used across multiple domains within the same forest.
  
- **Group Type**: Determines what the group is used for.
    1. **Security Group**: Used for access control and permissions, such as granting users access to folders, files, applications, or printers.
    2. **Distribution Group**: Used mainly for email distribution and cannot normally be used to assign Windows security permissions.
With that introduction, lets create 4 groups inside; **HR, Sales, Accounting and ICT**, All are security groups with global scope.
Right click **Users** OU inside Mombasa OU, **New** > **Group**. Group name: **HR**, Group scope: **Global**, and Group type: **Security**
![](images/server/users%20%26%20groups/Capture5.PNG)
Repeat the process to create the remaining 3 groups (ICT, Sales and Accounting), in each OU (Nairobi and Kisumu)

Next, We're going to create users. Users in the AD should have first and last names filled, plus their "User logon name", which is usually combination of first name initial and second name, but that can change according to company policy.
For easier future reference, I have adopted a naming convention, where user's second name is the department he/she belongs, see below.
Right click users (inside Mombasa OU) > **New** > **User**.
Proceed to add first name, last name, and user logon name. Full name will autofill.
Example: First name: peter, Last name: ICT, User logon name: peterict (or whichever name you want), then click Next.
![](images/server/users%20%26%20groups/Capture6.PNG)

Set first time logon password for user, and make sure to check **user must change password at next logon**. Click Next
![](images/server/users%20%26%20groups/Capture7.PNG)

Then Finish
![](images/server/users%20%26%20groups/Capture8.PNG)

Repeat this process, to create at least 2 people for groups (though we've not added them to groups.), e.g Paul ICT, Alex Sales, James HR, etc.
![](images/server/users%20%26%20groups/Capture9.PNG)

Now, With those user accounts added in the domain, They can logon and start operating computers that are joined in the domain. We can test that, but before testing, let ensure we add all our users to their respective groups.
To add **user into a group**, right click the user then **Properties**, a user profile card will pop up, and you can modify information about users.
![](images/server/users%20%26%20groups/Capture10.PNG)
![](images/server/users%20%26%20groups/Capture11.PNG)

Click **Member Of** tab, then **Add** button.
![](images/server/users%20%26%20groups/Capture12.PNG)

Type the group you wish to add user into, and select **Check names**.
For Peter ICT user, I will search 'ict', for James HR > hr ... The group will appear in the box, the select **Add**, and the user will be added into the group. Be sure to repeat the process to add all other users into respective groups.
- **Note:** For ICT users to be able to work with active directory and make changes, such as enabling or disabling other accounts, reset passwords etc, add them to **Domain Admins** group, created by default.
![](images/server/users%20%26%20groups/Capture13.PNG)
![](images/server/users%20%26%20groups/Capture14.PNG)

**And with that, our server side configurations are complete. We're going to create at least 2 client machines to test these functionalities.**


### Step 4: Setting up Windows 10 (Client)
Like we set up Windows Server 2022 previously, click on **Create a New Virtual Machine** on the VMware Workstation Pro 17 Dashboard. Proceed with the wizard: **Typical** > **I will install the operating system later** > Guest operating system: **Microsoft Windows**; Version: **Windows 10 x64** > Virtual machine name: **Windows 10 x64** (Default) > Maximum disk size: **20 GB & "Split virtual disk into multiple files** > Before clicking on **Finish** click on **Customize Hardware**.

You can increase the Memory to "4 GB (4096 MB)" from the Memory tab and also you can increase the number of cores per processor to 2 from the Processors tab. From the CD/DVD (SATA) tab under Connection, click on "Use ISO image file" then Browse. Select the Windows Server 10 (ISO) that was downloaded.
![](images/client/installation/Capture6.PNG)

Once the environment is created, you will see that another tab, "Windows 10 x64", was created next to our server "Windows Server 2022". As before, click on "Power on this Virtual Machine" to begin the Operating System (OS) installation. Quickly press "any key" when prompted to boot from the CD/ISO.
![](images/client/installation/Capture6.1.PNG)
![](images/client/installation/Capture6.2.PNG)

Select "Language, Time and currency format, Keyboard" then click Next. Click on "Install Now". Click on "I don't have a product key"
![](images/client/installation/Capture7.PNG)
![](images/client/installation/Capture8.PNG)

Only the Pro, Education, and Enterprise editions of Windows 10/11 can be joined to a domain. The Active Directory domain is not supported in Home Editions; thus, make sure to select the Pro version. Next.
![](images/client/installation/Capture9.PNG)

Accept the Software License Agreement and click Next. Click on "Custom: Install Windows only (advanced)" as we are installing Windows for the first time. Once the installation finishes, it will ask for our region. Select your region and click next.
![](images/client/installation/Capture19.PNG)

Create password for **Administrator** account
![](images/client/installation/Capture20.PNG)

Complete setting up Security questions
![](images/client/installation/Capture21.PNG)

Continue with limited setup. Finally You will be on your desktop.
![](images/client/installation/Capture25.PNG)


### Step 5: Client Configurations
Now that we have our new client, lets rename this machine for easier identification. By default, Windows assigns randomly generated names (such as DESKTOP-UOJ92P) to newly installed machines, which can make identification and management difficult. For this reason, it is important to rename each computer using a consistent and meaningful naming convention, such as DC01, CLIENT01, etc. For this lab, we will rename this Windows 10 machine to "COMP01".
Right-click on Start > System.
![](images/client/configuration/Capture0.PNG)

The About page will open. Then click on "Rename this PC".
![](images/client/configuration/Capture1.PNG)

Type "COMP01" > Next. The computer should restart itself.
![](images/client/configuration/Capture2.PNG)

To connect "helpdesk" to the DC, we need to know the DC's network details and reconfigure "COMP01" network settings. Remember we noted our domain controller's IP address during previous steps. If you can't remember, go inside our DC01 CMD and type **ipconfig*, or the easiest way is to ping DC01 from client machine CMD, i.e ping **DC01**, and we shall get our server's IP address.
After getting DCs IP address, Lets open **Network & Internet** in client (COMP01) machine, > **Ethernet** > **Change adapter options**
![](images/client/configuration/Capture4.PNG)

Right click the Network Adapter you are connected to, then **Properties**
![](images/client/configuration/Capture5.PNG)

Scroll down to find and double click **Internet Protocol Version 4 (TCP/IPv4)**
![](images/client/configuration/Capture6.PNG)

Here, select **Use the following DNS server addresses**, and add the IP address of our domain controller, **DC01** in the **Preferred DNS server**, and at **Alternate DNS server**, put google DNS server, for internet traffic. (8.8.8.8). Click OK and close the wizards.
![](images/client/configuration/Capture7.PNG)


### Step 6: Connecting Windows 10 to the Domain Controller
To connect "COMP01" to the DC, Navigate to **start menu** > **System** > **Advanced System Settings**
![](images/client/configuration/Capture8.PNG)
![](images/client/configuration/Capture9.PNG)

In the wizard, under **Computer Name**, click **Change button**
![](images/client/configuration/Capture10.PNG)

Select **Domain** instead of work group, and type our domain, which is **RoundTech.local**. Incase you forgot your domain, open active directory users and computers like below, and take note of domain name.
![](images/client/configuration/Capture11.PNG)
![](images/client/configuration/Capture12.PNG)
![](images/client/configuration/Capture13.PNG)



















