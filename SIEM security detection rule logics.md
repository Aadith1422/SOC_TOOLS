
---

# 🔐 SIEM Security Detection Rules 

---

## 1 Brute Force Login Attack

**Attack Type:** Brute Force
**Log Sources:** Active Directory, VPN, SSH logs

**Detection Logic:**

* Monitor authentication failure events
* Group by `source_ip` or `username`
* Count failed attempts ≥ 5 within 5 minutes

**Alert Criteria:**

* Threshold exceeded
* No successful login yet

**Severity:** Medium

**Purpose:**
Detect password guessing attempts before account compromise.

**Tuning Notes:**

* Exclude IT/admin IP ranges
* Raise threshold during business hours

---

## 2 Successful Login After Brute Force

**Attack Type:** Account Takeover
**Log Sources:** Active Directory, VPN

**Detection Logic:**

* ≥5 failed logins
* Followed by a successful login
* Same IP or same user
* Within 10 minutes

**Alert Criteria:**

* Failure → success sequence detected

**Severity:** High

**Purpose:**
Detect compromised credentials after brute-force success.

---

## 3 Password Spraying Attack

**Attack Type:** Credential Attack
**Log Sources:** Active Directory

**Detection Logic:**

* Same password attempt
* Across ≥10 different users
* From same IP
* Within 15 minutes

**Alert Criteria:**

* Multiple users targeted

**Severity:** High

**Purpose:**
Detect low-and-slow password spraying attacks.

---

## 4 Phishing Email Delivered

**Attack Type:** Phishing
**Log Sources:** Email Gateway

**Detection Logic:**

* Email marked as suspicious/phishing
* Delivery action = ALLOW
* Sender domain newly registered

**Alert Criteria:**

* High-risk email delivered to inbox

**Severity:** Medium

**Purpose:**
Detect phishing bypassing email filters.

---

## 5 Phishing Link Clicked

**Attack Type:** Phishing / Initial Access
**Log Sources:** Email Gateway + Proxy

**Detection Logic:**

* User clicks link from email
* URL reputation = malicious
* First-time domain seen

**Alert Criteria:**

* User interaction confirmed

**Severity:** High

**Purpose:**
Identify phishing victims immediately.

---

## 6 Malicious Email Attachment Opened

**Attack Type:** Malware Delivery
**Log Sources:** Email Gateway, Endpoint

**Detection Logic:**

* Attachment opened
* File hash matches threat intel
* Execution observed on endpoint

**Alert Criteria:**

* Malware confirmed

**Severity:** Critical

**Purpose:**
Detect malware delivered via phishing.

---

## 7 Suspicious PowerShell Execution

**Attack Type:** Malware / Living-off-the-Land
**Log Sources:** Sysmon / EDR

**Detection Logic:**

* Process = `powershell.exe`
* Command line contains encoded or obfuscated content
* Parent process = Office or browser

**Alert Criteria:**

* Encoded PowerShell detected

**Severity:** High

**Purpose:**
Detect fileless malware execution.

---

## 8 Malware Binary Execution

**Attack Type:** Malware
**Log Sources:** EDR

**Detection Logic:**

* Executed file hash matches known malware
* OR unsigned binary from temp directory

**Alert Criteria:**

* Malware execution confirmed

**Severity:** Critical

**Purpose:**
Stop malware at execution stage.

---

## 9 Command & Control (C2) Communication

**Attack Type:** Malware C2
**Log Sources:** Firewall, DNS

**Detection Logic:**

* Outbound connection
* Destination IP/domain flagged malicious
* Unusual port or beaconing pattern

**Alert Criteria:**

* Threat intel match

**Severity:** Critical

**Purpose:**
Detect active attacker control.

---

## 10 DNS Tunneling Detection

**Attack Type:** Data Exfiltration
**Log Sources:** DNS Logs

**Detection Logic:**

* Long, random-looking domain names
* High DNS query frequency
* Low TTL values

**Alert Criteria:**

