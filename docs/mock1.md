# Mock Incident Report – Suspicious Network Activity

**Case ID:** INC-2026-00124  
**Severity:** Medium  
**Status:** Under Investigation  
**Incident Type:** Network Intrusion / Data Exfiltration  
**Date Opened:** 2026-06-05 11:05 UTC

## Incident Summary

Unusual outbound traffic detected from a workstation in the HR department to multiple external IP addresses. The traffic was flagged by the network monitoring system due to high volume and anomalous protocol usage.

## Timeline

| Timestamp (UTC) | Event |
| --- | --- |
| 2026-06-05 10:48:12 | IDS triggered on outbound traffic exceeding normal thresholds. |
| 2026-06-05 10:50:44 | Workstation HR-WS-112 flagged for connecting to TOR exit node. |
| 2026-06-05 10:52:37 | Data exfiltration attempt detected via FTP to unknown server. |
| 2026-06-05 10:55:05 | Network flow logs confirmed large data transfer. |
| 2026-06-05 11:00:29 | Endpoint scan shows presence of suspicious executable. |
| 2026-06-05 11:05:00 | Incident case opened. |

## Affected Assets

**Hostname:** HR-WS-112  
**User:** mwilliams@examplecorp.com  
**IP Address:** 10.24.22.101  
**Operating System:** Windows 10 Pro  
**MAC Address:** 00:1A:2B:3C:4D:5E

## Indicators of Compromise (IOCs)

### IP Addresses

*   185.62.44.21
*   198.51.100.44
*   45.77.23.91

### Domains

*   hrdata-upload\[.\]com
*   secure-transfer-service\[.\]net

### File Hashes

**SHA256**

*   a1b2c3d4e5f60718293a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5
*   9f8e7d6c5b4a3c2b1a0e9d8c7b6a5e4d3c2b1a0f9e8d7c6b5a4e3d2c1b0a9f8

### Suspicious Processes

*   data\_sync.exe
*   cmd.exe /c "powershell -nop -w hidden -enc \<redacted\>"

## Evidence Collected

### EDR Alerts

Alert ID: EDR-45912  
Detection: High-volume FTP transfer from workstation to external IP.

### Windows Event Logs

*   Event ID 4624 (Successful Logon)
*   Event ID 4688 (Process Creation)
*   Event ID 5140 (Network Share Access)

### Network Logs

*   FTP connection to 198.51.100.44:21
*   TLS connections to hrdata-upload\[.\]com:443

### File Evidence

Suspicious executable found at:  
`C:\Users\mwilliams\AppData\Local\Temp\data_sync.exe`

## Containment Actions

*   Endpoint quarantined at 11:08 UTC
*   User account disabled at 11:12 UTC
*   Firewall rules applied to block external IPs
*   Network monitoring increased on HR subnet

**Case Owner:** SOC Analyst - Tier 2  
**Last Updated:** 2026-06-05 11:30 UTC
