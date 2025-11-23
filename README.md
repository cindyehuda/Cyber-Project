# 🛡️ SOC Incident Report
**Security Operations Center – Incident Documentation**
<img width="1064" height="325" alt="image" src="https://github.com/user-attachments/assets/89a27eb4-0b45-4ae5-b986-ef994215aca5" />

## 📌 1. Overview
Provide a short summary of the incident (2–3 sentences):
- What happened
- When it occurred
- Which system or asset was affected
- How the incident was detected


## 🕒 2. Timeline
| Time (UTC) | Event Description |
|------------|------------------|
| 12:03 | IDS alert triggered |
| 12:05 | Analyst validated abnormal activity |
| 12:10 | Investigation initiated |
| … | … |
![description](images/wireshark_to_git.png)

## 🎯 3. Detection
**Detection Source:** (IDS / SIEM / Firewall / Endpoint / Splunk / Cloud logs)  
**Alert Name:**  
**Severity:** (Low / Medium / High / Critical)  
**Category:** (Reconnaissance / Credential Access / Lateral Movement / Malware / Exfiltration / Web Attack, etc.)

## 🔍 4. Investigation Summary
Describe the investigative steps taken:
- Log review
- Correlation across multiple sources
- Packet analysis (pcap)
- Host-level inspection
- Searching for IOCs
- Checking authentication patterns
- Reviewing network behavior

## 📂 5. Evidence Collected
- Raw logs
- Splunk queries & results
- PCAP files
- Hash values
- Suspicious payloads
- Screenshots
- File artifacts
- User or process activity patterns

## 🧩 6. Technical Analysis

### 6.1 Attack Vector
Explain how the attacker attempted to execute the attack.

### 6.2 Indicators of Compromise (IOCs)
| Type | Value | Notes |
|------|-------|-------|
| IP Address | 192.168.10.25 | Suspected attacker host |
| File Hash | e99a... | Reverse shell payload |
| URL | /upload/reverse_proxy.php | Malicious upload attempt |
| User-Agent | ... | ... |

## 🌐 7. Affected Systems
List any impacted assets:
- Server names
- IP addresses
- Applications
- Services
- Containers / Docker images
- Cloud resources

## 📊 8. Log & Traffic Findings

### 8.1 Network Indicators
Summaries of suspicious traffic:
- Port scans (Nmap)
- Large volumes of SYN packets
- Reverse shell callbacks
- File upload attempts

### 8.2 Application Logs
- Failed logins
- Suspicious input parameters
- SQLi / LFI / RFI attempts
- Unauthorized file uploads

### 8.3 Splunk Queries Used
```
index=web_logs "reverse_proxy.php"
| stats count by src_ip, uri, user_agent
```

```
index=ids sourcetype=snort severity=high
| timechart count by signature
```

## 🔐 9. Containment Actions
Describe actions taken to stop the attack:
- Blocking attacker IP
- Disabling user accounts
- Stopping services
- Isolating endpoints
- Revoking credentials
- Restarting containers

## 🛠️ 10. Eradication & Recovery
- Removed malicious files
- Restored normal service operations
- Re-imaged machines (if required)
- Patched vulnerable components
- Updated firewall rules
- Validated system integrity

## 📘 11. Root Cause Analysis (RCA)
Explain what allowed the incident to occur:
- Misconfiguration
- Missing patch
- Weak password
- Insecure upload handler
- Firewall gap
- Lack of input validation

## 🛡️ 12. Recommendations & Hardening
- Apply security patches
- Enable WAF rules
- Restrict file upload types
- Enforce strong authentication
- Implement rate limiting
- Enable IDS signatures
- Improve logging and alerting
- Perform regular attack simulations

## ✔️ 13. Final Status
**Incident Status:** Closed / Mitigated / Monitoring  
**Risk Level:** Low / Medium / High  
**Notes:** Future monitoring or follow-up items.
