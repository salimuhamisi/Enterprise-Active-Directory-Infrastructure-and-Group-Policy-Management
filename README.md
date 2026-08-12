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

Next, select "Windows server" as guest operating system, and Window server 2022 version. Select Next
![](images/server/Installation/Capture4.PNG)

Then give your virtual machine a name, or leave the default "Windows server 2022". You van also browse a different location for the machine installation if you wish, then click Next.
![](images/server/Installation/Capture5.PNG)

Next, specify disk capacity. the recommended disk size is 60.0GB, but in this lab I will go with minimum, 20GB, because we're not going to install many applications. Select "split virtual disk into into multiple disk" and click Next
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
![](images/server/Installation/Capture19.PNG)
![](images/server/Installation/Capture20.PNG)
