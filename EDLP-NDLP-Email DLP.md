
## **1. Introduction**

Data Loss Prevention (DLP) is a core security function designed to prevent unauthorized exposure, misuse, or transfer of sensitive data. Organizations implement multiple layers of DLP to secure **data at rest**, **data in motion**, and **data in use**.
This report summarizes three major DLP components: **Endpoint DLP (EDLP)**, **Network DLP (NDLP)**, and **Email DLP**.

---

## **2. Endpoint DLP (EDLP)**

**Focus:** Protects **data at rest and data in use** on endpoint devices (laptops, desktops, servers).

### **Key Functions**

* Discovers and classifies sensitive data stored on endpoints
* Monitors user actions (open, copy, print, rename, ZIP, delete)
* Blocks unauthorized transfers to USB, cloud apps, Bluetooth, etc.
* Enforces access control for sensitive files
* Encrypts or quarantines high-risk data
* Provides offline protection even without network connectivity

### **Objective**

Prevent insider threats, accidental leaks, and unauthorized access **directly at the device level**, where data is most vulnerable.

---

## **3. Network DLP (NDLP)**

**Focus:** Protects **data in motion** as it travels across the organization’s network.

### **Key Functions**

* Inspects network traffic using Deep Content Inspection (DCI)
* Monitors email protocols, web uploads, cloud traffic, FTP/SFTP, messaging services
* Decrypts SSL/TLS traffic for analysis
* Blocks outbound transmission of sensitive data
* Detects data exfiltration attempts via abnormal traffic patterns
* Enforces organization-wide data transfer policies

### **Objective**

Ensure confidential data does **not leave the organization** through the network, intentionally or accidentally.

---

## **4. Email DLP**

**Focus:** Secures **email communication channels**, one of the most common paths for data leaks.

### **Key Functions**

* Scans email body and attachments for sensitive content
* Blocks or quarantines messages violating data protection policies
* Ensures proper recipient validation (internal vs external)
* Enforces encryption for sensitive messages
* Detects compromised accounts sending sensitive data
* Logs detailed email activity for compliance and forensic use

### **Objective**

Prevent accidental or malicious data leakage via email and ensure secure communication.

---

## **5. Comparison Overview**

| Feature    | EDLP                                | NDLP                             | Email DLP                        |
| ---------- | ----------------------------------- | -------------------------------- | -------------------------------- |
| Protects   | Data at rest & in use               | Data in motion                   | Email communications             |
| Monitors   | Endpoint activity                   | Network traffic                  | Email body + attachments         |
| Blocks     | Local file actions, USB, cloud apps | Uploads, transfers, exfiltration | Unauthorized or sensitive emails |
| Focus Area | User devices                        | Network perimeter                | Email gateways & cloud mail      |

---

## **6. Conclusion**

A successful DLP strategy requires **multiple layers of protection**.

* **EDLP** secures data directly on endpoints,
* **NDLP** stops sensitive data from leaking through network channels, and
* **Email DLP** protects one of the highest-risk communication methods.


