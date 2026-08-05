# 🖥️ IT Active Directory Home Lab

**Windows Server 2022 • Active Directory • DNS • Group Policy • Oracle VirtualBox**

Enterprise Windows Administration Lab

---

## Project Overview

This repository documents my hands-on Active Directory home lab built to gain practical experience with enterprise Windows administration. The lab simulates a small business network using Windows Server 2022, Active Directory Domain Services (AD DS), DNS, Oracle VirtualBox, and Windows 11.

The goal of this project was to strengthen my understanding of Windows Server administration, networking, virtualization, and Active Directory while building practical skills commonly used in enterprise IT environments.

---

# Table of Contents

- [Project Overview](#project-overview)
- [Network Diagram](#network-diagram)
- [Objectives](#objectives)
- [Technologies Used](#technologies-used)
- [Lab Architecture](#lab-architecture)
- [Lab Setup](#lab-setup)
- [Install Active Directory Domain Services](#install-active-directory-domain-services)
- [Create the Active Directory Forest](#create-the-active-directory-forest)
- [Configure DNS Forwarding](#configure-dns-forwarding)
- [Configure Organizational Units](#configure-organizational-units)
- [Create Users and Security Groups](#create-users-and-security-groups)
- [Assign Users to Security Groups](#assign-users-to-security-groups)
- [Configure Group Policy](#configure-group-policy)
- [Verify Active Directory with PowerShell](#verify-active-directory-with-powershell)
- [Skills Demonstrated](#skills-demonstrated)
- [What I Learned](#what-i-learned)

---

# Network Diagram

```text
                           Internet
                               │
                     Home Router / Gateway
                     192.168.1.1 (DHCP)
                               │
                 ─────────────────────────
                 │                      │
      Windows 11 Host PC         Windows Server 2022
      Oracle VirtualBox          DC01.lab.local
                                      │
                 ┌─────────────────────────────────┐
                 │ Active Directory Domain Services│
                 │ DNS Server                      │
                 │ Organizational Units           │
                 │ Users & Groups                 │
                 │ Group Policy                   │
                 └─────────────────────────────────┘
```

---

# Objectives

- Gain hands-on experience with Windows Server administration
- Install and configure Active Directory Domain Services (AD DS)
- Configure DNS for a Domain Controller
- Learn enterprise networking fundamentals
- Practice virtualization using Oracle VirtualBox
- Organize users and groups using Active Directory
- Configure Group Policy
- Build an IT portfolio demonstrating real-world administrative tasks

---

# Technologies Used

## Operating Systems
- Windows Server 2022 Evaluation
- Windows 11
- Ubuntu Linux *(Future Labs)*

## Virtualization
- Oracle VirtualBox

## Windows Server Roles
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy
- DHCP *(Future Lab)*

## Networking
- IPv4
- TCP/IP
- DNS
- Remote Desktop
- Windows Networking

## Administration Tools
- Server Manager
- Active Directory Users and Computers (ADUC)
- PowerShell
- Command Prompt
- Git
- GitHub

---

# Lab Architecture

## Home Router
- IP Address: `192.168.1.1`
- DHCP Server
- Internet Gateway
- DNS Forwarder

## Domain Controller (DC01)
- Windows Server 2022
- Static IPv4 Address
- Active Directory Domain Services
- DNS Server
- Domain: `lab.local`

## Host Machine
- Windows 11
- Oracle VirtualBox
- Bridged Network Adapter

---

# Lab Setup

> **Continue here with the step-by-step screenshots from your existing README.**  
> Keep all of your screenshots and replace each section with the expanded commentary we previously created.

Suggested sections:

- Install Oracle VirtualBox
- Download Windows Server 2022
- Create the Virtual Machine
- Configure Networking
- Install Windows Server 2022
- Rename the Server
- Verify the IP Address
- Check IP Availability
- Configure a Static IPv4 Address

---

# Install Active Directory Domain Services

Explain installing the AD DS role through Server Manager and the services it provides.

---

# Create the Active Directory Forest

Include:

- Promote the Server
- Create the `lab.local` forest
- Configure the DSRM password
- Verify `LAB\Administrator` after reboot

---

# Configure DNS Forwarding

Explain configuring the router as a DNS forwarder so internal DNS can resolve external internet addresses.

---

# Configure Organizational Units

Explain why OUs are used to organize users and apply Group Policy.

---

# Create Users and Security Groups

Describe creating users and security groups and introduce IAM and RBAC concepts.

---

# Assign Users to Security Groups

Explain assigning permissions through groups instead of directly to users.

---

# Configure Group Policy

Describe opening the Default Domain Policy and its role in centralized administration.

---

# Verify Active Directory with PowerShell

Document verification commands such as:

- `Get-ADUser`
- `Get-ADGroup`
- `nslookup google.com`

Explain what each validates.

---

# Skills Demonstrated

- Windows Server 2022 Administration
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- DNS Configuration
- DNS Forwarders
- Organizational Unit (OU) Management
- User and Group Administration
- Identity and Access Management (IAM)
- Role-Based Access Control (RBAC)
- Group Policy Management
- PowerShell Administration
- Windows Networking
- Virtualization (Oracle VirtualBox)
- System Administration
- Troubleshooting

---

# What I Learned

This lab provided hands-on experience deploying an enterprise-style Active Directory environment from the ground up. Throughout the project I configured Windows Server, networking, DNS, Active Directory, Organizational Units, users, security groups, and Group Policy while validating the environment using PowerShell.

The project strengthened my understanding of Windows Server administration and reinforced best practices for identity management, DNS, and enterprise network administration.
