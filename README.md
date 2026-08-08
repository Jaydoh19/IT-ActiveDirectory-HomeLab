# 🖥️ IT Active Directory Home Lab

**Windows Server 2022 • Active Directory • DNS • Group Policy • Oracle VirtualBox**


---

```text
                         Internet
                             │
                             │
                      Home Router
                      
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
      Windows 11 Host              Windows Server 2022
      Oracle VirtualBox              DC01.lab.local
                                            │
                                            ▼
                                  Active Directory (AD DS)
                                            │
                                            ▼
                                          DNS
                                            │
                                            ▼
                                     Group Policy
                                            │
                                            ▼
                                     Users & Groups
```

## Overview

This repository documents my hands-on Active Directory home lab built to gain practical experience with enterprise Windows administration. The lab simulates a small business network using Windows Server 2022, Active Directory Domain Services (AD DS), DNS, Oracle VirtualBox, and Windows 11.

The goal of this project was to strengthen my understanding of Windows Server administration, networking, virtualization, and Active Directory while building practical skills commonly used in enterprise IT environments.

---

## Part 1 - Active Directory Deployment

- [Overview](#overview)
- [Objectives](#objectives)
- [Technologies Used](#technologies-used)
- [Lab Architecture](#lab-architecture)
- [Lab Setup](#lab-setup)
- [Configure Static Networking](#configure-static-networking)
- [Install Active Directory Domain Services](#install-active-directory-domain-services)
- [Create the Active Directory Forest](#create-the-active-directory-forest)
- [Configure DNS Forwarding](#configure-dns-forwarding)
- [Configure Organizational Units](#configure-organizational-units-ous)
- [Create Users and Security Groups](#create-users-and-security-groups)
- [Assign Users to Security Groups](#assign-users-to-security-groups)
- [Configure Group Policy](#configure-group-policy)
- [Verify Active Directory with PowerShell](#verify-active-directory-with-powershell)

## Part 2 - Windows Client Domain Integration

- [Part 2 Overview](#part-2-overview)
- [Create the Windows 11 Client VM](#create-the-windows-11-client-vm)
- [Configure Client Networking](#configure-client-networking)
- [Configure Client DNS](#configure-client-dns)
- [Test Connectivity to the Domain Controller](#test-connectivity-to-the-domain-controller)
- [Join the Client to the Domain](#join-the-client-to-the-domain)
- [Verify the Client in Active Directory](#verify-the-client-in-active-directory)
- [Log In with a Domain User](#log-in-with-a-domain-user)
- [Verify Group Policy](#verify-group-policy)
- [Part 2 Troubleshooting](#part-2-troubleshooting)
- [Part 2 Skills Demonstrated](#part-2-skills-demonstrated)
- [Part 2 What I Learned](#part-2-what-i-learned)

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

- IP Address:
- Provides DHCP
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

## Install Oracle VirtualBox

<img width="1866" height="879" alt="image" src="https://github.com/user-attachments/assets/79ff04e6-d0f5-401e-abec-b748e552da43" />

Installed Oracle VirtualBox to create and manage virtual machines for the lab environment.

Virtualization allows multiple operating systems to run on a single physical computer, making it possible to safely build and test enterprise environments without purchasing dedicated hardware. Oracle VirtualBox provides an isolated environment where servers can be deployed, configured, and reset without affecting the host operating system.

---

## Download Windows Server 2022

<img width="1773" height="624" alt="image" src="https://github.com/user-attachments/assets/20aa6799-f5d2-4c4c-b2cb-1d3f21cf64d0" />

Downloaded the **Windows Server 2022 Evaluation ISO** directly from Microsoft.

Using the official evaluation edition provides access to enterprise Windows Server features while allowing the lab to be built without requiring a production license.

---

## Create the Virtual Machine

<img width="956" height="742" alt="image" src="https://github.com/user-attachments/assets/0816c171-24c4-4296-820b-836a87f0ced9" />

Created a Windows Server virtual machine with the following specifications:

- Windows Server 2022
- 50 GB Virtual Disk
- 4 GB RAM

These specifications provide enough resources to comfortably run Active Directory and DNS services while keeping the virtual machine lightweight enough for a personal lab environment.

The virtual machine will serve as the primary Domain Controller for the lab.

---

## Configure Networking

<img width="772" height="500" alt="image" src="https://github.com/user-attachments/assets/f1e74d46-543f-47f9-8542-7883ae1ba5f2" />

Changed the network adapter from **NAT** to **Bridged Adapter**.

Using a Bridged Adapter places the virtual machine directly on the local network, allowing it to obtain its own IP address from the home router and communicate with other devices as if it were a physical server.

This configuration better simulates a real enterprise network than using NAT.

---

## Install Windows Server 2022

<img width="1024" height="768" alt="VirtualBox_DC-01_04_08_2026_13_40_16 install" src="https://github.com/user-attachments/assets/f531a964-296e-4951-b483-161ac41fbd05" />

Installed **Windows Server 2022 Standard Evaluation (Desktop Experience)**.

Configured:

- Administrator account
- Administrator password
- 50 GB virtual storage

The **Desktop Experience** edition includes the graphical user interface (GUI), making it easier to learn Windows Server administration before transitioning to PowerShell-based management.

<img width="1016" height="843" alt="image" src="https://github.com/user-attachments/assets/635f0c03-8118-46f2-9c94-345b6856bbd4" />

After installation completed, Windows Server booted successfully and the initial configuration tasks were completed.

---

## Rename the Server

<img width="1018" height="765" alt="image" src="https://github.com/user-attachments/assets/44a6e906-00c5-4e25-905c-ffae6979b438" />

Renamed the server to **DC01** (Domain Controller 1).

Using meaningful server names follows common enterprise naming conventions and makes environments easier to manage as additional servers are deployed. Naming servers consistently helps administrators quickly identify each server's purpose within the network.

---

# Configure Static Networking

## Verify the IP Address

<img width="1022" height="769" alt="image" src="https://github.com/user-attachments/assets/3fbea965-0504-4392-bc70-10ac1e49de1d" />

Verified that the server successfully obtained an IP address on the same subnet as my home network (`192.168.1.x`).

Before configuring a static address, I confirmed that the server had network connectivity and was communicating correctly with my router. This establishes a baseline before making any network configuration changes.

---

## Check IP Availability

<img width="746" height="205" alt="image" src="https://github.com/user-attachments/assets/ef5c71e9-64ec-4bd3-adef-a81287b50708" />

Checked that the desired IP address was not already in use by another device on the network.

Verifying IP availability before assigning a static address helps prevent duplicate IP conflicts, which can cause connectivity issues and make troubleshooting more difficult.

---

## Configure a Static IPv4 Address

Active Directory depends heavily on DNS. Because of this, a Domain Controller should always have a static IP address.

| Setting | Value |
|----------|-------|
| IPv4 Address | `192.168.1.50` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |
| Preferred DNS | `192.168.1.50` |

<img width="1010" height="754" alt="image" src="https://github.com/user-attachments/assets/4c0a9c39-8970-4e1b-8ead-e0a5d527589a" />

Configured the server with a static IPv4 address and pointed the Preferred DNS server back to itself.

This is the recommended configuration for Active Directory because the Domain Controller is responsible for hosting DNS. A static IP ensures that domain services remain available and clients can consistently locate authentication and directory services.

---

# Install Active Directory Domain Services

<img width="782" height="556" alt="image" src="https://github.com/user-attachments/assets/59fdf734-41d9-47a4-9e52-e27c1e5889b4" />

<img width="1019" height="729" alt="image" src="https://github.com/user-attachments/assets/93fa7ca0-6ed8-4d12-a515-29a031bf08b3" />

Installed the **Active Directory Domain Services (AD DS)** role using **Server Manager**.

Active Directory Domain Services provides centralized identity management and allows administrators to manage users, computers, groups, Organizational Units (OUs), and security policies from a central location.

Installing this server role prepares Windows Server to become a Domain Controller.

The AD DS role includes support for:

- Centralized user authentication
- Computer account management
- Security groups
- Organizational Units (OUs)
- Group Policy
- Domain administration
- Authentication and authorization services

Once the installation completed, the server was ready to be promoted into a Domain Controller by creating a new Active Directory forest.

---

# Create the Active Directory Forest

## Promote the Server

<img width="1027" height="758" alt="image" src="https://github.com/user-attachments/assets/95e8a2d4-a8c7-4e2d-abb2-8ef8d2c11cb7" />

After installing the Active Directory Domain Services role, I promoted the Windows Server to a **Domain Controller** using the **Active Directory Domain Services Configuration Wizard**.

Promoting the server installs the services required to host Active Directory and allows the server to provide centralized authentication, authorization, and directory services for the domain.

This is one of the most important steps in the deployment because it transforms a standalone Windows Server into the first Domain Controller of the environment.

---

## Create the Forest

<img width="1021" height="760" alt="image" src="https://github.com/user-attachments/assets/9bf64cd6-7a8d-4f6a-a95d-0b41352ba128" />

Created a new Active Directory forest named:

```text
lab.local
```

Configured the **Directory Services Restore Mode (DSRM)** password during the promotion process.

The DSRM password is used for recovering or repairing Active Directory if the Domain Controller cannot start normally.

Since this is the first Domain Controller in the environment, creating the forest also establishes the root domain for the entire Active Directory infrastructure.

---

## Verify the Domain

<img width="1023" height="762" alt="image" src="https://github.com/user-attachments/assets/f4f9ea9d-2a6d-4235-a455-be6c7b1fa4b7" />

After restarting the server, Windows displayed:

```text
LAB\Administrator
```

This confirmed that the Domain Controller was successfully promoted and that the **lab.local** Active Directory forest was functioning correctly.

At this stage, the server became responsible for authenticating users, storing directory information, and hosting DNS for the domain.

---

# Configure DNS Forwarding

<img width="804" height="508" alt="image" src="https://github.com/user-attachments/assets/c87a0947-71e7-48d3-9732-ce5c1bb775c1" />

Configured a DNS Forwarder pointing to my home router (`192.168.1.1`).

By default, the Domain Controller can resolve internal Active Directory records but cannot resolve external internet domain names.

Configuring a DNS forwarder allows requests for external domains—such as `google.com`—to be forwarded to my router. This enables internet access for Windows Updates, software downloads, and public DNS resolution while still allowing the Domain Controller to resolve internal Active Directory records.

This configuration mirrors how many enterprise environments configure their internal DNS servers.

---

# Configure Organizational Units (OUs)

<img width="748" height="528" alt="image" src="https://github.com/user-attachments/assets/cd8de27f-8490-43d1-9fdd-58d566bd8d60" />

Created **Organizational Units (OUs)** to organize Active Directory objects into a logical structure.

Instead of storing every object inside the default **Users** container, Organizational Units provide a way to separate departments, computers, service accounts, and administrative resources.

Benefits of using OUs include:

- Better organization of Active Directory objects
- Simplified administration
- Easier delegation of administrative permissions
- Ability to apply **Group Policy Objects (GPOs)** to specific users or computers
- Improved scalability as the environment grows

Using Organizational Units follows enterprise best practices and creates a structured directory that is easier to manage over time.

---

# Create Users and Security Groups

<img width="758" height="526" alt="image" src="https://github.com/user-attachments/assets/8b8511ff-4771-4c68-8597-58c81b005846" />

<img width="759" height="526" alt="image" src="https://github.com/user-attachments/assets/3a463f92-83c5-43a2-a093-c822a0a21c05" />

<img width="757" height="527" alt="image" src="https://github.com/user-attachments/assets/aeb9eb0d-607b-4441-a58b-f4cd10713c71" />

Created several Active Directory user accounts and security groups to simulate a small business environment.

In a production environment, administrators typically assign permissions to **security groups** rather than directly to individual users. This simplifies administration because access only needs to be managed at the group level.

### Identity and Access Management (IAM)

One of the most valuable concepts I learned during this lab is the relationship between users and groups.

- **Users** represent individual identities.
- **Groups** represent collections of permissions.

By adding users to the appropriate security groups, administrators can efficiently manage access across an organization while following the **Principle of Least Privilege**, which grants users only the permissions they require to perform their job.

This model is commonly referred to as **Role-Based Access Control (RBAC)** and is considered an industry best practice for enterprise environments.

---

# Assign Users to Security Groups

<img width="763" height="526" alt="image" src="https://github.com/user-attachments/assets/3746e541-a4d8-45e9-8e96-847f1832df95" />

<img width="750" height="523" alt="image" src="https://github.com/user-attachments/assets/8cf336dd-726c-4546-989e-789a0d106133" />

Assigned each user account to its corresponding security group.

Managing permissions through security groups rather than individual users makes administration significantly easier. If a user's job role changes, administrators simply update the user's group membership instead of modifying permissions across multiple resources.

This approach reduces administrative overhead, minimizes configuration errors, and improves security.

---

# Configure Group Policy

<img width="861" height="591" alt="image" src="https://github.com/user-attachments/assets/80b526c0-784e-4ce2-90fd-b9b50baac6f9" />

Opened the **Default Domain Policy** using the **Group Policy Management Console (GPMC)**.

Group Policy is one of the most powerful features of Active Directory because it allows administrators to centrally configure settings across every computer and user within the domain.

Examples of settings managed through Group Policy include:

- Password complexity requirements
- Password expiration policies
- Account lockout policies
- Security settings
- Desktop configurations
- Windows Update settings
- Software deployment
- Login scripts

Using Group Policy ensures consistency, improves security, and reduces the amount of manual configuration required on individual computers.

---

# Verify Active Directory with PowerShell

<img width="612" height="248" alt="image" src="https://github.com/user-attachments/assets/826a467b-1d59-4d1c-b3e7-bb3bcf04725d" />

<img width="561" height="178" alt="image" src="https://github.com/user-attachments/assets/8745155d-1e5b-497a-a55d-8a462824bfa8" />

<img width="608" height="180" alt="image" src="https://github.com/user-attachments/assets/41264b7f-7277-4a42-a05a-d18c194b1401" />

Used PowerShell and networking tools to verify that Active Directory and DNS were functioning correctly.

Validation included:

- Retrieving Active Directory users using `Get-ADUser`
- Retrieving Active Directory groups using `Get-ADGroup`
- Performing DNS lookups with `nslookup`

The successful results confirmed that:

- Active Directory was functioning correctly.
- User accounts were successfully created.
- Security groups were properly configured.
- DNS was resolving both internal and external domain names.
- DNS forwarding was operating correctly.
- The Domain Controller could communicate with external DNS servers.

PowerShell is an essential tool for Windows administrators because it enables automation, configuration management, and rapid troubleshooting across enterprise environments.

---

# Skills Demonstrated

Throughout this project, I gained practical experience with the following technologies and concepts:

## Windows Server Administration

- Windows Server 2022 Installation
- Server Manager
- Domain Controller Deployment
- Windows Server Roles and Features
- Windows System Administration

---

# What I Learned

This project gave me hands-on experience deploying and managing a Windows Active Directory environment from the ground up.

Throughout this lab, I installed Windows Server 2022, configured networking and DNS, deployed Active Directory Domain Services, created Organizational Units, managed users and security groups, configured Group Policy, and verified the environment using PowerShell.

Most importantly, I strengthened my understanding of how Active Directory, DNS, Group Policy, and Role-Based Access Control (RBAC) work together in an enterprise environment. This project also improved my troubleshooting skills and gave me practical experience with technologies commonly used by IT support and system administrators.

---
# Part 2 Overview

---

# Create the Windows 11 Client VM

---

# Configure Client Networking

---

# Configure Client DNS

---

# Test Connectivity to the Domain Controller

---

# Join the Client to the Domain

---

# Verify the Client in Active Directory

---

# Log In with a Domain User

---

# Verify Group Policy

---

# Part 2 Troubleshooting

---

# Part 2 Skills Demonstrated

---

# Part 2 What I Learned

---
