# 🖥️ Active Directory Home Lab Setup Guide

## 1. Project Overview
> This repository contains the scripts and configurations to deploy a fully functional Active Directory domain (labdomain.com) with users, Organizational Units, and Group Policies on Windows Server 2022.

## 2. Prerequisites (What you need BEFORE you start)
- **Hardware:** PC with at least 16GB RAM and 50GB free SSD space.
- **Hypervisor:** [VMware Workstation 17 (or VirtualBox 7.0).](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion#product-overview)
- **ISOs:** [Windows Server 2022 Evaluation ISO.](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
- **Tools:** [Windows 11 ISO (for the client machine).](https://www.microsoft.com/en-us/software-download/windows11)
- **Skills:** Basic understanding of networking and PowerShell.

## 3. Virtual Machine Specifications
| Machine | OS | vCPU | RAM | HDD | Network |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DC-01** | Windows Server 2022 | 2 | 4 GB | 60 GB | NAT (192.168.10.0/24) |
| **CLIENT-01** | Windows 11 Pro | 2 | 4 GB | 60 GB | NAT (192.168.10.0/24) |

## 4. Step-by-Step Deployment Instructions
