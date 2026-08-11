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
