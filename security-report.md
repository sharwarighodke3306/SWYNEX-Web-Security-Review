# Security Assessment Report — DVWA

**Project**: SWYNEX-Web-Security-Review
**Author**: Sharwari Ghodke
**Target**: DVWA (Damn Vulnerable Web Application), local Docker deployment
**Testing Methodology**: NIST SP 800-115
**Classification**: CWE, CVSS v3.1

---

## 1. Scope & Methodology

Testing was conducted against a locally hosted instance of DVWA (`ghcr.io/digininja/dvwa`), running via Docker with a linked MySQL 5.7 database container. All testing was performed at **Security Level: Low**, with one finding (F-04) additionally verified at **Medium** to demonstrate filter bypass. No external or production systems were in scope.

Testing followed the NIST SP 800-115 phases: Planning, Discovery, Attack (Execution), and Reporting.

---

## 2. Findings

### F-01: SQL Injection
- **CWE**: CWE-89 (Improper Neutralization of Special Elements used in an SQL Command)
- **Module**: DVWA SQL Injection
- **Payload**: `1' OR '1'='1` (and baseline test with `1'` alone, which produced a raw SQL syntax error, confirming unsanitized input is passed directly into the query)
- **Evidence**: `f01-injection.png`, `f01-error.png`, `f01-normal.png`
- **CVSS 3.1**: `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:N` → **8.1 (High)**
- **NIST Phase**: Execution
- **Root Cause**: User input concatenated directly into SQL queries without parameterization.
- **Remediation**: Use parameterized queries / prepared statements; apply least-privilege database accounts; validate and sanitize all input server-side.

### F-02: Reflected Cross-Site Scripting (XSS)
- **CWE**: CWE-79 (Improper Neutralization of Input During Web Page Generation)
- **Module**: DVWA XSS (Reflected)
- **Payload**: `<script>alert('XSS')</script>`
- **Evidence**: `f02-normal.png` (baseline), `f02-xss.png` (payload executes, alert fires), `f02-after.png`
- **CVSS 3.1**: `AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N` → **6.1 (Medium)**
- **NIST Phase**: Execution
- **Root Cause**: User-supplied input reflected into the HTML response without output encoding.
- **Remediation**: Context-aware output encoding (HTML-entity encode all reflected input), implement a Content Security Policy (CSP).

### F-03: Stored Cross-Site Scripting (XSS)
- **CWE**: CWE-79
- **Module**: DVWA XSS (Stored) — Guestbook
- **Payload**: Script payload submitted via the guestbook Message field
- **Evidence**: `f03-stored.png` (submission), `f03-after.png` (payload executes on page reload for any visitor)
- **CVSS 3.1**: `AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N` → **6.1 (Medium)**, though real-world impact is typically rated higher than reflected XSS since the payload persists and affects every visitor without a crafted link.
- **NIST Phase**: Execution
- **Root Cause**: User-submitted content stored and rendered without sanitization or output encoding.
- **Remediation**: Sanitize input before storage, encode output on render, apply CSP.

### F-04: OS Command Injection (including filter bypass)
- **CWE**: CWE-78 (Improper Neutralization of Special Elements used in an OS Command)
- **Module**: DVWA Command Injection
- **Payload (Low)**: `127.0.0.1 | id` → `uid=33(www-data) gid=33(www-data) groups=33(www-data)`
- **Evidence**: `f04-cmdi.png`
- **Additional observation**: The same payload was also tested at Medium security level and was observed to still succeed, since Medium-level filtering blacklists `&&` and `;` but does not block the pipe (`|`) character. This was not separately screenshotted and is reported as a tested observation rather than a formally evidenced sub-finding.
- **CVSS 3.1**: `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` → **9.9 (Critical)**
- **NIST Phase**: Execution
- **Root Cause**: User input passed to a shell command without sanitization; Medium-level mitigation relies on an incomplete blacklist (CWE-184) rather than strict input validation.
- **Remediation**: Avoid shell invocation entirely; use safe, parameterized system APIs. If shell use is unavoidable, apply strict allow-listing (valid IP/hostname format only), never blacklist-based filtering.

### F-05: Cross-Site Request Forgery (CSRF)
- **CWE**: CWE-352
- **Module**: DVWA CSRF — Change Password
- **Request**: `GET /vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change` — password changed successfully with no CSRF token and no re-entry of current password required at Low
- **Evidence**: `f05b-csrf-revert.png` (shows the same vulnerable flow used to revert the password, confirming the mechanism)
- **CVSS 3.1**: `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N` → **8.1 (High)**
- **NIST Phase**: Execution
- **Root Cause**: No anti-CSRF token; state-changing action accepted via GET request.
- **Remediation**: Implement per-session CSRF tokens validated server-side; require current password re-entry for sensitive actions; use POST (not GET) for all state-changing requests.

### F-06: Unrestricted File Upload
- **CWE**: CWE-434 (Unrestricted Upload of File with Dangerous Type)
- **Module**: DVWA File Upload
- **Action**: Uploaded a PHP test file (`dvwa_test.php`) with no file-type validation enforced; file was accepted and, once accessed directly, executed server-side
- **Evidence**: `F04_File_Upload_Success.png` (upload accepted), `F04_File_Upload_Execution.png` (uploaded file executes and returns "DVWA File Upload Test Successful")
- **CVSS 3.1**: `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` → **9.1 (Critical)**
- **NIST Phase**: Execution
- **Root Cause**: No server-side validation of file type, extension, or content before storing the upload in a web-accessible directory.
- **Remediation**: Validate file type by content (not extension), store uploads outside the web root or in a directory with script execution disabled, rename uploaded files, enforce an allow-list of permitted file types.

### F-07: Brute Force (Login)
- **CWE**: CWE-307 (Improper Restriction of Excessive Authentication Attempts)
- **Module**: DVWA Brute Force (Low)
- **Test**: Submitted 5-6 consecutive incorrect login attempts, followed immediately by the correct credentials (`admin`/`password`)
- **Result**: After repeated failures, the application displayed a message suggesting a possible account lockout ("the account has been locked because of too many failed logins... if this is the case, please try again in 15 minutes"). However, the correct login succeeded immediately afterward with no delay — confirming this message is misleading and that no actual lockout, rate-limiting, or delay is enforced at Low security.
- **Evidence**: `F05_Brute_Force_Invalid_Login.png`, `F05_Brute_Force_Success.png`
- **CVSS 3.1**: `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N` → **7.5 (High)**
- **NIST Phase**: Execution
- **Root Cause**: No account lockout, rate-limiting, or CAPTCHA enforced after repeated failed login attempts; the displayed warning message does not correspond to actual enforced behavior.
- **Remediation**: Implement real account lockout after N failed attempts, add progressive delays between attempts, require CAPTCHA after repeated failures, and log/alert on repeated authentication failures.

### F-08: Local File Inclusion (LFI)
- **CWE**: CWE-98 (PHP Remote File Inclusion) / CWE-22 (Path Traversal)
- **Module**: DVWA File Inclusion (Low)
- **Payload**: `?page=../../../../../etc/passwd`
- **Result**: The application returned the complete contents of the system's `/etc/passwd` file, confirming arbitrary local file inclusion via path traversal:
