#  SOC Log Sources and Detectable Attacks

---

| **Log Source** | **What It Monitors** | **Types of Attacks Detected** | **Example Indicators** |
|---------------|---------------------|-------------------------------|------------------------|
| **Firewall Logs** | Network traffic (allowed/blocked) | • Port scanning <br> • Brute-force attempts (SSH/RDP) <br> • Unauthorized access <br> • C2 communication <br> • Data exfiltration | Multiple denied connections to port 22 from same IP |
| **IDS / IPS Logs** | Known attack signatures | • SQL Injection <br> • XSS <br> • Remote Code Execution <br> • Exploit attempts <br> • Malware traffic | “SQL Injection Attempt Detected” |
| **Active Directory (AD) Logs** | Authentication & authorization | • Brute force <br> • Password spraying <br> • Account takeover <br> • Privilege escalation <br> • Insider threats | Event ID 4625 followed by 4624 |
| **Web Server Logs** | HTTP requests & responses | • Web brute force <br> • Admin page probing <br> • Directory traversal <br> • Bot & scraping attacks <br> • Web exploitation | Repeated `/admin/login.php` requests |
| **VPN Logs** | Remote access activity | • Credential theft <br> • Impossible travel <br> • Unauthorized remote access <br> • Off-hours access | Successful login from new country |
| **Endpoint Logs (EDR / Sysmon)** | Process, file, network activity | • Malware execution <br> • Ransomware <br> • Credential dumping <br> • Lateral movement <br> • Living-off-the-land attacks | `winword.exe → powershell.exe` |
| **Email / Gateway Logs** | Email flow & attachments | • Phishing <br> • Malware delivery <br> • Spoofing <br> • Business Email Compromise (BEC) | Malicious attachment clicked |
| **Application Logs** | User actions & transactions | • Fraud <br> • Account takeover <br> • Privilege abuse <br> • Insider threats | Password change + high-value transaction |
| **DNS Logs** | Domain name resolution | • Malware beaconing <br> • DGA-based malware <br> • Phishing domains <br> • C2 communication | Repeated queries to suspicious domain |
| **Cloud Audit Logs (AWS / Azure / GCP)** | Cloud resource & IAM activity | • Cloud account takeover <br> • Unauthorized API calls <br> • Privilege escalation <br> • Data exposure | New admin role assigned unexpectedly |

---

