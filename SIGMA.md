While YARA rules are designed to inspect **files** (static analysis), Sigma rules are designed to inspect **logs** (events).

Think of Sigma as the "universal translator" for SIEM queries. You write a rule in Sigma once, and it can be converted to work in OpenSearch, Splunk, Graylog, or Wazuh.

Here is a classic Sigma rule to detect an attacker trying to cover their tracks by **clearing Windows Event Logs**.

### The Sigma Rule

```yaml
title: Windows Security Log Cleared
id: 7f43c49c-3088-4332-9396-5b430b35548d
status: stable
description: Detects the clearing of the Windows Security Event Log, a common tactic used by attackers to hide activity.
author: SOC Lab Admin
date: 2023-10-27
level: high

logsource:
    product: windows
    service: security

detection:
    selection:
        EventID: 1102
    
    condition: selection

falsepositives:
    - Administrative maintenance (rare, usually scheduled)

tags:
    - attack.defense_evasion
    - attack.t1070.001

```

---

### Detailed Explanation

A Sigma rule is written in **YAML** and has three critical sections: **Logsource**, **Detection**, and **Tags**.

#### 1. Logsource (Where to look)

```yaml
logsource:
    product: windows
    service: security

```

* **Context:** This tells your SIEM *which* index or log file to search.
* **Mapping:** In your stack (OpenSearch), this ensures the query only runs against your Windows Security logs, saving processing power by ignoring Linux logs or Firewall logs.

#### 2. Detection (What to look for)

```yaml
detection:
    selection:
        EventID: 1102
    condition: selection

```

* **Selection:** This defines the specific field and value we want.
* **EventID 1102:** In the Windows ecosystem, Event ID **1102** is hardcoded to mean "The audit log was cleared." It is generated specifically when an administrator (or hacker) right-clicks "Clear Log" in Event Viewer or runs a PowerShell command to wipe it.
* **Condition:** This is simple boolean logic. Here, `selection` just means "If you see the selection above, trigger." You could have complex logic like `selection1 and not selection2`.

#### 3. Tags (The Classification)

```yaml
tags:
    - attack.defense_evasion
    - attack.t1070.001

```

* **MITRE ATT&CK:** This is crucial for a modern SOC.
* **`attack.defense_evasion`:** The tactic (High-level goal).
* **`attack.t1070.001`:** The specific technique ID (Clear Windows Event Logs).
* **Why it matters:** In your **TheHive** case management system, this tag allows you to generate reports like "How many *Defense Evasion* attempts did we see this month?"

