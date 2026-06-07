# Incident Record 5

**Case ID:** INC-2026-00128
**Title:** Suspicious Activity on Finance Department Workstation
**Severity:** High
**Priority:** P2
**Status:** Active Investigation
**Incident Type:** Unauthorized Access / Malware Activity
**Date Opened:** 2026-06-06 14:42 UTC
**Case Owner:** SOC Tier 2

---

## Incident Summary

Multiple security alerts were generated involving a finance department workstation. Activity included suspicious authentication events, execution of unsigned binaries, creation of scheduled tasks, and outbound communications to external infrastructure not previously observed within the environment.

---

## Timeline

| Timestamp (UTC)     | Event                                                           |
| ------------------- | --------------------------------------------------------------- |
| 2026-06-06 13:07:14 | Successful VPN login for user account from external IP address. |
| 2026-06-06 13:08:33 | User authenticated to workstation FIN-WS-081.                   |
| 2026-06-06 13:11:56 | File downloaded to Downloads directory.                         |
| 2026-06-06 13:13:04 | Executable launched from user profile.                          |
| 2026-06-06 13:13:18 | Child process spawned PowerShell instance.                      |
| 2026-06-06 13:14:21 | Scheduled task created.                                         |
| 2026-06-06 13:15:42 | DNS request made to previously unseen domain.                   |
| 2026-06-06 13:16:03 | HTTPS connection established to external IP.                    |
| 2026-06-06 13:17:47 | Archive file created in temporary directory.                    |
| 2026-06-06 13:18:10 | Network transfer volume exceeded baseline threshold.            |
| 2026-06-06 13:19:55 | Additional authentication event observed from same account.     |
| 2026-06-06 13:22:41 | Endpoint detection alert generated.                             |
| 2026-06-06 13:29:17 | Network monitoring alert generated.                             |
| 2026-06-06 14:42:00 | Incident case created.                                          |

---

## Affected Assets

### Primary Endpoint

* Hostname: FIN-WS-081
* Asset ID: AST-004482
* Operating System: Windows 11 Enterprise
* Internal IP: 10.20.18.81
* MAC Address: 4C-44-5B-82-1A-7F
* Logged-In User: [cjohnson@examplecorp.com](mailto:cjohnson@examplecorp.com)

### User Account

* Username: cjohnson
* Department: Finance
* Email: [cjohnson@examplecorp.com](mailto:cjohnson@examplecorp.com)
* Role: Financial Analyst

### Additional Systems Referenced

* FILE-SRV-02
* DC-01
* VPN-GW-01

---

## Indicators of Compromise (IOCs)

### IP Addresses

* 185.212.70.91
* 45.146.164.88
* 91.243.44.117

### Domains

* portal-documentcenter[.]com
* secure-docsportal[.]net
* sync-notificationservice[.]org

### URLs

* hxxps://portal-documentcenter[.]com/client/update.zip
* hxxps://secure-docsportal[.]net/api/v2/checkin
* hxxp://91.243.44.117/gate

### SHA256 Hashes

* 3e2e06f2b4d4c28b76a31b4fa15c9dc9f602a841f32e57c7cf6bfc6f79f4a1b2
* c5fd6db77c9c0c8cbfa41c8db47c42f4c16ab7f4ea96fd9f0d48b2b4a19f22d6
* a9f2719f50b5a6d7124d9913f35d1fba4b80c9b69f30e61f5d7ec7f7d2389a45

### File Names

* update.zip
* invoice_review.exe
* cache.dat
* report_archive.zip

---

## Process Activity

| Timestamp (UTC) | Process            |
| --------------- | ------------------ |
| 13:13:04        | invoice_review.exe |
| 13:13:18        | powershell.exe     |
| 13:13:24        | cmd.exe            |
| 13:14:21        | schtasks.exe       |
| 13:17:47        | 7z.exe             |
| 13:18:01        | chrome.exe         |

### Command Line Artifacts

```text
powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -EncodedCommand <redacted>

schtasks.exe /create /sc minute /mo 30 /tn "WindowsUpdateCheck" /tr "C:\Users\cjohnson\AppData\Local\invoice_review.exe"

cmd.exe /c whoami && ipconfig /all
```

---

## Network Observations

### DNS Requests

| Timestamp | Query                        |
| --------- | ---------------------------- |
| 13:15:42  | portal-documentcenter.com    |
| 13:16:11  | secure-docsportal.net        |
| 13:18:33  | sync-notificationservice.org |

### Connection Activity

| Source      | Destination   | Port | Protocol |
| ----------- | ------------- | ---- | -------- |
| 10.20.18.81 | 185.212.70.91 | 443  | HTTPS    |
| 10.20.18.81 | 45.146.164.88 | 8443 | TCP      |
| 10.20.18.81 | 91.243.44.117 | 80   | HTTP     |

### Data Transfer

| Timestamp | Direction | Volume |
| --------- | --------- | ------ |
| 13:17:58  | Outbound  | 118 MB |
| 13:18:10  | Outbound  | 243 MB |
| 13:18:44  | Outbound  | 91 MB  |

---

## Evidence Collected

### EDR

* Alert ID: EDR-46088
* Alert ID: EDR-46091
* Alert ID: EDR-46094

### SIEM

* Correlation Rule: Suspicious PowerShell Execution
* Correlation Rule: Rare External Destination
* Correlation Rule: New Scheduled Task Creation

### Event Logs

| Event ID | Description                           |
| -------- | ------------------------------------- |
| 4624     | Successful Logon                      |
| 4625     | Failed Logon                          |
| 4688     | Process Creation                      |
| 4698     | Scheduled Task Created                |
| 4104     | PowerShell Script Block Logging       |
| 5156     | Windows Filtering Platform Connection |

### File Locations

```text
C:\Users\cjohnson\Downloads\update.zip
C:\Users\cjohnson\AppData\Local\invoice_review.exe
C:\Users\cjohnson\AppData\Local\Temp\cache.dat
C:\ProgramData\WindowsUpdateCheck.log
```

### Collected Artifacts

* Memory Capture: MEM-FIN-081-06062026.mem
* Disk Image: IMG-FIN-081-06062026.E01
* Browser History Export: BH-FIN-081.csv
* Windows Security Log Export: SECLOG-081.evtx
* PowerShell Operational Log: PSLOG-081.evtx

---

## Notes

* Multiple alerts associated with the same endpoint.
* Scheduled task remained present at time of collection.
* External destinations not present in prior 30-day network baseline.
* User account observed authenticating to VPN gateway and workstation during incident window.
* Archive file present in temporary directory at time of evidence acquisition.

**Last Updated:** 2026-06-06 15:18 UTC
