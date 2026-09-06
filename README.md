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
| **DC-01** | Windows Server 2022 | 2 | 4 GB | 64 GB | NAT (10.10.10.2/24) |
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

- Open up VMware Workstation
- I will be using this simple network structure to demonstrate how the Active Domain and Client will communicate
<img width="1101" height="579" alt="image" src="https://github.com/user-attachments/assets/a1ad7f00-d592-480d-a707-a8cd35431684" />

- To create the virtual network. Go to Edit and open Virtual Network Editor

<img width="1226" height="857" alt="ActiveDirectoryLab_README md at main · BEdwardsIT_ActiveDirectoryLab - Brave 9_6_2026 9_34_43" src="https://github.com/user-attachments/assets/cd2a6a4c-fd6b-40c5-a4a6-50a5047b5557" />

- Click "Add Network". Select any Network to add this is just the name
<img width="601" height="525" alt="Captures - File Explorer 9_6_2026 9_42_13" src="https://github.com/user-attachments/assets/71f452e1-a875-4fbe-9c11-5cc1667edebf" />
<img width="601" height="554" alt="image" src="https://github.com/user-attachments/assets/85292da7-bcec-4836-92d1-e883acc4291d" />

- After creating the network click "Change Settings" to start editing the network
<img width="601" height="525" alt="Screenshot 9_6_2026 9_45_49" src="https://github.com/user-attachments/assets/11eafb34-7205-4c7a-9a8a-eee194b49315" />

- Select Host-only because we want the network to be between the virtual machines only which means none will have internet
- Disable Connect a host to isolate the network
- Disable DHCP we will be creating our own
- IP: 10.10.10.0, Subnet: 255.255.255.0
<img width="601" height="497" alt="Photos 9_6_2026 9_54_52" src="https://github.com/user-attachments/assets/4c7b3808-9e0e-453e-bd97-d176574ba90b" />

- Great now we have a complete isolated network for our virtual machines to communicate through!
  
- To create a New Virtual machine go to file and select "New Virtual Machine" or you can use Ctrl + N
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 8_15_59" src="https://github.com/user-attachments/assets/d47655e7-5d81-4fef-9270-cf83d4bc9506" />

- The Wizard will open. Typical is enough for what we are doing. Click "Browse" and locate the Server ISO you downloaded earlier. You can leave the product key empty and it will work just fine.

<img width="426" height="398" alt="Captures - File Explorer 9_6_2026 8_13_06" src="https://github.com/user-attachments/assets/7d909713-dfee-4705-b100-c1fd044bacd1" />

<img width="426" height="398" alt="Captures - File Explorer 9_6_2026 8_13_20" src="https://github.com/user-attachments/assets/308028a3-1f2a-42f5-b872-30a649373eb7" />

<img width="426" height="398" alt="Windows Server 2022 - VMware Workstation 9_6_2026 8_48_41" src="https://github.com/user-attachments/assets/3b700ae8-f40a-4317-9572-eef54cb2cafb" />

- Name the machine and allocate enough disk size. (you can always allocate more in the future). RAM and CPU will be automatically set to 4GB and 2 cores. (you can also change these to fit your workload) 

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

- Windows Server requires you to press Ctrl + Alt + Delete which you can send by pressing the button in the picture. (This is only needed in a virtual environment because Ctrl + Alt is used to exit the machine)

<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_11_21" src="https://github.com/user-attachments/assets/fdd10cdd-7e12-49ef-97b3-4ca731854c5d" />
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_14_28" src="https://github.com/user-attachments/assets/57cba3e0-46dc-45ff-bb04-d01901ccbb05" />


- Once you login windows server will start on its own.
<img width="1343" height="882" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_16_47" src="https://github.com/user-attachments/assets/f8d3fec5-628a-4695-b78d-ae8edd814be3" />

- Great now we need to make sure the virtual machine is connected to the right network (you can do it without powering off the machine)
- Outside the machine enter the settings and go to network adapter
<img width="755" height="702" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_32_17" src="https://github.com/user-attachments/assets/9a48fd15-7303-42b9-ad1c-19e9ec338a0a" />

- Select Custom and Choose the network you created
<img width="755" height="702" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_35_40" src="https://github.com/user-attachments/assets/168174a9-099b-4a20-abac-e343ad126f95" />

- Go back inside the machine and click "Network and Internet settings"

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_20_51" src="https://github.com/user-attachments/assets/3bbaf2bb-45fa-4c83-a83e-4bf6e5986a5d" />

- Select "Change Adapter Options"
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_20_58" src="https://github.com/user-attachments/assets/768abbfa-a8b1-4bb2-a52a-b235d9b46bd0" />

- Open Ethernet0
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_21_08" src="https://github.com/user-attachments/assets/47fff10e-d731-4259-a87c-77f6d9e2e155" />

- Open the Internet Protocol by double-clicking

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_21_14" src="https://github.com/user-attachments/assets/1d154208-6eb6-43ab-92a6-e86e02afe310" />

- Enter the IP, subnet mask, DNS as per the diagram
<img width="1101" height="579" alt="646878496-a1ad7f00-d592-480d-a707-a8cd35431684" src="https://github.com/user-attachments/assets/002a42b4-45f2-45f3-8d15-65f4580595ec" />

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_22_15" src="https://github.com/user-attachments/assets/64b5fb66-8d3b-446d-80d3-3b514bf2e684" />

- Click Ok and open up cmd (Command Prompt)
<img width="1226" height="857" alt="Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_47_54" src="https://github.com/user-attachments/assets/ccc081c4-9873-4b7f-a7dd-346d044399d1" />

