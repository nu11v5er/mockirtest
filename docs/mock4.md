# mock incident 4
## **Mock Incident 4 – Ransomware / Malware Outbreak**

**Case ID:** INC-2026-00127  
**Severity:** Critical  
**Status:** Under Investigation  
**Incident Type:** Ransomware / Malware Infection  
**Date Opened:** 2026-06-06 13:45 UTC

### Timeline

| Timestamp (UTC) | Event |
| --- | --- |
| 2026-06-06 13:20:14 | Endpoint EDR detected suspicious encryption process. |
| 2026-06-06 13:22:57 | Multiple network shares flagged for mass file modifications. |
| 2026-06-06 13:25:30 | Ransom note created on desktop of affected workstation. |
| 2026-06-06 13:35:12 | Antivirus quarantined initial payload. |
| 2026-06-06 13:45:00 | Incident case opened. |

### Affected Assets

*   **Hostname:** FIN-WS-044
*   **User:** tnguyen@examplecorp.com
*   **IP Address:** 10.24.40.77
*   **Operating System:** Windows 11 Enterprise

### Indicators of Compromise (IOCs)

*   **Malware Hashes (SHA256):**
    *   e4f7d2a3b6c8d1e9f0a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4
*   **Suspicious Process Names:** crypto\_lock.exe, powershell.exe -enc \<redacted\>
*   **Network Indicators:** 192.168.200.15:445 outbound to 45.32.12.7

### Evidence Collected

*   EDR alerts for process creation and file encryption
*   Windows Event Logs: 4688, 5140
*   Network flow logs showing SMB traffic to unknown IP
*   Screenshots of ransom note

### Containment Actions

*   Endpoint isolated
*   Network shares disconnected
*   Firewall block applied to external IP
