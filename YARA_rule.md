#  YARA Rule – Detect Encoded PowerShell Malware



The rule focuses on identifying **behavioral patterns** rather than relying on static file hashes, making it effective against multiple malware variants.

---

##  Attack Technique Covered
- Malware Execution
- Fileless / Living-off-the-Land Attacks
- Obfuscated PowerShell Payloads

---

##  Sample YARA Rule

```yara
rule Encoded_PowerShell_Malware
{
    meta:
        description = "Detects PowerShell-based malware using encoded commands"
        author = "SOC Analyst"
        severity = "High"
        date = "2025-02-15"

    strings:
        $ps1 = "powershell.exe" nocase
        $ps2 = "-enc" nocase
        $ps3 = "Invoke-Expression" nocase

    condition:
        uint16(0) == 0x5A4D and
        filesize < 500KB and
        2 of ($ps*)
}
```

---

##  Rule Explanation

### 1 Meta Section
The `meta` section provides descriptive information about the rule such as description, author, and severity.  
This helps SOC analysts with documentation and reporting.

---

### 2 Strings Section
The strings represent common indicators used by PowerShell-based malware:
- `powershell.exe` – PowerShell execution
- `-enc` – Encoded PowerShell command
- `Invoke-Expression` – Executes malicious code

The `nocase` modifier ensures case-insensitive matching.

---

### 3 Condition Section
The condition defines when the rule triggers:

- `uint16(0) == 0x5A4D`  
  Confirms the file is a Windows executable (PE file)

- `filesize < 500KB`  
  Focuses on small malware droppers

- `2 of ($ps*)`  
  Requires multiple malicious indicators to reduce false positives

---

##  Why This Rule Is Effective
- Detects behavior-based malware patterns
- Works even if malware is recompiled
- Reduces false positives through contextual checks

---

## 🧪 SOC Use Case
1. A suspicious attachment is downloaded  
2. YARA scans the file  
3. Encoded PowerShell behavior is detected  
4. The file is quarantined  
5. SOC analysts investigate and respond  

---

