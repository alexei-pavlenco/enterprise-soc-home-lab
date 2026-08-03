                   # 🌐 Enterprise SOC Network Diagram

## Overview

The Enterprise SOC Home Lab is designed to simulate a small enterprise network. The environment consists of a Windows Active Directory domain, a monitored Windows workstation, and an Elastic Security platform responsible for collecting, analyzing, and detecting security events.

---

# Network Topology

```
                    VMware Workstation Pro
                           │
          ┌────────────────┴────────────────┐
          │        Virtual Network          │
          │       192.168.149.0/24          │
          └────────────────┬────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
     DC01               WS01              ELK01
 Windows Server       Windows 11        Ubuntu Server
 Active Directory     Elastic Agent     Elasticsearch
 DNS                  Sysmon            Kibana
 Domain Controller                     Fleet Server
```

---

# Virtual Machines

| Host | Role | Purpose |
|------|------|---------|
| DC01 | Domain Controller | Active Directory, DNS, Authentication |
| WS01 | Workstation | Endpoint telemetry and security monitoring |
| ELK01 | SIEM | Log collection, detection, and investigation |

---

# Data Flow

1. User activity occurs on **WS01**
2. Sysmon records endpoint events
3. Elastic Agent collects the logs
4. Logs are forwarded to **ELK01**
5. Elasticsearch indexes the data
6. Kibana visualizes the events
7. Elastic Security detection rules generate alerts
8. Analysts investigate alerts through Kibana

---

# Security Components

- Active Directory
- Sysmon
- Elastic Agent
- Fleet Server
- Elasticsearch
- Kibana
- Elastic Security

---

## Future Expansion

Planned additions include:

- Kali Linux attack workstation
- BloodHound
- Atomic Red Team
- Sigma Rules
- Threat Intelligence
