# Incident Report 001 – PowerShell Process Detection

## Incident Summary

This incident demonstrates the successful detection and investigation of a PowerShell-initiated process execution within the Enterprise SOC Home Lab. The activity was intentionally generated to validate the end-to-end detection pipeline, including Sysmon, Elastic Agent, Elastic Security, and custom KQL detection rules.

The objective was to verify that endpoint telemetry was successfully collected, analyzed, and converted into actionable security alerts.

---

# Incident Information

| Item | Value |
|------|-------|
| Incident ID | IR-001 |
| Date | August 3, 2026 |
| Severity | Medium |
| Status | Closed |
| Detection Method | Custom KQL Detection Rule |
| Data Source | Sysmon Event ID 1 |
| Endpoint | WS01 |
| Analyst | Alexei Pavlenco |

---

# Environment

| Component | Description |
|----------|-------------|
| Endpoint | Windows 11 Pro |
| Hostname | WS01 |
| SIEM | Elastic Security 9.4.4 |
| Endpoint Telemetry | Sysmon |
| Log Collection | Elastic Agent |
| Management | Fleet Server |

---

# Detection Rule

**Rule Name**

```
PowerShell Process Execution
```

**Rule Type**

```
Custom Query
```

**KQL Query**

```kql
winlog.channel : "Microsoft-Windows-Sysmon/Operational"
and event.code : "1"
```

---

# Alert Details

| Field | Value |
|-------|-------|
| Alert Severity | Medium |
| Risk Score | 50 |
| Event Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Alert Status | Open (during validation) |

---

# Investigation

## Observed Activity

The investigation identified a PowerShell process spawning the **whoami.exe** executable.

### Parent Process

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

### Child Process

```text
C:\Windows\System32\whoami.exe
```

### Executed Command

```powershell
whoami
```

### User

```text
CYBERLAB\Administrator
```

### Host

```text
WS01
```

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1033 | System Owner/User Discovery |

The execution of **whoami.exe** is commonly used by attackers after gaining initial access to determine the security context of the compromised account.

---

# Evidence Collected

The following evidence was successfully collected:

- Sysmon Process Creation Event (Event ID 1)
- Parent process information
- Child process information
- Command line execution
- User account
- Hostname
- Process hashes
- Process GUID
- Parent Process GUID

---

# Root Cause

The alert was intentionally generated during detection validation by executing the **whoami** command from PowerShell. This confirmed that Sysmon telemetry was successfully collected and that the custom Elastic Security detection rule functioned as expected.

No malicious activity occurred.

---

# Impact Assessment

No production systems were affected.

The event was generated in a controlled lab environment for validation purposes.

Business Impact:

- None

Operational Impact:

- Successful validation of the Elastic Security detection pipeline.

---

# Lessons Learned

- Successfully integrated Sysmon with Elastic Security.
- Validated Elastic Agent communication through Fleet.
- Confirmed end-to-end telemetry collection.
- Successfully created a custom KQL detection rule.
- Verified that Elastic Security generated alerts based on Sysmon process creation events.
- Demonstrated the complete detection and investigation workflow.

---

# Future Improvements

- Detect encoded PowerShell commands.
- Detect PowerShell ExecutionPolicy Bypass.
- Detect LOLBins.
- Detect credential dumping tools.
- Build automated dashboards for endpoint telemetry.
- Expand MITRE ATT&CK coverage.

---

# Screenshots

The following screenshots accompany this report:

1. Fleet Agents Healthy
2. Sysmon Events in Discover
3. Custom Detection Rule
4. Alert Generated
5. Alert Investigation
