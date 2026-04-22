# Windows Server Project 🖥️

A comprehensive Windows Server infrastructure project covering Active Directory, DNS, IIS, FTP, RDP, and Group Policy configuration across a multi-site domain environment.

> Supervised by: **Eng. Mohamed Abosehly**

---

## Project Overview

This project simulates a real-world enterprise network environment built on Windows Server. It includes domain management, user policy enforcement, web hosting, remote access, and multi-site domain architecture — all connected over a local network using static IP addressing.

---

## Infrastructure & Architecture

- All physical PCs and virtual machines were connected on a single local network via mobile hotspot
- Static IP addresses were assigned to all devices for stable and organized communication
- The primary domain `ITI.local` was established as the root of the forest
- A child domain `fayoum.ITI.local` was created to represent a separate branch with local authentication and administrative separation
- A secondary DNS zone was configured at `portsaid.ITI.local`

---

## Features Implemented

### Active Directory & Domain Controllers
- Installed and configured **Active Directory Domain Services (AD DS)**
- Set up the primary Domain Controller **DC2** with a static IP
- Promoted a second server as an **Additional Domain Controller (DC4)** for redundancy and load distribution
- Created **Organizational Units (OUs)** and user accounts (user1 through user8) to structure the domain

### User Management & Access Control
- **USR1** — Restricted from logging into PC1 on Fridays (logon hours policy)
- **user2** — Can log into PC1 and remotely access DC1 (non-domain admin RDP access)
- **user3** — Software restriction: WinRAR was installed by a domain admin; user cannot install software
- **user3 & user4** — Blocked from using flash memory and Control Panel; desktop wallpaper set to ITI logo via GPO
- **user6** — Member of `portsaid.ITI.local`; can access `www.web2.com` via a Secondary DNS Zone
- **user7** — Local user on PC4 with remote admin privileges on the web server; uses FTP to back up IIS logs
- **user8** — Roaming profile user; settings and data follow the user across all domain computers

### Group Policy (GPO)
- Configured multiple GPOs linked to OUs for permission management and security enforcement
- Policies include: Control Panel restriction, flash memory block, desktop wallpaper enforcement, software installation control, and remote login rules
- Software deployment policy used to automatically install applications domain-wide

### Web Server & DNS
- Hosted two websites via IIS:
  - `www.web1.com` — HTTP
  - `www.web2.com` — HTTPS
- Configured forward lookup zones in DNS for both websites
- Secondary DNS zone set up in `portsaid` for `www.web2.com` resolution

### FTP Configuration
- Implemented an FTP server at `www.ftplogs.com` for centralized IIS log collection and backup management from the web server

### RDP Configuration
- Enabled Remote Desktop Protocol (RDP) for secure remote administration across domain machines

### Roaming Profiles
- Configured roaming profiles so that user settings and data remain consistent regardless of which domain computer the user logs into

---

## Problems Encountered

- **Network connectivity issues** — DNS errors and routing failures caused intermittent connection problems between sites and domain controllers
- **Domain Controller failure** — PDC failure led to login disruptions and replication issues
- **Network adapter misconfiguration** — Incorrect IP/DNS settings and disabled adapters caused connectivity breaks
- **GPO deployment issues** — Slow policy replication, incorrect security filtering, and conflicts between overlapping policies

---

## Technologies Used

- Windows Server 2022
- Active Directory Domain Services (AD DS)
- DNS Manager
- IIS (Internet Information Services)
- FTP Server
- Remote Desktop Protocol (RDP)
- Group Policy Management Console (GPMC)
- VMware Workstation

---

## Supervisor

**Eng. Mohamed Abosehly** — ITI
