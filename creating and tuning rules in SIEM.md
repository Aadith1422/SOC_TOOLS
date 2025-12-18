

## 1. Brute Force Login Detection (Windows / Linux)

### Rule Logic
Detect when a single IP or user triggers multiple failed authentication attempts in a short period.

```
IF count(EventID=4625 OR "Failed password") > 10
WITHIN 5 minutes
GROUP BY source.ip OR user.name
THEN raise "Possible Brute Force Attack"
```

### Purpose
Brute-force attacks try many passwords rapidly.

### Tuning Tips
- Whitelist scanners
- Ignore noisy service accounts

---

## 2. Port Scan Detection (Vertical Scan)

### Rule Logic
```
IF count_distinct(destination.port) > 20
WITHIN 1 minute
GROUP BY source.ip
```

### Purpose
Identifies scanning behavior.

---

## 3. Suspicious PowerShell Execution (Encoded Command)

### Rule Logic
```
IF process.name = "powershell.exe"
AND process.command_line CONTAINS "-enc"
```

### Purpose
Encoded PowerShell is common in malware.

---

## 4. Outbound Connection to Known Malicious IP

### Rule Logic
```
IF destination.ip IN threat_intel.malicious_ip_list
```

### Purpose
Detects C2 communication.

---

## 5. Privilege Escalation Attempt (Domain Admin Modification)

### Rule Logic
```
IF EventID = 4728
AND target.group = "Domain Admins"
```

### Purpose
Critical indicator of lateral movement and escalation.