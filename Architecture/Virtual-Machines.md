# 💻 Virtual Machines

This document describes the virtual infrastructure used in the Enterprise SOC Home Lab.

---

# DC01 – Domain Controller

| Property | Value |
|----------|-------|
| Hostname | DC01 |
| Operating System | Windows Server 2022 |
| Primary Role | Active Directory Domain Controller |
| Domain | cyberlab.local |
| Services | Active Directory Domain Services (AD DS), DNS |
| Purpose | Provides centralized authentication, authorization, and domain management for the lab environment. |

---

# WS01 – Windows Workstation

| Property | Value |
|----------|-------|
| Hostname | WS01 |
| Operating System | Windows 11 Pro |
| Primary Role | Domain-Joined Endpoint |
| Installed Software | Sysmon, Elastic Agent |
| Purpose | Simulates an enterprise user workstation and generates endpoint telemetry for monitoring and detection. |

---

# ELK01 – Elastic Server

| Property | Value |
|----------|-------|
| Hostname | ELK01 |
| Operating System | Ubuntu Server |
| Primary Role | Security Monitoring Platform |
| Installed Software | Elasticsearch, Kibana, Fleet Server |
| Purpose | Centralizes logs, manages Elastic Agents, creates detection rules, and supports security investigations. |

---

# Future Virtual Machines

| Hostname | Purpose | Status |
|----------|---------|--------|
| KALI01 | Attack Simulation | Planned |
| Additional Workstations | Lateral Movement & Detection | Planned |

---

# Virtual Infrastructure Summary

| Virtual Machine | Function |
|----------------|----------|
| DC01 | Active Directory & DNS |
| WS01 | Windows Endpoint |
| ELK01 | Elastic SIEM Platform |
| KALI01 | Offensive Security Testing (Planned) |

---

## Skills Demonstrated

- VMware Workstation Administration
- Active Directory Deployment
- Windows Endpoint Administration
- Ubuntu Server Administration
- Elastic Stack Deployment
- Enterprise Lab Design
