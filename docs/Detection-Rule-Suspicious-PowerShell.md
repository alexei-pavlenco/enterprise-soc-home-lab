# Detection Rule: Suspicious PowerShell Execution

---

## Executive Summary

This detection rule identifies PowerShell execution on a monitored Windows 11 endpoint using **Sysmon**, **Elastic Agent**, and **Elastic Security**.

Although PowerShell is a legitimate administrative tool, it is one of the most frequently abused utilities by threat actors for executing malicious scripts, downloading payloads, establishing persistence, performing reconnaissance, and evading detection.

This project demonstrates an end-to-end Security Operations Center (SOC) workflow by collecting endpoint telemetry, detecting suspicious activity, generating a security alert, and documenting the investigation process.

---

# Detection Objective

The objective of this detection is to identify PowerShell process creation events recorded by Sysmon and generate an alert inside Elastic Security.

The detection validates the complete security monitoring pipeline:

```
Windows Endpoint
        │
        ▼
Sysmon (Event ID 1)
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
Kibana Discover
        │
        ▼
Detection Rule
        │
        ▼
Security Alert
        │
        ▼
Incident Investigation
```

---

# Lab Environment

| Component | Description |
|------------|-------------|
| Endpoint | Windows 11 (WS01) |
| Domain Controller | Windows Server 2022 (DC01) |
| SIEM Platform | Elastic Security |
| Log Collection | Elastic Agent |
| Endpoint Logging | Sysmon |
| Visualization | Kibana |
| Operating System | Ubuntu Server (Elastic Stack) |

---

# Data Source

The detection relies on **Sysmon Event ID 1 (Process Creation)**.

Each time a process starts on the endpoint, Sysmon records detailed metadata including:

- Process Name
- Command Line
- Parent Process
- User
- Host
- Process ID
- Timestamp

Elastic Agent forwards these events into Elasticsearch where they become searchable in Kibana.

---

# Detection Logic

## KQL Query

```kql
winlog.event_id: 1 and process.name: "powershell.exe"
```

This query identifies Sysmon Process Creation events where the executed process is **powershell.exe**.

---

## Expanded Detection

The rule can also detect PowerShell Core.

```kql
winlog.event_id: 1 and
(process.name: "powershell.exe" or process.name: "pwsh.exe")
```

---

# Rule Configuration

| Setting | Value |
|----------|-------|
| Rule Name | Suspicious PowerShell Execution |
| Rule Type | Custom Query |
| Query Language | KQL |
| Severity | Medium |
| Risk Score | 47 |
| Rule Schedule | Every 5 Minutes |
| Additional Look-back | 1 Minute |
| Index Pattern | logs-* |
| Status | Enabled |

---

# Validation Procedure

To validate the detection rule, several PowerShell commands were executed on the Windows endpoint.

Example commands:

```powershell
whoami

Get-Process

Get-Service
```

These commands generate legitimate PowerShell activity while allowing the SIEM pipeline to be validated.

---

# Investigation Workflow

After the alert was generated, the event was investigated using Kibana Discover and Elastic Security.

The investigation focused on the following fields:

- host.name
- user.name
- process.name
- process.command_line
- process.parent.name
- process.pid
- winlog.event_id
- @timestamp
- agent.name

The investigation confirmed that:

- PowerShell execution originated from WS01
- Sysmon successfully captured the process
- Elastic Agent forwarded the event
- Elasticsearch indexed the log
- The custom detection rule triggered successfully
- Elastic Security generated an alert
- The activity was an authorized laboratory test

---

# Alert Classification

**Classification**

> True Positive – Authorized Administrative Activity

The detection rule correctly identified PowerShell execution.

The activity was expected because it was intentionally performed during laboratory testing.

No containment or remediation actions were required.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|----------|-----------|------------|
| Execution | Command and Scripting Interpreter | T1059 |
| Execution | PowerShell | T1059.001 |

PowerShell remains one of the most commonly abused Windows utilities during post-exploitation and lateral movement.

---

# SOC Analyst Playbook

When this alert is generated in a production environment, the analyst should perform the following actions:

1. Review the PowerShell command line.
2. Identify the initiating user.
3. Review the parent process.
4. Determine whether the command is Base64 encoded.
5. Check for execution-policy bypasses.
6. Review network connections initiated by PowerShell.
7. Search for additional activity from the same endpoint.
8. Determine whether the activity is authorized.
9. Escalate suspicious behavior to Incident Response if necessary.

---

# Future Detection Improvements

The initial detection focuses on all PowerShell execution.

Future improvements include detecting:

- Encoded PowerShell
- Hidden PowerShell windows
- Execution Policy Bypass
- DownloadString()
- Invoke-WebRequest
- Invoke-Expression
- PowerShell spawned from Microsoft Office
- Suspicious parent-child process relationships
- Network connections initiated by PowerShell

Example:

```kql
winlog.event_id: 1 and
process.name: "powershell.exe" and
process.command_line: (
    "*-enc*" or
    "*-encodedcommand*" or
    "*downloadstring*" or
    "*invoke-webrequest*" or
    "*bypass*"
)
```

---

# Evidence

The following screenshots document the detection workflow.

| Screenshot | Description |
|------------|-------------|
| 01 | PowerShell Test Command |
| 02 | Sysmon Event ID 1 |
| 03 | Kibana Discover |
| 04 | Detection Rule Configuration |
| 05 | Elastic Security Alert |
| 06 | Alert Investigation |
| 07 | MITRE ATT&CK Mapping |

---

# Lessons Learned

This project demonstrates how endpoint telemetry can be transformed into actionable security alerts using the Elastic Stack.

The implementation highlights several important SOC concepts:

- Endpoint telemetry collection
- Centralized log management
- Custom detection engineering
- Security alert generation
- Incident triage
- Threat hunting foundations
- MITRE ATT&CK mapping
- Security documentation

---

# Outcome

This detection successfully validated the complete monitoring pipeline:

```
Windows Endpoint
      ↓
Sysmon
      ↓
Elastic Agent
      ↓
Fleet Server
      ↓
Elasticsearch
      ↓
Kibana
      ↓
Detection Rule
      ↓
Security Alert
      ↓
SOC Investigation
```

The project demonstrates practical experience with **Windows endpoint monitoring**, **Elastic Security**, **Sysmon**, **SIEM detection engineering**, and **incident investigation**, closely mirroring workflows used by modern Security Operations Centers.
