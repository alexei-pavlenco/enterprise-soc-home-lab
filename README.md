<p align="center">
  <img src="images/github-banner.png"
       alt="Enterprise SOC Home Lab Banner"
       width="100%">
</p>

<p align="center">
  <strong>Enterprise Security Operations Center (SOC) | Threat Hunting | Detection Engineering | Elastic Security | Active Directory</strong>
</p>

# 🛡️ Enterprise SOC Home Lab

![Status](https://img.shields.io/badge/Project-Completed-brightgreen)
![Elastic Security](https://img.shields.io/badge/SIEM-Elastic%20Security-005571)
![Sysmon](https://img.shields.io/badge/Endpoint-Sysmon-blue)
![Windows](https://img.shields.io/badge/OS-Windows%2011-0078D6)
![Active Directory](https://img.shields.io/badge/Directory-Active%20Directory-003366)
![MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE_ATT%26CK-red)
![KQL](https://img.shields.io/badge/Language-KQL-orange)

---

## Project Overview

This project demonstrates the design, deployment, and operation of a simulated Enterprise Security Operations Center (SOC) using industry-standard security tools and enterprise infrastructure.

The lab was built to simulate a real-world corporate environment where endpoint telemetry is collected, centralized, analyzed, detected, and investigated using Elastic Security.

The objective of this project is to demonstrate hands-on experience with:

- Security Monitoring
- Detection Engineering
- Threat Hunting
- Incident Response
- Active Directory Administration
- Endpoint Logging
- SIEM Investigation
- MITRE ATT&CK Mapping

---

![Lab Overview](Architecture/01-Lab-Overview.png)

![Detection Pipeline](Architecture/02-Detection-Pipeline.png)

---

# Technologies Used

| Technology | Purpose |
|------------|---------|
| VMware Workstation Pro | Virtualization Platform |
| Windows Server 2022 | Active Directory Domain Controller |
| Windows 11 | Endpoint Workstation |
| Ubuntu Server | Elastic Stack |
| Elastic Security | SIEM Platform |
| Elasticsearch | Log Storage |
| Kibana | Visualization & Investigation |
| Fleet | Agent Management |
| Elastic Agent | Log Collection |
| Sysmon | Endpoint Telemetry |
| PowerShell | Administrative Testing |
| MITRE ATT&CK | Threat Mapping |
| KQL | Detection Queries |

---

# Skills Demonstrated

- Security Operations Center (SOC)
- SIEM Administration
- Elastic Security
- Detection Engineering
- Threat Hunting
- Incident Investigation
- Active Directory
- Windows Administration
- Endpoint Security
- Sysmon Configuration
- Fleet Management
- KQL Query Development
- Log Analysis
- MITRE ATT&CK Mapping
- Security Documentation

---

# Documentation

| Document | Description |
|----------|-------------|
| [📁 Detection Rules](Detection-Rules/README.md) | Custom detection-rule library and coverage |
| [📄 PowerShell Execution Policy Bypass](Detection-Rules/PowerShell-Execution-Policy-Bypass.md) | Sysmon Event ID 1 detection, testing, and validation |
| [📄 Windows User Account Creation](Detection-Rules/Windows-User-Account-Creation.md) | Windows Event ID 4720 detection and investigation |
| [📄 Architecture Overview](Architecture/README.md) | Enterprise SOC architecture |
| [📄 Network Diagram](Architecture/Network-Diagram.md) | Network topology |
| [📄 Suspicious PowerShell Rule](docs/Detection-Rule-Suspicious-PowerShell.md) | Original PowerShell detection-engineering workflow |
| [📄 Threat Hunting Report](docs/Threat-Hunting-Report.md) | Threat-hunting methodology |
| [📄 Incident Report](Incident-Reports/IR-001-PowerShell-Process-Detection.md) | Incident-investigation workflow |
| [📄 Virtual Machines](Architecture/Virtual-Machines.md) | Virtual-machine configuration |
---

---

# Detection Engineering Highlights

## Suspicious PowerShell Execution

- Collected Sysmon Event ID 1 process-creation telemetry from `WS01`
- Developed KQL logic for suspicious PowerShell command-line indicators
- Executed a controlled `ExecutionPolicy Bypass` test
- Validated matching events in Kibana Discover
- Documented investigation guidance and potential false positives

## New Windows User Account

- Monitored Windows Security Event ID 4720
- Created the temporary `SOC-Lab-TEST` account during controlled testing
- Generated and investigated a medium-severity Elastic alert
- Verified the initiating user and target-account fields
- Added an analyst investigation note
- Removed the temporary account after validation
  
# Enterprise Environment

## Infrastructure

- Domain Controller (DC01)
- Windows 11 Endpoint (WS01)
- Ubuntu Elastic Server
- Fleet Server
- Elasticsearch
- Kibana

---

# Security Monitoring Workflow

```
User Activity
      │
      ▼
Windows Endpoint
      │
      ▼
Sysmon
      │
      ▼
Elastic Agent
      │
      ▼
Fleet Server
      │
      ▼
Elasticsearch
      │
      ▼
Kibana
      │
      ▼
Detection Rule
      │
      ▼
Security Alert
      │
      ▼
Threat Hunting
      │
      ▼
Incident Investigation
```

---

# MITRE ATT&CK Coverage

| Tactic | Technique |
|----------|-----------|
| Execution | PowerShell — T1059.001 |
| Persistence | Create Account: Local Account — T1136.001 |
| Defense Evasion | Obfuscated/Compressed Files and Information — T1027 |
| Command and Control | Ingress Tool Transfer — T1105 |

---

enterprise-soc-home-lab/
│
├── Active-Directory/
├── Architecture/
├── Attack-Simulations/
├── Detection-Rules/
│   ├── README.md
│   ├── PowerShell-Execution-Policy-Bypass.md
│   └── Windows-User-Account-Creation.md
├── Elastic/
├── Incident-Reports/
├── Resources/
├── Scripts/
├── Sysmon/
├── docs/
├── images/
└── README.md
```

---

# Future Enhancements

- Windows Event Forwarding (WEF)
- Sysmon Configuration Tuning
- Sigma Rule Integration
- Additional Detection Rules
- Malware Analysis
- Atomic Red Team Testing
- ATT&CK Coverage Expansion
- Automated Alerting
- SOAR Integration
- Threat Intelligence Feeds

---

# Project Outcomes

This lab successfully demonstrates practical experience with enterprise security monitoring, centralized logging, endpoint detection, threat hunting, incident response, and detection engineering.

The project closely mirrors workflows performed by Security Operations Center (SOC) analysts and provides a foundation for future security engineering and threat detection projects.