- Type in the command ipconfig
- confirm the ip and subnet you set is there

<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 10_46_17" src="https://github.com/user-attachments/assets/cab6f057-72c5-482e-86f2-dc0f61cf41a3" />


- Great this Done!

- Right now we will go the setting to change the name of the device

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_24_06" src="https://github.com/user-attachments/assets/239441bd-56dc-465d-a1e4-dada441c0956" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_24_21" src="https://github.com/user-attachments/assets/29983c34-cf57-4e31-b3eb-b4fbbe034f2f" />
<img width="1343" height="882" alt="ActiveDirectoryLab_README md at main · BEdwardsIT_ActiveDirectoryLab - Brave 9_6_2026 9_22_34" src="https://github.com/user-attachments/assets/fe3df9db-cee5-4aa3-b1ec-62183c08cf4f" />
<img width="1343" height="882" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_22_51" src="https://github.com/user-attachments/assets/caf3ebf9-ea3c-4a23-bff7-eb15f4535d22" />
<img width="1343" height="882" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_23_00" src="https://github.com/user-attachments/assets/04a514ec-a716-4534-b4f6-ba5cd2399bbd" />

- After the restart we can finally go to windows server
- Go to Manage and from there select Add Role and Features

<img width="1343" height="882" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_17_46" src="https://github.com/user-attachments/assets/510c68fa-4087-4841-95f5-4a067ee98540" />
<img width="1343" height="882" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_18_19" src="https://github.com/user-attachments/assets/0d4a2478-0f52-4a2a-9b3f-fb4fa1e03553" />

- From here we will create the server and domain controller

<img width="1343" height="882" alt="Captures - File Explorer 9_6_2026 9_19_53" src="https://github.com/user-attachments/assets/8c0c8699-a89a-4dfa-af71-70ed1a8dcccc" />

<img width="1343" height="882" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_21_02" src="https://github.com/user-attachments/assets/56612209-b393-492f-add1-dd1ff4170a8a" />

- Select the server that we can identify by the name we gave it

<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 9_29_55" src="https://github.com/user-attachments/assets/e00356aa-24b7-47bc-8794-3db622185715" />

- Check the Active Directory Domain Services
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 9_31_45" src="https://github.com/user-attachments/assets/3d803210-3531-43dc-acca-ae44ac6db55c" />

- Once you do this pop up will appear click "Add Features"
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_05_34" src="https://github.com/user-attachments/assets/c905bc64-235d-4c35-8a78-7f2d579010c2" />

- Click "Next"
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_07_03" src="https://github.com/user-attachments/assets/d0a4454e-8bc4-4651-a2fc-913d2ec24850" />
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 10_07_45" src="https://github.com/user-attachments/assets/8c446925-8d0c-4a24-bff0-88f4d219edf8" />

- Click "Install"
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_08_18" src="https://github.com/user-attachments/assets/9b799cf2-ff5a-4c9c-9af2-bedffaca2ac1" />
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_08_56" src="https://github.com/user-attachments/assets/5bbad129-fa35-41c1-90fc-2f36c5aec584" />

- After the installation a flag will be triggered.
- Click on it
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_09_12" src="https://github.com/user-attachments/assets/4e07d2db-59b6-4243-8048-d4aaa5f18a2c" />

- Click "Promote this server to a domain controller"
<img width="1226" height="857" alt="Captures - File Explorer 9_6_2026 10_11_03" src="https://github.com/user-attachments/assets/84877aca-d39f-4891-b3f3-5a0211ef8842" />

- In this page this where you create domain and give a name
- Go to add a new forest
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_13_04" src="https://github.com/user-attachments/assets/3c7948ec-2b37-48e5-a3f5-901f94ee6de5" />

- In the "root domain name" type in the domain name
<img width="1101" height="579" alt="646878496-a1ad7f00-d592-480d-a707-a8cd35431684 (1)" src="https://github.com/user-attachments/assets/09115b3f-efe0-4b47-bb6e-a3ccd0848aff" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_13_29" src="https://github.com/user-attachments/assets/d2dfc7b7-0cc2-4112-b438-d3b2c39f8653" />

- Create a password 
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_17_07" src="https://github.com/user-attachments/assets/250f97f4-4cdd-4a93-9195-350cd11678f2" />
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_18_09" src="https://github.com/user-attachments/assets/b793a29e-8b9b-4452-966e-e030e7d2bdca" />

- Click "Next"

<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_18_32" src="https://github.com/user-attachments/assets/6aa2547f-2f0b-4670-88db-ac9f5e920280" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_18_44" src="https://github.com/user-attachments/assets/2d4e3184-3ed3-4b3f-a041-b2ced9082499" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_18_48" src="https://github.com/user-attachments/assets/d1c48790-84e0-4a2c-8027-d168d2661403" />
<img width="1226" height="857" alt="Windows Server 2022 - VMware Workstation 9_6_2026 10_18_53" src="https://github.com/user-attachments/assets/450f9875-138c-4de8-9092-541eb66fe3c9" />

- Wait for the Perquisite check to complete.
- If you face any issues relating to the TCP/IP it means you probably skipped a step or 2
- Click Install. The installation is a long process and will take time
<img width="1226" height="857" alt="Editing Active-directory-lab_README md at main · AhmedAbdelmagyd_Active-directory-lab - Brave 9_6_2026 10_50_11" src="https://github.com/user-attachments/assets/c23e372b-3777-4193-9402-32b38db00ca6" />


