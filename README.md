
# 🛡️ HackMaster Web Application Penetration Testing Report

**Author:** Rajeev Sharma  
**Role Applied:** Penetration Tester & Red Team Specialist  
**Date:** May 4, 2025  
**Target:** [https://hack-master.hackersprey.com](https://hack-master.hackersprey.com)

---

## 📄 Overview

This repository contains the results of a comprehensive penetration test conducted on the HackMaster web application. The assessment aimed to identify security vulnerabilities, exploit real-world scenarios, and provide actionable recommendations to enhance the application's security posture.

---

## 🎯 Objective

- Identify 10 distinct security flags within the target web application.
- Exploit real-world web vulnerabilities to uncover these flags.
- Document findings, methodologies, and provide remediation strategies.

---

## 🧪 Methodology

The penetration testing approach adhered to industry best practices, incorporating both automated tools and manual techniques:

- **Tools Used:**
  - Burp Suite – Intercept & analyze requests
  - SQLMap – SQL injection testing
  - Gobuster – Directory enumeration
  - cURL – Manual HTTP requests
  - Browser Developer Tools – Frontend inspection
  - Custom Payloads – SSRF, Authentication Bypass, etc.

- **Testing Covered:**
  - Input validation & injection flaws
  - Directory & file discovery
  - Server-side request forgery (SSRF)
  - Authentication and access control
  - Sensitive data exposure

---

## 🧾 Findings & Flags

1. **Flag #1 – Sensitive File in `/donotopen`**
   - **Vulnerability:** Exposed sensitive flag via `robots.txt`
   - **Payload:** `curl https://hack-master.hackersprey.com/donotopen`
   - **Flag:** `hackersprey{d0_n0t_0p3n}`
   - **Severity:** Low

2. **Flag #2 – Exposed Credentials in `/adminCreds`**
   - **Payload:** `curl https://hack-master.hackersprey.com/adminCreds`
   - **Output:**
     ```
     Username: krichardson@hackersprey.com
     Password: backstreetboys
     ```
   - **Use Case:** Login for further exploitation (admin panel, SSRF, etc.)
   - **Severity:** High

3. **Flag #3 – Hidden Content in `/secret`**
   - **Response:** “look farther down” (possible lead to nested or encoded content)
   - **Next Step:** Analyze page source, JavaScript, or attempt path traversal
   - **Status:** Partial – needs further enumeration

4. **Flag #4 – Restricted Access in `/internal2` & `/internal3`**
   - **Status:** HTTP 403 Forbidden
   - **Bypass Attempts:** Use `X-Forwarded-For`, encoded URLs (`%2e`), etc.
   - **Flag Status:** Pending – might be flag-bearing endpoints

5. **Flag #5 – SQL Injection Vulnerability**
   - **Tool:** SQLMap
   - **Targeted Parameter:** `/admin?request=fetch&url=...`
   - **Injection Type:** Time-based blind
   - **DBMS:** MySQL
   - **Flag Status:** Likely hidden in backend data (DB dump pending)

*(Continue detailing the remaining flags as discovered.)*

---

## 📂 Repository Structure

````

hackmaster-pentest-report/
├── report/
│   ├── HackMaster\_Pentest\_Report.pdf
│   └── HackMaster\_Pentest\_Report.md
├── screenshots/
│   ├── flag1\_robots\_txt.png
│   ├── flag2\_admin\_creds.png
│   └── ...
├── payloads/
│   ├── sqlmap\_payload.txt
│   ├── ssrf\_payload.txt
│   └── ...
├── tools/
│   ├── burp\_config.json
│   └── ...
├── notes/
│   ├── methodology.md
│   ├── observations.md
│   └── ...
├── references/
│   ├── OWASP\_Top10.pdf
│   └── PTES\_Guide.pdf
├── LICENSE
└── README.md

```

---

## 🛠️ Tools & Resources

- **Burp Suite:** Intercepting proxy for analyzing web traffic.
- **SQLMap:** Automated tool for SQL injection detection and exploitation.
- **Gobuster:** Directory and file brute-forcing tool.
- **cURL:** Command-line tool for transferring data with URLs.
- **Browser Developer Tools:** Inspecting and debugging web applications.
- **Custom Payloads:** Crafted inputs for testing SSRF, authentication bypasses, etc.

---

## ✅ Recommendations

| Issue                          | Recommendation                                                                 |
|--------------------------------|--------------------------------------------------------------------------------|
| Exposed `robots.txt` entries   | Remove sensitive paths or restrict them via authentication headers.            |
| Hardcoded admin credentials    | Rotate credentials and store them securely in environment/configuration files. |
| Unprotected `/adminCreds`      | Apply access controls; restrict sensitive endpoints.                           |
| SQL Injection vulnerability    | Use parameterized queries; validate all user inputs.                           |
| Access control on `/internal`  | Enforce strict authorization and monitor for 403 bypass attempts.              |

---

## 📸 Appendix: Screenshots

Screenshots demonstrating the exploitation of identified vulnerabilities are available in the `screenshots/` directory:

- `flag1_robots_txt.png`: Exposure of sensitive file via `robots.txt`.
- `flag2_admin_creds.png`: Retrieved admin credentials from `/adminCreds`.
- *(Include additional screenshots as necessary.)*

---

## 📚 References

- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Penetration Testing Execution Standard (PTES)](http://www.pentest-standard.org/index.php/Main_Page)
- [Hack The Box: Penetration Testing Reports Guide](https://www.hackthebox.com/blog/penetration-testing-reports-template-and-guide)

---

## ⚠️ Disclaimer

This penetration testing report is intended solely for educational purposes. All testing activities were conducted on systems for which explicit authorization was obtained. No unauthorized testing was performed. All sensitive information has been removed to protect privacy and confidentiality.
```

