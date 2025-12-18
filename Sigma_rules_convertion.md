Below is a **clean, technical documentation-style explanation** of **how Sigma rules are converted for different SIEM platforms**, written in a way suitable for **SOC documentation, reports, or study notes**.

---

# Sigma Rule Conversion for Different SIEM Platforms

## 1. What Sigma Conversion Means

Sigma rules are written in a **generic, SIEM-agnostic YAML format**.
They **cannot run directly** inside a SIEM.

Instead, Sigma rules must be **translated (converted)** into the **native query or rule language** of the target SIEM platform.

This conversion ensures that:

* The same detection logic works across different tools
* SOC teams avoid rewriting detections from scratch
* Detection engineering becomes portable and scalable

---

## 2. Why Conversion Is Necessary

Each SIEM uses its **own query language and data model**:

| SIEM                 | Native Language                  |
| -------------------- | -------------------------------- |
| Splunk               | SPL (Search Processing Language) |
| Elastic / OpenSearch | KQL / Lucene                     |
| Microsoft Sentinel   | KQL                              |
| QRadar               | AQL                              |
| ArcSight             | EQL                              |
| Chronicle            | YARA-L                           |
| Graylog              | Lucene-based syntax              |

Sigma provides **logic**, not execution.

Conversion maps:

* Fields → SIEM field names
* Operators → SIEM syntax
* Conditions → SIEM query structure

---

## 3. Sigma Conversion Architecture (High-Level)

**Detection Logic Flow**

```
Sigma Rule (YAML)
        ↓
Sigma Converter (Backend)
        ↓
SIEM-Specific Query / Rule
```

The converter understands:

* Sigma rule structure
* SIEM query language
* Field mappings

---

## 4. The Sigma Conversion Toolchain

### 4.1 Sigma CLI (sigmac)

The **primary tool** used for conversion is:

```
sigmac
```

It is a command-line tool that:

* Reads Sigma YAML rules
* Outputs SIEM-specific detection syntax

---

## 5. Conversion Components Explained

### 5.1 Sigma Rule (Input)

A Sigma rule contains:

* `logsource` → event source
* `detection` → logic
* `condition` → execution logic

This is the **source of truth**.

---

### 5.2 Backend (Target SIEM)

The backend defines:

* Output format
* Query language
* Rule structure

Examples:

* `splunk`
* `es-qs`
* `sentinel`
* `qradar`

---

### 5.3 Configuration Files

Conversion relies on **config files** to map fields.

Example:

* `winlogbeat.yml`
* `sysmon.yml`

These map:

```
Sigma field → SIEM field
```

Example:

```
process_name → process.name
```

---

## 6. Conversion Process Step-by-Step

### Step 1: Choose Target SIEM

Identify where the rule will run:

* Splunk
* Elastic
* Sentinel
* QRadar

---

### Step 2: Select Backend

Each SIEM has a backend.

Example:

```
splunk
es-qs
sentinel
```

---

### Step 3: Apply Field Mapping

Sigma fields are normalized.
SIEM fields are not.

Mappings ensure compatibility.

---

### Step 4: Generate Output Query

The converter outputs:

* A search query
* A detection rule
* Or a correlation logic (depending on SIEM)

---

## 7. Example Conversions

### 7.1 Sigma → Splunk (SPL)

**Sigma Logic**

* Detect PowerShell execution
* Match command line patterns

**Converted Output**

```
index=windows process_name="powershell.exe"
| search CommandLine="*-enc*"
```

Splunk-specific features added:

* Index reference
* Pipe-based filtering

---

### 7.2 Sigma → Elastic / OpenSearch (KQL)

**Converted Output**

```
process.name:"powershell.exe" and process.command_line:*"-enc"*
```

Elastic-specific:

* Field-based filtering
* Boolean logic

---

### 7.3 Sigma → Microsoft Sentinel (KQL)

**Converted Output**

```
SecurityEvent
| where ProcessName == "powershell.exe"
| where CommandLine contains "-enc"
```

Sentinel-specific:

* Table-based queries
* Pipe operators
* Time-based execution handled separately

---

### 7.4 Sigma → QRadar (AQL)

**Converted Output**

```
SELECT * FROM events
WHERE ProcessName = 'powershell.exe'
AND CommandLine LIKE '%-enc%'
```

QRadar-specific:

* SQL-like syntax
* Event table querying

---

