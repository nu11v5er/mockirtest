# mock incident 3
## **Mock Incident 3 – Insider Data Exfiltration**

**Case ID:** INC-2026-00126  
**Severity:** Medium  
**Status:** Under Investigation  
**Incident Type:** Insider Threat / Data Exfiltration  
**Date Opened:** 2026-06-06 10:30 UTC

### Timeline

| Timestamp (UTC) | Event |
| --- | --- |
| 2026-06-06 10:05:10 | DLP system flagged large copy of HR files to USB device. |
| 2026-06-06 10:07:42 | File transfer activity confirmed in endpoint logs. |
| 2026-06-06 10:15:33 | User accessed sensitive payroll spreadsheets outside of normal hours. |
| 2026-06-06 10:28:19 | USB device disconnected from endpoint. |
| 2026-06-06 10:30:00 | Incident case opened. |

### Affected Assets

*   **User:** lmartin@examplecorp.com
*   **Workstation:** HR-WS-154
*   **IP Address:** 10.24.22.54

### Indicators of Compromise (IOCs)

*   **USB Device Serial:** 5B4A-2C9D
*   **File Names:** Payroll\_2026\_Q1.xlsx, Employee\_Salaries.xlsx
*   **Suspicious Processes:** explorer.exe (unusual copy activity), cmd.exe /c copy

### Evidence Collected

*   Endpoint DLP logs
*   USB device mount logs
*   Windows Event IDs: 4663 (File Access), 4656 (Handle Open)
*   Timestamped file hashes of exfiltrated files

### Containment Actions

*   User workstation isolated
*   USB device confiscated
*   Account temporarily disabled
