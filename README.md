# 🖥️ Active Directory Home Lab Setup Guide

## 1. Project Overview
> This repository contains the scripts and configurations to deploy a fully functional Active Directory domain (labdomain.com) with users, Organizational Units, and Group Policies on Windows Server 2022.
> This is a simple lab to get you started with the basics you need to begin your own Active Directory Lab.

## 2. Prerequisites (What you need BEFORE you start)
- **Hardware:** PC with at least 16GB RAM and 50GB free SSD space.
- **Hypervisor:** [VMware Workstation 17 (or VirtualBox 7.0).](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion#product-overview)
- **ISOs:** [Windows Server 2022 Evaluation ISO.](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
- **Tools:** [Windows 11 ISO (for the client machine).](https://www.microsoft.com/en-us/software-download/windows11)
- **Skills:** Basic understanding of networking and PowerShell.

## 3. Virtual Machine Specifications
| Machine | OS | vCPU | RAM | HDD | Network |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DC-01** | Windows Server 2022 | 2 | 4 GB | 60 GB | NAT (10.10.10.1/24) |
| **CLIENT-01** | Windows 11 Pro | 2 | 4 GB | 60 GB | NAT (10.10.10.0/24) |

## 4. Step-by-Step Deployment Instructions
## Step 1: Download and install your virtual Environment
- Download your virtual environment it can be whatever you want. For this lab I will be using VMware.
- Using the link provided above you should be greeted with this page
- click "Download Now"
<img width="2560" height="1438" alt="My Downloads - Support Portal - Broadcom support portal - Brave 9_6_2026 7_29_12" src="https://github.com/user-attachments/assets/685f1c72-3053-4663-9e2e-022912deb333" />

- Login to continue

<img width="2560" height="1438" alt="ActiveDirectoryLab_README md at main · BEdwardsIT_ActiveDirectoryLab - Brave 9_6_2026 7_34_03" src="https://github.com/user-attachments/assets/6f73c131-1e7c-4561-a2ef-791149f7e57f" />

- Click "HERE" to view the free software 

<img width="2560" height="1438" alt="Windows Server 2022 _ Microsoft Evaluation Center - Brave 9_6_2026 7_03_18" src="https://github.com/user-attachments/assets/9e5ab268-274f-447d-bfb4-c8bd8f3ebb5c" />

- Select VMware Workstation Pro

<img width="2560" height="1438" alt="My Downloads - Support Portal - Broadcom support portal - Brave 9_6_2026 7_03_32" src="https://github.com/user-attachments/assets/bb85ca1f-41e6-46bb-b066-ecbf8fbcb62c" />

- Choose the latest version

<img width="2560" height="1438" alt="My Downloads - Support Portal - Broadcom support portal - Brave 9_6_2026 7_03_47" src="https://github.com/user-attachments/assets/9446a601-89f6-4da7-884f-ca9ac48d64ea" />

<img width="2560" height="1438" alt="My Downloads - Support Portal - Broadcom support portal - Brave 9_6_2026 7_04_16" src="https://github.com/user-attachments/assets/5878b05c-e210-4369-9701-7ff361c888fd" />

<img width="2560" height="1438" alt="My Downloads - Support Portal - Broadcom support portal - Brave 9_6_2026 7_04_38" src="https://github.com/user-attachments/assets/a30d1124-3a69-48cf-9291-b46c9c12025f" />

> After the download run the setup to begin the installation

## Step 2: Download Windows 2022 Sever ISO
- Download the ISO  
<img width="2560" height="1438" alt="Windows Server 2022 _ Microsoft Evaluation Center - Brave 9_6_2026 6_57_36" src="https://github.com/user-attachments/assets/fd770523-62c1-45b3-925b-d67f8bec953d" />

## Step 3: Download Windows 11 ISO (Client)
- Go to "Select Download"
<img width="2560" height="1438" alt="Screenshot 9_6_2026 7_51_34" src="https://github.com/user-attachments/assets/064184b8-499b-48bc-8a3b-69be729d33dd" />

- Choose the Available ISO Image
<img width="2560" height="1438" alt="Download Windows 11 - Brave 9_6_2026 7_56_27" src="https://github.com/user-attachments/assets/c46e2408-d1a6-4e39-bbed-70b2bde5c0f1" />

- Click "Confirm"
<img width="2560" height="1438" alt="Download Windows 11 - Brave 9_6_2026 7_56_27" src="https://github.com/user-attachments/assets/13db7109-2721-4d07-af2f-edf3a19f3b34" />

- Select the product Language and click "Confirm"
<img width="2560" height="1438" alt="Captures - File Explorer 9_6_2026 7_59_13" src="https://github.com/user-attachments/assets/b9455d93-5290-4efd-995f-0da0761e857a" />

Great Now you have everything you need to get started!

## Step 4: 
