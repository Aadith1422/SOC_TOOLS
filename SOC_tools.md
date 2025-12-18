
---

#  How SOC Tools Interact With Each Other

A SOC is **not one tool** — it’s an **ecosystem** where tools continuously exchange data to **detect, investigate, and respond** to security incidents.

---



### 1 Log Sources (Data Producers)

These are the **eyes and ears** of the SOC.

**Examples:**

* Endpoints (Windows, Linux, macOS)
* Network devices (Firewall, IDS/IPS, Router)
* Applications & Servers
* Cloud services (AWS, Azure, O365)

**What they send:**
 Logs, events, telemetry

 Logs flow into SIEM

---

### 2 SIEM – Security Information & Event Management

**Role:** Central brain of the SOC

**What SIEM does:**

* Collects logs from all sources
* Normalizes and parses data
* Correlates events across systems
* Triggers alerts based on rules

**Example interaction:**

```
Firewall detects port scan
+
EDR detects suspicious process
→ SIEM correlates both
→ High-confidence alert
```

 Alerts move to SOAR & Ticketing

---

### 3 SOAR – Security Orchestration, Automation & Response

**Role:** SOC automation engine

**What SOAR does:**

* Receives alerts from SIEM
* Runs playbooks (automated workflows)
* Enriches alerts with threat intelligence
* Executes response actions

**Example playbook:**

```
Alert → Check IP reputation → Isolate endpoint → Notify analyst
```

 Response actions sent to EDR / Firewall

---

### 4 EDR / XDR – Endpoint Detection & Response

**Role:** Endpoint visibility and action

**What EDR/XDR does:**

* Monitors processes, memory, file activity
* Detects malware and suspicious behavior
* Executes response commands from SOAR

**Example interaction:**

```
SOAR → EDR → Isolate compromised machine
```

 Investigation feedback to SIEM

---

### 5 Threat Intelligence Platform (TIP)

**Role:** Context provider

**What TIP does:**

* Provides IOC reputation (IP, hash, domain)
* Feeds intelligence into SIEM & SOAR
* Improves alert confidence

**Example:**

```
Unknown IP → TIP confirms C2 server → Severity raised
```

 Enrichment improves decision-making

---

### 6 Ticketing System

**Role:** Case management and documentation

**Examples:** ServiceNow, Jira, TheHive

**What it does:**

* Tracks incidents from open → close
* Assigns incidents to analysts
* Maintains audit trail

**Example:**

```
SIEM Alert → Ticket Created → Analyst Investigates → Ticket Closed
```

---



```
Logs → SIEM → Alert
             ↓
          SOAR
             ↓
     EDR / Firewall
             ↓
         Ticketing
```

---

##  Real-World Incident Example

**Phishing Email Incident**

1. Email gateway logs phishing attempt
2. User clicks malicious link
3. EDR detects suspicious process
4. SIEM correlates email + endpoint activity
5. SOAR runs playbook:

   * Block domain
   * Isolate endpoint
   * Reset user password
6. Ticket created and closed after validation

---
