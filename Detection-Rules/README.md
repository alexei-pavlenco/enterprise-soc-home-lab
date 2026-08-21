# Detection Rules

This folder documents the custom detection rules developed and tested in the Enterprise SOC Home Lab.

The rules use Windows Sysmon telemetry collected from the `WS01` endpoint and forwarded through Elastic Agent to Elasticsearch and Kibana. Each rule includes its objective, data source, KQL logic, testing process, investigation guidance, and MITRE ATT&CK mapping.

## Detection Environment

* **Endpoint:** WS01 — Windows 11
* **Telemetry:** Sysmon
* **Event:** Sysmon Event ID 1 — Process Creation
* **Collection:** Elastic Agent
* **SIEM:** Elastic Security
* **Query language:** Kibana Query Language (KQL)

## Detection Coverage

| Detection                    | Objective                                                          | MITRE ATT&CK                                        |
| ---------------------------- | ------------------------------------------------------------------ | --------------------------------------------------- |
| PowerShell Execution         | Identify PowerShell process creation                               | T1059.001 — PowerShell                              |
| [Execution Policy Bypass](PowerShell-Execution-Policy-Bypass.md) | Detect PowerShell launched with the `Bypass` argument | T1059.001 — PowerShell       |
| Encoded PowerShell           | Identify potentially obfuscated PowerShell commands                | T1027 — Obfuscated/Compressed Files and Information |
| Suspicious Download Commands | Detect PowerShell download activity using commonly abused commands | T1105 — Ingress Tool Transfer                       |

## Baseline KQL Query

```kql
winlog.channel:"Microsoft-Windows-Sysmon/Operational" and
winlog.event_id:1 and
winlog.event_data.Image:*powershell.exe
```

Additional command-line conditions can be added to identify behaviors such as:

* `Bypass`
* `-enc`
* `-encodedcommand`
* `DownloadString`
* `Invoke-WebRequest`

## Validation Process

1. Execute controlled PowerShell commands on `WS01`.
2. Confirm that Sysmon records process-creation telemetry.
3. Verify that Elastic Agent forwards the event.
4. Search for the event in Kibana Discover.
5. Validate the relevant fields and command-line arguments.
6. Test and refine the KQL detection logic.
7. Document the results and investigation workflow.

## Troubleshooting and Lessons Learned

During testing, highly specific KQL searches initially returned no results. The query was reduced to a broader baseline search for PowerShell process-creation events before command-line conditions were applied individually.

This demonstrated an important detection-engineering principle: validate the underlying telemetry and field mappings before troubleshooting the complete detection rule.

## Planned Improvements

* Add screenshots showing successful query results
* Document each detection rule separately
* Configure alert severity and risk scores
* Add false-positive considerations
* Expand testing with additional PowerShell techniques
* Create investigation and response guidance
