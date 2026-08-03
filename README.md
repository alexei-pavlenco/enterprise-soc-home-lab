# 🛡️ Enterprise SOC Home Lab

> A hands-on enterprise Security Operations Center (SOC) home lab built to simulate real-world cybersecurity operations using Active Directory, Sysmon, Elastic Security, and VMware.

---

# 📖 Project Overview

This project demonstrates the design, deployment, and operation of an enterprise-style Security Operations Center (SOC) environment. The lab provides a realistic platform for developing practical cybersecurity skills including system administration, endpoint monitoring, detection engineering, threat hunting, and incident response.

The environment is built entirely in VMware Workstation and integrates Windows infrastructure with the Elastic Stack to collect, analyze, and investigate security telemetry generated from Windows endpoints.

Unlike tutorial-based labs, this project focuses on documenting the complete lifecycle of building, monitoring, detecting, and investigating security events.

---

# 🎯 Project Objectives

- Design and deploy an enterprise Active Directory environment
- Configure Windows Server 2022 and Windows 11 endpoints
- Deploy Sysmon for advanced endpoint telemetry
- Centralize Windows event logs using Elastic Security
- Create custom detection rules using KQL
- Investigate security alerts and map activity to the MITRE ATT&CK framework
- Simulate attacker techniques in a controlled lab environment
- Document the complete build and investigation process

---

# 🏗️ Lab Architecture

| Component | Status |
|------------|--------|
| VMware Workstation Pro | ✅ Complete |
| Windows Server 2022 Domain Controller | ✅ Complete |
| Active Directory Domain Services | ✅ Complete |
| Organizational Units | ✅ Complete |
| Security Groups | ✅ Complete |
| Windows 11 Workstation | ✅ Complete |
| Sysmon Deployment | ✅ Complete |
| Ubuntu Server | ✅ Complete |
| Elastic Fleet Server | ✅ Complete |
| Elastic Agent | ✅ Complete |
| Elastic Security | ✅ Complete |
| Windows Event Collection | ✅ Complete |
| Sysmon Log Collection | ✅ Complete |
| Custom Detection Rules | ✅ Complete |
| Alert Investigation | ✅ Complete |
| Kali Linux Attack VM | 🚧 Planned |

---

# 💻 Technologies Used

## Infrastructure

- VMware Workstation Pro
- Windows Server 2022
- Windows 11 Pro
- Ubuntu Server

## Identity

- Active Directory
- Group Policy
- Organizational Units
- Security Groups

## Security Monitoring

- Elastic Stack 9.x
- Elastic Security
- Fleet Server
- Elastic Agent
- Kibana
- Sysmon

## Scripting

- PowerShell
- KQL (Kibana Query Language)

---

# 🔍 Detection Engineering

Current detections include:

- ✅ Sysmon Process Creation Detection
- ✅ PowerShell Process Execution Detection

Upcoming detections:

- Encoded PowerShell Commands
- Command Prompt Abuse
- LOLBins (Living off the Land Binaries)
- Brute Force Authentication
- Scheduled Task Persistence
- New Local Administrator Creation
- RDP Activity
- PsExec Execution
- Mimikatz Activity
- BloodHound Enumeration

---

# 🚨 Incident Investigation

Current investigation workflow:

1. Generate endpoint activity
2. Collect telemetry using Sysmon
3. Forward events through Elastic Agent
4. Analyze events in Kibana Discover
5. Trigger custom detection rules
6. Investigate generated alerts
7. Map activity to MITRE ATT&CK
8. Document findings

---

# 🛠️ Skills Demonstrated

- Active Directory Administration
- Windows Server Administration
- Endpoint Monitoring
- Sysmon Deployment
- Elastic Stack Administration
- Fleet Management
- Log Analysis
- Detection Engineering
- KQL Query Development
- Security Alert Investigation
- MITRE ATT&CK Mapping
- Incident Response
- Technical Documentation

---

# 📂 Repository Structure

```
enterprise-soc-home-lab
│
├── Active-Directory
├── Architecture
├── Attack-Simulations
├── Elastic
├── Incident-Reports
├── Resources
├── Screenshots
├── Scripts
├── Sysmon
└── README.md
```

---

# 🚀 Project Roadmap

## ✅ Phase 1 — Infrastructure

- VMware Environment
- Active Directory
- Windows Server 2022
- Windows 11 Endpoint
- Sysmon Deployment

## ✅ Phase 2 — SIEM Deployment

- Ubuntu Server
- Elastic Stack
- Fleet Server
- Elastic Agent
- Windows Log Collection
- Sysmon Integration
- Custom Detection Rules
- Alert Validation

## 🚧 Phase 3 — Detection Engineering

- Advanced KQL Rules
- Detection Tuning
- Dashboard Development
- Threat Hunting

## 🚧 Phase 4 — Attack Simulation

- PowerShell Abuse
- Command Prompt Abuse
- BloodHound
- Kerberoasting
- Lateral Movement
- Privilege Escalation
- Persistence
- Incident Response

---

# 📈 Current Status

**Status:** 🟢 Active Development

Latest accomplishments:

- Successfully deployed Elastic Fleet
- Configured Elastic Agent
- Integrated Sysmon telemetry
- Created custom KQL detection rules
- Generated and investigated first Elastic Security alerts
- Validated end-to-end detection pipeline

---

# 📚 Future Enhancements

- Elastic Dashboards
- Sigma Rule Conversion
- Detection-as-Code
- Malware Analysis
- Threat Intelligence Integration
- SOAR Automation
- Purple Team Exercises

---

# 👨‍💻 Author

**Alexei Pavlenco**

Cybersecurity Analyst

Building practical cybersecurity skills through enterprise security engineering, detection engineering, and incident response projects.
