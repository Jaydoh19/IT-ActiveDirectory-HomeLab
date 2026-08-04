# IT-ActiveDirectory-HomeLab
This repository documents my hands-on IT home lab environment as I prepare for a career in Information Technology. The goal of this lab is to develop practical experience with Windows Server administration, Active Directory, networking, system administration, virtualization, and troubleshooting by simulating a small business IT environment.

Each lab includes documentation, screenshots, configurations, challenges encountered, and lessons learned.

**Objectives**
- Gain hands-on experience with enterprise IT technologies
- Practice Windows Server administration
- Learn Active Directory management
- Configure networking services
- Strengthen troubleshooting skills
- Build an IT portfolio for employers

**Technologies & Tools**

**Operating Systems**
- Windows Server 2022 Evaluation
- Windows 11
- Ubuntu Linux (future labs)

**Virtualization**
- Oracle VirtualBox

**Windows Services**
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy
- DHCP (future)

**Networking**
- TCP/IP
- IPv4
- DNS
- Remote Desktop
- Windows Networking

**Tools**
- PowerShell
- Command Prompt
- Server Manager
- Active Directory Users and Computers
- Git
- GitHub
______________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Install VirtualBox for VMs**
<img width="1866" height="879" alt="image" src="https://github.com/user-attachments/assets/79ff04e6-d0f5-401e-abec-b748e552da43" />
**Download Windows 2022 Sever ISO**
<img width="1773" height="624" alt="image" src="https://github.com/user-attachments/assets/20aa6799-f5d2-4c4c-b2cb-1d3f21cf64d0" />
These are the key softwares needed for this home lab that I installed. 
______________________________________________________________________________________________________________________________________________________________________________________________________________________________

**Network Architecture**

**Wi-Fi Router (Gateway)**
- IP: my gateway (e.g 192.168.1.1)
- Provides DHCP to all devices
- Handles external DNS forwarding
- My home internet gateway

**DC01 - Domain Controller (VM)**
-    Static IP: e.g 192.167.1.59
-    Runs AD DS + DNS Server roles
-    Domain: lab.local
-    DNS points to itself

**Host Laptop (My Machine)**
-    Runs VirtualBox
-    Connected to same Wi-Fi
-    Gets DHCP address from router
-    Bridged networking shares the LAN
______________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Create the VM**
<img width="956" height="742" alt="image" src="https://github.com/user-attachments/assets/0816c171-24c4-4296-820b-836a87f0ced9" />
I created the Domain Controller VM with Windows Sever 2022 ISO 
**Configured Network Adapter**
<img width="772" height="500" alt="image" src="https://github.com/user-attachments/assets/f1e74d46-543f-47f9-8542-7883ae1ba5f2" />
Changed the Network from NAT to Bridged Adapter so that it gets Real IP on my home network instead of a private network where nothing can reach it.
