# SWYNEX-Web-Security-Review

Defensive web security review conducted as part of the SWYNEX Technologies Cyber Security Internship (Task 3).

## Overview

This project documents a hands-on security assessment of **DVWA (Damn Vulnerable Web Application)**, deployed locally via Docker. The goal was to identify, exploit, and document common web application vulnerabilities in a safe, controlled environment, and to understand both the attacker's perspective and appropriate remediation strategies.

## Environment

- **Target**: DVWA (`ghcr.io/digininja/dvwa`), run via Docker
- **Database**: MySQL 5.7, linked container
- **Security Level**: Low (unless otherwise noted)
- **Classification frameworks used**: CWE, CVSS v3.1, NIST SP 800-115

## Findings Summary

| ID | Vulnerability | CWE | CVSS 3.1 Score | Status |
|----|----------------|-----|-----------------|--------|
| F-01 | SQL Injection | CWE-89 | 8.1 (High) | ✅ Confirmed |
| F-02 | Reflected XSS | CWE-79 | 6.1 (Medium) | ✅ Confirmed |
| F-03 | Stored XSS | CWE-79 | 6.1 (Medium) | ✅ Confirmed |
| F-04 | OS Command Injection (incl. Medium-level filter bypass) | CWE-78 | 9.9 (Critical) | ✅ Confirmed |
| F-05 | Cross-Site Request Forgery (CSRF) | CWE-352 | 8.1 (High) | ✅ Confirmed |
| F-06 | Unrestricted File Upload | CWE-434 | 9.1 (Critical) | ✅ Confirmed |
| F-07 | Brute Force (login) | CWE-307 | 7.5 (High) | ✅ Confirmed |
| F-08 | Local File Inclusion (LFI) | CWE-98 / CWE-22 | 7.5 (High) | ✅ Confirmed |

See [`security-report.md`](./security-report.md) for full details, including payloads, evidence, and remediation guidance.

## Repository Structure
