# RDP Brute Force Attack Analysis Report

## 📌 Overview
This report presents the analysis of a simulated **RDP brute force attack**, investigated using Splunk.

- The attack logs were artificially generated using ChatGPT for training purposes.
- The logs were ingested into Splunk to simulate a real SOC investigation workflow.
- The goal: identify suspicious behavior, detect brute-force patterns, and analyze IPS/SIEM correlation.

---

## 🧩 Step 1 — Identifying Suspicious IP Addresses
After filtering relevant RDP (port **3389**) traffic in Splunk, three IP addresses appeared suspicious:

```
203.0.113.50
10.0.0.70
10.0.0.50
```

Based on event volume, **203.0.113.50** showed the largest spike and was marked as the primary suspect.

---

## 🔍 Deep-Dive Into the Suspicious IP (203.0.113.50)

Further filtering showed:

- **21 total events** associated with this IP  
- **16 login attempts** within **32 seconds**

### 🕒 Attack Timeline
| Event | Timestamp |
|-------|-----------|
| **First login attempt** | 25/11/2025 10:05:01 |
| **Last recorded attempt** | 25/11/2025 10:05:33 |

After the last logged attempt, additional attempts were likely made but **were blocked by the IPS**.

---

## 🚨 IPS Alerts & Behavior

During the attack, two IPS alert types were triggered:

1. **`rdp_bruteforce_threshold`**  
   - Triggered **3 times**
   - Indicates the system identified high-frequency login attempts

2. **`rdp_bruteforce_blocked_ip`**  
   - Triggered **2 times**
   - Indicates the IP was added to the IPS blacklist and traffic was blocked

**Conclusion:**  
The attacker IP (`203.0.113.50`) was **automatically blacklisted** by the IPS after exceeding the brute-force threshold.

---

## 🛡 Additional Investigation — Lateral Activity?
A search was conducted to verify whether this IP engaged in any additional activity within the environment.

**Result:**  
All events originated from **RDP traffic only**.  
No evidence of lateral movement or non-RDP probing was found.

---

## 📌 Attack Pattern Summary
- Traffic detected on port **3389**
- Multiple rapid login attempts (**16 attempts / 32 seconds**)
- Attempts originating from a single IP
- IPS detection + automatic blocking sequence initiated

---

## 📸 Splunk Evidence
A screenshot of the Splunk query identifying these events was added to the Alerts dashboard.

