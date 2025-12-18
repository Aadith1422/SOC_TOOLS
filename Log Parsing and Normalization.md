
---

# 📘 **Document: How Logs Are Parsed and Normalized Before Ingestion**


![Image](https://last9.ghost.io/content/images/2025/02/key.png?utm_source=chatgpt.com)

---

## **1. Introduction**

Before logs enter a SIEM or security analytics platform, they must be **parsed and normalized**.
Different devices—firewalls, servers, endpoints, cloud systems—generate logs in different formats.
To make them usable for correlation, alerting, and searching, SIEM systems convert them into a **standardized structure**.

This document explains how that process works.

---

# -----------------------------------------------------

#  **2. What Is Log Parsing?**

### **Definition:**

**Parsing** is the process of breaking raw log messages into meaningful fields.

### Example: Raw Firewall Log

```
Feb 10 12:45:22 firewall01 TRAFFIC: action=deny src=192.168.1.20 dst=185.92.221.34 proto=TCP dst_port=443
```

### After Parsing:

| Field     | Value           |
| --------- | --------------- |
| timestamp | Feb 10 12:45:22 |
| device    | firewall01      |
| action    | deny            |
| src_ip    | 192.168.1.20    |
| dst_ip    | 185.92.221.34   |
| protocol  | TCP             |
| dst_port  | 443             |

Parsing converts unstructured logs into structured data.

---

# -----------------------------------------------------

#  **3. Parsing Techniques**

### ✔ **1. Regex (Regular Expressions)**

Matches text patterns to extract fields.

### ✔ **2. Grok Patterns (ELK Stack)**

Pre-built parsing templates for common log types.

### ✔ **3. Field Delimiter Parsing**

Splits text using characters like commas, spaces, or pipes.

### ✔ **4. Vendor-Specific Parsing Engines**

* Splunk Extractors
* Wazuh Decoders
* QRadar DSMs
* ArcSight SmartConnectors

### ✔ **5. JSON Parsing**

Modern logs often arrive in JSON format → easier to parse.

---

# -----------------------------------------------------

# **4. What Is Log Normalization?**

### **Definition:**

**Normalization** converts parsed log fields into a **common schema** shared by all log sources.

Different devices use different field names.
Normalization maps these to consistent SIEM field names.

### Example

| Raw Field from Device | Normalized SIEM Field |
| --------------------- | --------------------- |
| src                   | source.ip             |
| dst                   | destination.ip        |
| suser                 | user.name             |
| eventCode             | event.id              |
| action                | outcome               |

This makes correlation possible across systems.

---

# -----------------------------------------------------

#  **5. Why Normalization is Critical**

Normalization enables:

* ✔ Consistent queries across all data
* ✔ Cross-device correlation rules
* ✔ Unified dashboards
* ✔ Machine learning use cases
* ✔ Threat detection accuracy

Example query without normalization:

```
src_ip OR source OR source_address OR ip.src
```

After normalization:

```
source.ip = 192.168.1.20
```

Much simpler and reliable.

---

# -----------------------------------------------------

#  **6. Steps in Parsing & Normalization Pipeline**

![Image](https://substackcdn.com/image/fetch/w_1456%2Cc_limit%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5244cbee-8937-468d-b1b6-758cbcafbc75_1920x1080.png?utm_source=chatgpt.com)

![Image](https://d2908q01vomqb2.cloudfront.net/b6692ea5df920cad691c20319a6fffd7a4a766b8/2020/07/27/NormalizeDataElasticsearch2.png?utm_source=chatgpt.com)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AI33Wslma4CInN4T8?utm_source=chatgpt.com)

### **Step 1 — Receive Raw Logs**

Logs arrive via:

* Syslog
* Agents
* API integration
* File ingestion
* Cloud connectors

### **Step 2 — Identify Log Type**

SIEM checks:

* Device IP
* Message format
* Header
* Log signature

### **Step 3 — Apply Parser/Decoder**

Extract fields using:

* Regex
* Predefined patterns
* Vendor mappings

### **Step 4 — Normalize Fields**

Map fields to SIEM standard schema:

* source.ip
* destination.port
* event.action
* user.name
* threat.indicator.*

### **Step 5 — Enrich Data (Optional)**

Add context using:

* Threat intelligence
* GeoIP data
* Asset classification
* User identity databases

### **Step 6 — Forward to Indexer / SIEM Storage**

Normalized logs enter SIEM for:

* Detection
* Correlation
* Dashboards
* Long-term storage

---

# -----------------------------------------------------

#  **7. Examples of Parsing & Normalization for Different Log Sources**

---

## **A. Firewall Log**

### Raw Log:

```
action=deny src=10.1.5.10 dst=203.0.113.55 sport=5154 dport=443
```

### Normalized:

```
event.action: deny
source.ip: 10.1.5.10
destination.ip: 203.0.113.55
source.port: 5154
destination.port: 443
event.category: network
```

---

## **B. Endpoint Log (Windows Event ID 4688)**

### Raw Log:

```
New Process: powershell.exe CommandLine: powershell -enc JABxAG0...
```

### Normalized:

```
process.name: powershell.exe
process.command_line: powershell -enc JABxAG0...
user.name: user1
event.category: process
event.type: start
```

---

## **C. Server Log (Linux Auth Log)**

### Raw Log:

```
sshd[2340]: Failed password for root from 192.168.2.10
```

### Normalized:

```
event.action: login_failed
user.name: root
source.ip: 192.168.2.10
event.category: authentication
```

---

# -----------------------------------------------------

#  **8. SIEM Platforms That Perform Parsing & Normalization**

### ✔ ELK Stack (Logstash, Beats, Elasticsearch)

Uses Grok, Elastic Common Schema (ECS)

### ✔ Splunk

Uses field extractors, CIM (Common Information Model)

### ✔ Wazuh

Uses decoders/rules + mapping templates

### ✔ QRadar

Uses DSMs (Device Support Modules)

### ✔ ArcSight

Uses SmartConnectors

Each platform transforms logs into a unified format.

---

# -----------------------------------------------------

#  **9. Why This Matters to SOC Analysts**

Parsed & normalized logs allow the SOC to:

* Correlate events across firewalls, endpoints, and servers
* Detect threats quickly
* Write universal detection rules
* Build consistent dashboards
* Perform forensic analysis

Without normalization, SIEM detection would be:

* Slow
* Inaccurate
* Unreliable

Normalization = **foundation of good detection engineering**.

---

