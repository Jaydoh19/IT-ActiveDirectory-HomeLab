# IT Active Directory Home Lab

This repository documents my hands-on Active Directory home lab built to gain practical experience with enterprise Windows administration. The lab simulates a small business network using Windows Server 2022, Active Directory, DNS, VirtualBox, and Windows 11.

The objective is to strengthen my skills in system administration, networking, troubleshooting, virtualization, and Active Directory while building a portfolio that demonstrates real-world IT experience.

---

# Objectives

- Gain hands-on experience with Windows Server administration
- Install and configure Active Directory Domain Services (AD DS)
- Configure DNS for a domain controller
- Practice networking fundamentals
- Learn virtualization using Oracle VirtualBox
- Build an IT portfolio for employers

---

# Technologies Used

## Operating Systems

- Windows Server 2022 Evaluation
- Windows 11
- Ubuntu Linux *(future labs)*

## Virtualization

- Oracle VirtualBox

## Windows Server Roles

- Active Directory Domain Services (AD DS)
- DNS
- Group Policy
- DHCP *(future lab)*

## Networking

- IPv4
- TCP/IP
- DNS
- Remote Desktop
- Windows Networking

## Tools

- Server Manager
- PowerShell
- Command Prompt
- Active Directory Users and Computers
- Git
- GitHub

---

# Lab Architecture

## Home Router

- IP Address: `192.168.1.1`
- Provides DHCP
- Internet Gateway
- DNS Forwarder

## Domain Controller (DC01)

- Windows Server 2022
- Static IP
- Active Directory Domain Services
- DNS Server
- Domain: `lab.local`

## Host Computer

- Windows 11
- Oracle VirtualBox
- Connected using a Bridged Adapter

---

# Lab Setup

## Install Oracle VirtualBox

<img width="1866" height="879" alt="image" src="https://github.com/user-attachments/assets/79ff04e6-d0f5-401e-abec-b748e552da43" />

Installed Oracle VirtualBox to host the Windows Server virtual machine.

---

## Download Windows Server 2022

<img width="1773" height="624" alt="image" src="https://github.com/user-attachments/assets/20aa6799-f5d2-4c4c-b2cb-1d3f21cf64d0" />

Downloaded the Windows Server 2022 Evaluation ISO from Microsoft.

---

## Create the Virtual Machine

<img width="956" height="742" alt="image" src="https://github.com/user-attachments/assets/0816c171-24c4-4296-820b-836a87f0ced9" />

Created a Windows Server 2022 virtual machine with:

- 50 GB Virtual Disk
- 4 GB RAM
- Windows Server 2022 ISO

---

## Configure Networking

<img width="772" height="500" alt="image" src="https://github.com/user-attachments/assets/f1e74d46-543f-47f9-8542-7883ae1ba5f2" />

Changed the network adapter from **NAT** to **Bridged Adapter** so the virtual machine receives an IP address on my home network.

---

## Install Windows Server 2022

<img width="1024" height="768" alt="VirtualBox_DC-01_04_08_2026_13_40_16 install" src="https://github.com/user-attachments/assets/f531a964-296e-4951-b483-161ac41fbd05" />

Installed Windows Server 2022 Standard Evaluation (Desktop Experience) on the virtual machine.

Configured:

- Administrator password
- 50 GB virtual disk

<img width="1016" height="843" alt="image" src="https://github.com/user-attachments/assets/635f0c03-8118-46f2-9c94-345b6856bbd4" />

---

## Rename the Server

<img width="1018" height="765" alt="image" src="https://github.com/user-attachments/assets/44a6e906-00c5-4e25-905c-ffae6979b438" />

Renamed the server to **DC01** (Domain Controller 1) to follow standard enterprise naming conventions.

---

# Configure Networking

## Verify the IP Address

<img width="1022" height="769" alt="image" src="https://github.com/user-attachments/assets/3fbea965-0504-4392-bc70-10ac1e49de1d" />

Verified that the server obtained an IP address on the same subnet as my home network (`192.168.1.x`).

---

## Check IP Availability

<img width="746" height="205" alt="image" src="https://github.com/user-attachments/assets/ef5c71e9-64ec-4bd3-adef-a81287b50708" />

Checked that my desired static IP address was not currently being used before assigning it to the server.

---

## Configure Static IPv4 Address

Active Directory requires reliable DNS. The domain controller should use itself as its preferred DNS server.

| Setting | Value |
|----------|-------|
| IPv4 Address | `192.168.1.50` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |
| Preferred DNS | `192.168.1.50` |

<img width="1010" height="754" alt="image" src="https://github.com/user-attachments/assets/4c0a9c39-8970-4e1b-8ead-e0a5d527589a" />

---

# Install Active Directory Domain Services

<img width="782" height="556" alt="image" src="https://github.com/user-attachments/assets/59fdf734-41d9-47a4-9e52-e27c1e5889b4" />

<img width="1019" height="729" alt="image" src="https://github.com/user-attachments/assets/93fa7ca0-6ed8-4d12-a515-29a031bf08b3" />

Installed the **Active Directory Domain Services (AD DS)** role using Server Manager.

This role provides:

- Centralized authentication
- User account management
- Security groups
- Organizational Units (OUs)
- Group Policy support
- Domain administration

---

# Create the Active Directory Forest

## Promote the Server

<img width="1027" height="758" alt="image" src="https://github.com/user-attachments/assets/95e8a2d4-a8c7-4e2d-abb2-8ef8d2c11cb7" />

Promoted DC01 to a Domain Controller.

---

## Create the Forest

<img width="1021" height="760" alt="image" src="https://github.com/user-attachments/assets/9bf64cd6-7a8d-4f6a-a95d-0b41352ba128" />

Created a new Active Directory forest named:

```
lab.local
```

Configured a Directory Services Restore Mode (DSRM) password.

---

## Verify the Domain

<img width="1023" height="762" alt="image" src="https://github.com/user-attachments/assets/f4f9ea9d-2a6d-4235-a455-be6c7b1fa4b7" />

After restarting, the login screen displayed:

```
LAB\Administrator
```

This confirms that the Active Directory forest was successfully created and that the server is functioning as the first Domain Controller for the `lab.local` domain.

---