* Abnormal DNS behavior

**Severity:** High

**Purpose:**
Detect covert data exfiltration channels.

---

## 11 Network Port Scanning

**Attack Type:** Reconnaissance
**Log Sources:** Firewall

**Detection Logic:**

* Same IP connects to ≥20 ports
* Within 1 minute

**Alert Criteria:**

* Rapid multi-port access

**Severity:** Medium

**Purpose:**
Detect pre-attack reconnaissance.

---

## 12 Unauthorized Admin Group Addition

**Attack Type:** Privilege Escalation
**Log Sources:** Active Directory

**Detection Logic:**

* User added to admin group
* Initiator not approved admin

**Alert Criteria:**

* Privilege change detected

**Severity:** Critical

**Purpose:**
Detect privilege abuse or escalation.

---

## 13 Privileged Login Outside Business Hours

**Attack Type:** Suspicious Admin Access
**Log Sources:** AD, VPN

**Detection Logic:**

* Admin account login
* Outside business hours
* From non-whitelisted IP

**Alert Criteria:**

* Off-hours privileged login

**Severity:** High

**Purpose:**
Detect unauthorized admin usage.

---

## 14 Unauthorized User Account Creation

**Attack Type:** Persistence
**Log Sources:** Active Directory

**Detection Logic:**

* New user account created
* Creator not HR/admin system

**Alert Criteria:**

* Suspicious account creation

**Severity:** High

**Purpose:**
Detect attacker persistence.

---

## 15 Lateral Movement via SMB

**Attack Type:** Lateral Movement
**Log Sources:** Endpoint, Network

**Detection Logic:**

* SMB connections to multiple hosts
* Same user/session
* Short time window

**Alert Criteria:**

* Internal spread detected

**Severity:** High

**Purpose:**
Detect internal compromise spread.

---

## 16 Ransomware File Encryption Activity

**Attack Type:** Ransomware
**Log Sources:** Endpoint

**Detection Logic:**

* Rapid file modifications
* Extension changes
* High entropy writes

**Alert Criteria:**

* Mass file activity

**Severity:** Critical

**Purpose:**
Stop ransomware early.

---

## 17 SQL Injection Attempt

**Attack Type:** Web Attack
**Log Sources:** Web Server, IDS

**Detection Logic:**

* SQL keywords in URL or POST data
* IDS signature match

**Alert Criteria:**

* Injection attempt detected

**Severity:** High

**Purpose:**
Protect backend databases.

---

## 18 Directory Traversal Attack

**Attack Type:** Web Exploitation
**Log Sources:** Web Server

**Detection Logic:**

* `../` patterns in requests
* Repeated attempts

**Alert Criteria:**

* Unauthorized file access attempt

**Severity:** Medium

**Purpose:**
Detect web server exploitation.

---

## 19 Impossible Travel Login

**Attack Type:** Credential Compromise
**Log Sources:** VPN, Cloud Auth

**Detection Logic:**

* Same user logs in from distant locations
* Time gap physically impossible

**Alert Criteria:**

* Geo-anomaly detected

**Severity:** High

**Purpose:**
Detect stolen credentials.

---

## 20 High-Value Transaction Fraud

**Attack Type:** Fraud
**Log Sources:** Application Logs

**Detection Logic:**

* Transaction value exceeds user baseline
* Occurs after login or password change

**Alert Criteria:**

* Behavioral anomaly

**Severity:** High

**Purpose:**
Prevent financial fraud.

---

## Final SOC Insight (Very Important)

> **Rules alone don’t stop attacks.
> Correlation, tuning, and analyst judgment do.**

---

###  Next (Highly Recommended)

I can:

* Convert these into **KQL / Splunk SPL / Wazuh rules**
* Put this into a **professional README or PDF**
* Map each rule to **MITRE ATT&CK**
* Turn this into a **full SOC project submission**
* Do a **mock SOC interview using these rules**

Just tell me what you want next — this is already **strong L2-level content**.
