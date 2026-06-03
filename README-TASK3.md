# Task 3: Basic Vulnerability Scan on Personal Computer
**Cyber Security Internship — ElevateLabs**

---

## Objective
To perform a basic vulnerability scan on a personal computer using free tools, identify common vulnerabilities, and document findings with remediation steps.

---

## Tools Used
- **Nessus Essentials** (by Tenable) — Free vulnerability scanner
- **Operating System:** Windows 10 (Version 10.0.26100)
- **Scan Target:** 127.0.0.1 (localhost — my own machine)

---

## Steps Performed

### 1. Installation
- Downloaded Nessus Essentials v10.12.0 for Windows x86_64 from [tenable.com](https://www.tenable.com/products/nessus/nessus-essentials)
- Registered for a free activation code via email
- Installed and accessed Nessus at `https://localhost:8834`
- Waited for plugins to finish compiling (~30 minutes)

### 2. Setting Up the Scan
- Selected **"Basic Network Scan"** template
- Set target as `127.0.0.1` (loopback address = my own PC)
- Launched the scan

### 3. Running the Scan
- **Scan Start:** 12:59 PM
- **Scan End:** 1:09 PM
- **Elapsed Time:** 10 minutes
- **Scanner:** Local Scanner
- **Severity Base:** CVSS v3.0

### 4. Results
- **Total Vulnerabilities Found:** 28
- **Severity Breakdown:**
  - 🔴 High: 1
  - 🟠 Medium: 1
  - 🟣 Mixed: 1
  - 🔵 Info: 25

---

## Vulnerability Report

### 1. 🔴 HIGH — Oracle TNS Listener Remote Poisoning
| Field | Details |
|---|---|
| **Severity** | High |
| **CVSS Score** | 7.3 |
| **Family** | Databases |
| **Count** | 1 |

**Description:**  
The Oracle TNS Listener service is running and vulnerable to a remote poisoning attack. An attacker could redirect database client connections to a malicious server, potentially intercepting sensitive data.

**Remediation:**  
- Disable Oracle TNS Listener if not actively used
- Apply the latest Oracle Critical Patch Update
- Restrict access to port 1521 using a firewall

---

### 2. 🟠 MEDIUM — SMB Signing Not Required
| Field | Details |
|---|---|
| **Severity** | Medium |
| **CVSS Score** | 5.3 |
| **Family** | Misc |
| **Count** | 1 |

**Description:**  
The SMB (Server Message Block) protocol is used for Windows file sharing. When signing is not enforced, an attacker on the same network can perform a man-in-the-middle attack and intercept or modify shared files.

**Remediation:**  
- Enable SMB signing via Windows Group Policy
- Navigate to: `Local Security Policy → Security Options → Microsoft network server: Digitally sign communications (always)` → Set to **Enabled**

---

### 3. 🟣 MIXED — SSL Multiple Issues (9 issues)
| Field | Details |
|---|---|
| **Severity** | Mixed |
| **Family** | General |
| **Count** | 9 |

**Description:**  
Multiple SSL/TLS configuration issues were found including use of weak cipher suites, outdated protocol versions, and self-signed certificates.

**Remediation:**  
- Disable SSL 2.0 and SSL 3.0
- Use TLS 1.2 or TLS 1.3 only
- Replace self-signed certificates where applicable

---

### 4. 🔵 INFO — Notable Informational Findings

| Name | Family | Count |
|---|---|---|
| TLS Multiple Issues | General | 5 |
| SMB Multiple Issues | Windows | 5 |
| HTTP Multiple Issues | Web Servers | 2 |
| Netstat Portscanner (SSH) | Port Scanners | 24 |
| DCE Services Enumeration | Windows | 8 |
| Service Detection | Service Detection | 3 |
| Remote Services Not Using Encryption | General | 2 |
| TLS Version 1.2 Protocol Detection | Service Detection | 2 |

> **Note:** Informational findings are not direct vulnerabilities but highlight services and open ports that could be potential attack surfaces.

---

## Key Concepts Learned

### What is Vulnerability Scanning?
An automated process of checking a system against a database of known vulnerabilities to identify security weaknesses before attackers can exploit them.

### What is CVSS?
**Common Vulnerability Scoring System** — A standardized scoring system (0–10) to rate the severity of vulnerabilities:
- **9.0–10.0** → Critical 🔴
- **7.0–8.9** → High 🟠
- **4.0–6.9** → Medium 🟡
- **0.1–3.9** → Low 🟢
- **0** → Info 🔵

### Vulnerability Scanning vs Penetration Testing
| Vulnerability Scanning | Penetration Testing |
|---|---|
| Automated | Manual (human expert) |
| Finds weaknesses | Actively exploits weaknesses |
| Non-invasive | Can cause disruption |
| Faster | Time-consuming |
| Surface-level | Deep dive |

### What is a False Positive?
When a scanner reports a vulnerability that doesn't actually exist on the system. Always verify findings manually before applying fixes.

### How Often Should Scans Be Performed?
- **Monthly** for personal computers
- **Weekly** for business systems
- **After every major update or configuration change**

### How to Prioritize Vulnerabilities?
1. Fix **Critical and High** severity first
2. Then **Medium**
3. Then **Low**
4. Review **Info** findings for awareness

---

## Conclusion
This task provided hands-on experience with vulnerability assessment using Nessus Essentials. The scan identified 28 vulnerabilities on my local machine, with the most critical being an Oracle TNS Listener issue (CVSS 7.3) and SMB Signing not being enforced (CVSS 5.3). These findings highlight the importance of regularly scanning systems and applying security patches and configurations proactively.

---

*Submitted as part of Cyber Security Internship — ElevateLabs*  
*Intern: Khushi Hegde*
