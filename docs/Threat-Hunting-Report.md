# Threat Hunting Report

---

# Executive Summary

This report documents proactive threat hunting activities performed within the Enterprise SOC Home Lab using Elastic Security and Kibana.

The objective was to identify potentially suspicious behavior by analyzing endpoint telemetry collected from Windows endpoints through Sysmon and Elastic Agent.

Rather than relying solely on automated alerts, multiple hunting queries were executed to search for attacker techniques commonly observed during real-world incidents.

---

# Lab Environment

| Component | Description |
|-----------|-------------|
| SIEM | Elastic Security |
| Endpoint | Windows 11 (WS01) |
| Domain Controller | Windows Server 2022 |
| Logging | Sysmon |
| Log Collection | Elastic Agent |
| Visualization | Kibana Discover |

---

# Hunt #1 — PowerShell Activity

## Objective

Identify all PowerShell execution occurring on monitored endpoints.

## Query

```kql
winlog.event_id: 1 and
winlog.event_data.Image: "*\\powershell.exe"
```

## Why This Matters

PowerShell is one of the most abused Windows utilities during cyber attacks because it allows attackers to execute scripts without dropping files onto disk.

## Findings

PowerShell execution was successfully observed from the Windows endpoint.

The commands were executed as part of authorized laboratory testing.

## MITRE ATT&CK

- T1059.001 – PowerShell

---

# Hunt #2 — Encoded PowerShell Commands

## Objective

Identify attempts to hide PowerShell commands using Base64 encoding.

## Query

```kql
winlog.event_data.CommandLine: "*-enc*" or
winlog.event_data.CommandLine: "*-encodedcommand*"
```

## Why This Matters

Attackers frequently encode PowerShell commands to evade detection.

## Findings

No encoded PowerShell commands were identified during this assessment.

## MITRE ATT&CK

- T1059.001

---

# Hunt #3 — Download Activity

## Objective

Search for PowerShell attempting to download remote content.

## Query

```kql
winlog.event_data.CommandLine: "*invoke-webrequest*" or
winlog.event_data.CommandLine: "*downloadstring*"
```

## Why This Matters

Malware commonly uses these commands to retrieve additional payloads.

## Findings

No suspicious download activity was identified.

## MITRE ATT&CK

- T1105 – Ingress Tool Transfer

---

# Hunt #4 — Suspicious Parent Processes

## Objective

Identify PowerShell launched by unusual parent processes.

## Query

```kql
winlog.event_id: 1 and
winlog.event_data.ParentImage: "*winword.exe"
```

## Why This Matters

Microsoft Office spawning PowerShell is commonly associated with malicious Office documents.

## Findings

No suspicious parent-child process relationships were identified.

## MITRE ATT&CK

- T1204 – User Execution

---

# Hunt #5 — Administrative Utilities

## Objective

Search for common Living-off-the-Land Binaries (LOLBins).

## Query

```kql
winlog.event_data.Image: (
    "*cmd.exe" or
    "*certutil.exe" or
    "*bitsadmin.exe" or
    "*wmic.exe" or
    "*rundll32.exe"
)
```

## Why This Matters

Attackers often abuse trusted Windows utilities to evade traditional security controls.

## Findings

Only expected administrative activity was observed.

No suspicious LOLBin execution was detected.

## MITRE ATT&CK

- T1218 – System Binary Proxy Execution

---

# Hunt Summary

| Hunt | Result |
|------|--------|
| PowerShell Activity | Observed |
| Encoded Commands | None Detected |
| Download Commands | None Detected |
| Suspicious Parent Process | None Detected |
| LOLBins | Normal Activity |

---

# Analyst Assessment

The hunting activities identified only expected administrative behavior generated during laboratory testing.

No indicators of compromise were identified.

The environment behaved as expected and all observed activity was consistent with authorized testing.

---

# Recommendations

Future hunting activities should include:

- Network connections initiated by PowerShell
- Scheduled Tasks
- Registry persistence
- New local user creation
- Service creation
- Lateral movement
- RDP activity
- SMB activity
- DNS anomalies
- Authentication failures

---

# Lessons Learned

Threat hunting complements automated detection by enabling analysts to proactively search for suspicious activity before alerts are generated.

This exercise demonstrated the ability to:

- Build hunting queries using KQL
- Analyze endpoint telemetry
- Investigate Sysmon events
- Validate normal versus suspicious behavior
- Map findings to MITRE ATT&CK
- Document investigative results

---

# Outcome

This threat hunting exercise demonstrates practical experience using Elastic Security to proactively search endpoint telemetry for attacker techniques commonly associated with modern cyber threats.

The process closely reflects real-world SOC analyst responsibilities involving detection engineering, threat hunting, and incident investigation.
