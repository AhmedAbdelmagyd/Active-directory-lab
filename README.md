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
| **DC-01** | Windows Server 2022 | 2 | 4 GB | 64 GB | NAT (10.10.10.1/24) |
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

## Step 4: Create Domain Controller and Install Server 2022

Open up VMware Workstation
To create a New Virtual machine go to file and select "New Virtual Machine" or you can use Ctrl + N
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 8_15_59" src="https://github.com/user-attachments/assets/d47655e7-5d81-4fef-9270-cf83d4bc9506" />

The Wizard will open. Typical is enough for what we are doing. Click "Browse" and locate the Server ISO you downloaded earlier. You can leave the product key empty and it will work just fine.

<img width="426" height="398" alt="Captures - File Explorer 9_6_2026 8_13_06" src="https://github.com/user-attachments/assets/7d909713-dfee-4705-b100-c1fd044bacd1" />

<img width="426" height="398" alt="Captures - File Explorer 9_6_2026 8_13_20" src="https://github.com/user-attachments/assets/308028a3-1f2a-42f5-b872-30a649373eb7" />

<img width="426" height="398" alt="Windows Server 2022 - VMware Workstation 9_6_2026 8_48_41" src="https://github.com/user-attachments/assets/3b700ae8-f40a-4317-9572-eef54cb2cafb" />

Name the machine and allocate enough disk size. (you can always allocate more in the future). RAM and CPU will be automatically set to 4GB and 2 cores. (you can also change these to fit your workload) 

<img width="426" height="398" alt="Screenshot 9_6_2026 8_26_50" src="https://github.com/user-attachments/assets/b95abac6-8498-4149-8f5e-10258033adeb" />
<img width="426" height="398" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 8_52_18" src="https://github.com/user-attachments/assets/270b6b64-41af-4e10-8055-5194046888f0" />
<img width="426" height="398" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 8_53_20" src="https://github.com/user-attachments/assets/d87d52ca-d883-4a4f-8960-92705115da58" />

- An issue you will likely face when booting up the machine is this error!
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 8_54_57" src="https://github.com/user-attachments/assets/569d5358-83cb-4b6b-8b87-7a0faa19f8a9" />


- The unusual fix to this is closing the machine and going to the machine's setting. At hardware go to floppy and disable connect at power on.

<img width="755" height="702" alt="Captures - File Explorer 9_6_2026 8_56_50" src="https://github.com/user-attachments/assets/802f56e5-d077-4b0f-8b20-d3d7c31379ad" />
<img width="755" height="702" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 8_57_37" src="https://github.com/user-attachments/assets/3b1821a8-73f6-4439-bf6c-8265ba465ed1" />

- Now that the machine is working properly we will go through the setup.

<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 8_59_52" src="https://github.com/user-attachments/assets/47d13dfc-5c45-45fe-99da-3a3ac218766a" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_00_01" src="https://github.com/user-attachments/assets/ed3d7140-8a32-43e8-b66c-72a506eb28ec" />

- Choose the system you want but make sure you select desktop experience otherwise you will be doing everything in CMD!
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 9_00_57" src="https://github.com/user-attachments/assets/ff09d4ac-3490-4aa7-b5ce-877e8621586e" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_01_09" src="https://github.com/user-attachments/assets/35ffb4fd-a6b2-47ca-a4fe-c1eac225783b" />

Click Custom and select the available drive 

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_01_19" src="https://github.com/user-attachments/assets/ef72bdd6-0c2d-4cc9-83b5-4006fffebd42" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_01_24" src="https://github.com/user-attachments/assets/4e9b91fe-25c4-4e1a-bf59-8256aa1fe0ad" />
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_01_35" src="https://github.com/user-attachments/assets/420fcbae-96ff-40d8-82fb-f27730cb4499" />

- Now that the system is installed create a password. Anything will be okay since this is a home lab and in a safe enviornment

<img width="1226" height="857" alt="Screenshot 9_6_2026 9_04_10" src="https://github.com/user-attachments/assets/44ba32ee-34e8-4a08-8309-b8b06ef1147e" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_04_28" src="https://github.com/user-attachments/assets/61db2642-1cd2-47d2-8373-142dc5b825f4" />



