#  SIEM Detection Rules – 


## 1 Brute Force Login Detection

**Rule Name:** Multiple Failed Login Attempts

**Objective:**  
Detect potential brute-force attacks targeting user authentication.

**Log Sources:**
- Windows Security Logs (Event ID 4625)
- VPN authentication logs
- Linux SSH logs

**Rule Logic:**
- Monitor login failure events
- Group by source IP
- Trigger alert if 5 or more failed attempts occur within 5 minutes

**Tuning:**
- Exclude IT/admin IP ranges
- Exclude service accounts
- Adjust thresholds during business hours

**Severity:** Medium (High if followed by success)

---

## 2 Port Scan Detection

**Rule Name:** Network Port Scanning Activity

**Objective:**  
Detect reconnaissance activity.

**Log Sources:**
- Firewall logs
- IDS/IPS
- Packetbeat / Zeek

**Rule Logic:**
- Count unique destination ports per source IP
- Alert if 20+ ports are scanned within 1 minute

**Tuning:**
- Whitelist vulnerability scanners
- Exclude monitoring tools

**Severity:** Medium

---

## 3 Suspicious PowerShell Execution

**Rule Name:** Suspicious PowerShell Command Execution

**Objective:**  
Detect malware or post-exploitation activity.

**Log Sources:**
- Sysmon
- EDR
- Windows Event Logs

**Rule Logic:**
- Process name is powershell.exe
- Encoded or obfuscated command detected
- Parent process is unusual (Office, browser, unknown)

**Tuning:**
- Exclude signed scripts
- Exclude known admin automation

**Severity:** High

---

## 4 Impossible Travel Detection

**Rule Name:** Impossible Travel Login Activity

**Objective:**  
Detect compromised user accounts.

**Log Sources:**
- VPN logs
- Cloud authentication logs
- Identity provider logs

**Rule Logic:**
- Same user logs in from distant locations
- Time gap is physically impossible

**Tuning:**
- Account for VPN usage
- Whitelist corporate VPN IPs

**Severity:** High

---

## 5 Suspicious File Download

**Rule Name:** Suspicious Executable Download

**Objective:**  
Detect potential malware delivery.

**Log Sources:**
- Proxy logs
- Web gateway logs
- EDR telemetry

**Rule Logic:**
- File extension: .exe, .js, .bat, .ps1
- Downloaded from low-reputation or new domain

**Tuning:**
- Whitelist trusted vendors
- Use threat intelligence scores

**Severity:** High

---

##  Notes
- Rules are behavior-based
- Continuous tuning is mandatory
- Document changes after every update

**Author:** SOC Analyst – Learning Project