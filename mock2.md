# mock incident 3
## **Mock Incident 1 – Phishing / Credential Harvesting**

**Case ID:** INC-2026-00125  
**Severity:** High  
**Status:** Under Investigation  
**Incident Type:** Phishing / Compromised Credentials  
**Date Opened:** 2026-06-06 09:12 UTC

### Timeline

| Timestamp (UTC) | Event |
| --- | --- |
| 2026-06-06 08:45:22 | User reports suspicious email requesting password reset. |
| 2026-06-06 08:47:10 | Email header analysis shows external SPF fail. |
| 2026-06-06 08:50:33 | User clicks link and submits credentials on phishing page. |
| 2026-06-06 08:55:44 | Unauthorized login detected from foreign IP. |
| 2026-06-06 09:00:12 | MFA challenge triggered for affected account. |
| 2026-06-06 09:12:00 | Incident case opened. |

### Affected Assets

*   **User:** rthomas@examplecorp.com
*   **Workstation:** HR-WS-207
*   **IP Address:** 10.24.33.198
*   **Email:** rthomas@examplecorp.com

### Indicators of Compromise (IOCs)

*   **Phishing Domain:** secure-login-update\[.\]net
*   **Malicious IPs:** 203.0.113.55, 198.51.100.77
*   **Suspicious URL:** hxxps://secure-login-update\[.\]net/login?user=rthomas

### Evidence Collected

*   Email headers (SPF fail, DKIM fail)
*   Web proxy logs showing HTTP POST to phishing domain
*   Authentication logs showing foreign login attempts
*   Screenshot of phishing landing page

### Containment Actions

*   Account disabled at 09:15 UTC
*   Password reset initiated
*   Email filter updated to block domain
