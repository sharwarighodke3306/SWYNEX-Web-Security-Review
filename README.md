# SWYNEX – Web Security Review

**Cybersecurity Internship | Task 3 | SWYNEX Technologies**

## 1. Project Overview

This project documents a practical web security review conducted as part of the SWYNEX Technologies Cybersecurity Internship.

The assessment was performed using **DVWA (Damn Vulnerable Web Application)**, an intentionally vulnerable web application deployed locally through Docker.

The objective was to explore common web application security vulnerabilities, observe application behaviour, collect testing evidence, understand potential security risks, and identify appropriate remediation techniques.

All practical exercises were conducted in a controlled local environment.

## 2. Objectives

- Understand common web application vulnerabilities.
- Perform practical security testing using DVWA.
- Observe application responses to different test inputs.
- Capture and organise testing evidence.
- Understand potential security impacts.
- Identify appropriate security controls and remediation techniques.
- Document practical observations in a structured security assessment report.

## 3. Tools and Environment

| Component | Details |
|---|---|
| Testing Application | DVWA (Damn Vulnerable Web Application) |
| Deployment | Docker |
| Database | MySQL |
| Testing Environment | Localhost |
| Browser | Web Browser |
| Documentation | GitHub |
| Classification Reference | Common Weakness Enumeration (CWE) |

**Application:** Damn Vulnerable Web Application (DVWA)  
**Local URL:** `http://localhost:4280`  
**Security Level:** Low

## 4. Testing Methodology

The assessment followed a structured practical testing approach:

1. Set up the DVWA application locally using Docker.
2. Accessed the application through a web browser.
3. Explored the available vulnerability modules.
4. Performed basic tests within the controlled environment.
5. Observed application responses and behaviour.
6. Captured screenshots as supporting evidence.
7. Documented observations, potential risks, and recommended remediation.

## 5. Vulnerabilities Tested

The following eight vulnerability areas were explored during the assessment.

| ID | Vulnerability | CWE | Testing Status |
|---|---|---|---|
| F-01 | SQL Injection | CWE-89 | Tested |
| F-02 | Reflected Cross-Site Scripting (XSS) | CWE-79 | Tested |
| F-03 | Stored Cross-Site Scripting (XSS) | CWE-79 | Tested |
| F-04 | OS Command Injection | CWE-78 | Tested |
| F-05 | Cross-Site Request Forgery (CSRF) | CWE-352 | Tested |
| F-06 | File Upload | CWE-434 | Upload and harmless PHP execution observed |
| F-07 | Brute Force – Login Behaviour | CWE-307 | Successful and unsuccessful login attempts tested |
| F-08 | File Inclusion | CWE-98 (potential mapping) | Page inclusion observed; arbitrary file inclusion not confirmed |

**Testing limitations:**

- The Brute Force exercise demonstrated successful and unsuccessful login behaviour but did not establish whether rate limiting was absent.
- The File Upload exercise confirmed the upload and execution of a harmless PHP test file. Other upload restrictions were not comprehensively assessed.
- The File Inclusion exercise demonstrated page selection and inclusion, but arbitrary local file inclusion was not confirmed.
- Testing status reflects the observations made during the exercises and does not imply that every possible attack condition was verified.

## 6. Key Learning Outcomes

The practical exercises provided exposure to the following concepts:

- SQL query security and input handling.
- Reflected and stored XSS vulnerabilities.
- Secure file upload practices.
- Authentication security and login protection.
- Operating system command handling.
- CSRF protection mechanisms.
- File inclusion and path validation.
- Security evidence collection and documentation.
- Vulnerability impact assessment.
- Security remediation and defensive practices.

## 7. Repository Structure

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

*The screenshot directory structure represents the planned organisation of supporting evidence. Actual folders and files should be added before final submission.*

## 8. Detailed Security Assessment Report

The detailed security assessment report provides further information about the practical exercises, including:

- Vulnerability descriptions.
- Testing observations.
- Potential security impacts.
- Recommended remediation measures.
- Evidence references.
- Testing limitations.

**[View Detailed Security Assessment Report](./security-report.md)**

## 9. Scope and Disclaimer

- All testing was performed on a locally hosted DVWA training application.
- No third-party websites, networks, or systems were targeted.
- The exercises were conducted for educational and defensive cybersecurity learning.
- The assessment was limited to the selected DVWA modules and observed application behaviour.
- The documented observations should not be interpreted as a comprehensive security audit.

## 10. Conclusion

This project provided practical exposure to common web application security testing concepts through DVWA.

Working with the application helped develop an understanding of how insecure input handling, authentication weaknesses, file processing, and request validation can affect web application security.

The assessment also highlighted the importance of collecting reliable evidence, interpreting testing results accurately, understanding security limitations, and recommending appropriate remediation measures.

---

**Organization:** SWYNEX Technologies  
**Internship:** Cybersecurity Internship  
**Task:** Task 3 – Web Security Review

*Learning through practical application and defensive security testing.*
