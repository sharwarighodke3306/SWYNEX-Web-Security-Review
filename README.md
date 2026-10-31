# SWYNEX – Web Security Review

**Cybersecurity Internship | Task 3 | SWYNEX Technologies**

## 1. Project Overview

This project documents a practical web security review conducted as part of the SWYNEX Technologies Cybersecurity Internship.

The assessment was performed using **DVWA (Damn Vulnerable Web Application)**, an intentionally vulnerable web application deployed locally through Docker.

The objective was to explore common web application security vulnerabilities, observe application behaviour, collect testing evidence, understand potential security risks, and identify suitable remediation techniques.

All practical exercises were conducted in a controlled local environment.

## 2. Objectives

- Understand common web application vulnerabilities.
- Perform basic security testing using DVWA.
- Observe application responses to different test inputs.
- Capture and organise testing evidence.
- Understand potential security impacts.
- Identify appropriate security controls and remediation techniques.

## 3. Tools and Environment

| Component | Details |
|---|---|
| Testing Application | DVWA |
| Deployment | Docker |
| Database | MySQL |
| Testing Environment | Localhost |
| Browser | Web Browser |
| Documentation | GitHub |
| Classification Reference | CWE |

**Application:** Damn Vulnerable Web Application (DVWA)  
**Local URL:** `http://localhost:4280`  
**Security Level:** Low

## 4. Vulnerabilities Tested

The following vulnerability areas were explored during the practical assessment.

| ID | Vulnerability | CWE | Testing Status |
|---|---|---|---|
| F-01 | SQL Injection | CWE-89 | Tested |
| F-02 | Reflected Cross-Site Scripting (XSS) | CWE-79 | Tested |
| F-03 | Stored Cross-Site Scripting (XSS) | CWE-79 | Tested |
| F-04 | OS Command Injection | CWE-78 | Tested |
| F-05 | Cross-Site Request Forgery (CSRF) | CWE-352 | Tested |
| F-06 | File Upload | CWE-434 | Upload and harmless PHP execution observed |
| F-07 | Brute Force – Login Behaviour | CWE-307 | Successful and unsuccessful login attempts tested |
| F-08 | File Inclusion | CWE-98 | Page inclusion observed; arbitrary file inclusion not confirmed |

*Note: Testing status describes the practical observations made during the exercises. It does not imply that every possible attack condition or security control was independently verified.*

## 5. Key Learning Outcomes

Through this assessment, the following concepts were explored:

- SQL query security and input handling.
- Reflected and stored XSS risks.
- Secure file upload practices.
- Authentication security and login protection.
- Operating system command handling.
- CSRF protection mechanisms.
- File inclusion and path validation.
- Security evidence collection and documentation.
- Identifying appropriate mitigation techniques.

## 6. Repository Structure

```text
SWYNEX-Web-Security-Review/
│
├── README.md
│
├── security-report.md
│
└── screenshots/
    ├── SQL-Injection/
    ├── Reflected-XSS/
    ├── Stored-XSS/
    ├── File-Upload/
    ├── Command-Injection/
    ├── CSRF/
    ├── Brute-Force/
    └── File-Inclusion/
```

*The directory structure represents the intended organisation of project evidence.*

## 7. Detailed Security Assessment Report

The detailed report includes:

- Vulnerability descriptions.
- Practical testing observations.
- Potential security impacts.
- Recommended remediation measures.
- Evidence references and testing limitations.

**[View Detailed Security Report](./security-report.md)**

## 8. Scope and Disclaimer

- All testing was performed on a locally hosted DVWA training application.
- No third-party websites, networks, or systems were targeted.
- The exercises were conducted for educational and defensive cybersecurity learning.
- Findings are limited to the behaviours observed during the assessment.

## 9. Conclusion

This project provided practical exposure to common web application security testing concepts.

Working with DVWA helped develop an understanding of how insecure input handling, authentication weaknesses, file processing, and request validation can affect application security.

The assessment also highlighted the importance of collecting reliable evidence, interpreting test results accurately, and recommending suitable remediation measures.

---

**Organization:** SWYNEX Technologies  
**Internship:** Cybersecurity Internship  
**Task:** Task 3 – Web Security Review

*Learning through practical application and defensive security testing.*
