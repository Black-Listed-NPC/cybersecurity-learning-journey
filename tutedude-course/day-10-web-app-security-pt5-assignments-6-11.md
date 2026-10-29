# Day 10 - Module 5 (Part 5): CSRF and RCE + Assignments 6-11

**Date:** 17 Oct 2026
**Module:** Module 5 - Application Security and Penetration Testing (complete)
**Study time:** 46m
**Assignments:** 6, 7, 8, 9, 10, 11

| Lecture | Duration |
|---|---|
| Bug Bounty Workflow Part 2 (CSRF and RCE) | 46m |

> All hands-on work below was done only on the course's dedicated practice application, for learning purposes.

## Covered today

### CSRF - Cross-Site Request Forgery
- **What it is:** a malicious page makes the victim's browser send a request to a site where the victim is already logged in. The browser attaches the session cookie automatically, so the request runs with the victim's permissions.
- **Why it works:** the server checks *who* is sending (the cookie) but not whether the user *intended* the action.
- **Typical impact:** changing email or password, transferring money, changing settings.
- **Defences:**
  - Anti-CSRF tokens (unique, unpredictable, checked on every state-changing request)
  - `SameSite=Lax` or `Strict` cookies
  - Re-authentication for sensitive actions
  - Checking the `Origin`/`Referer` headers
  - Never changing state with GET requests

### RCE - Remote Code Execution
- **What it is:** the attacker gets the server to run commands of their choosing. It is the worst-case result of many bugs: command injection, unsafe file upload, insecure deserialisation, or vulnerable components.
- **Impact:** full server compromise, data theft, pivoting into the internal network.
- **Defences:**
  - Never pass user input to system calls or shells; use safe library functions and allow-lists
  - Validate uploads (type, extension, storage outside the web root, no execute permission)
  - Patch frameworks and components quickly
  - Run services with least privilege, so even a successful RCE gets very little

## Assignments completed
All six Module 5 assignments were done on the course's practice web application using Burp Suite (Proxy and Repeater).

| # | Assignment | OWASP category | What it was about |
|---|---|---|---|
| 6 | Improper Session Management | A01 / A07 | The app trusted a client-side value for the user's role |
| 7 | Admin Panel | A01 Broken Access Control | The admin panel was protected only by a flag the client could edit |
| 8 | IDOR | A01 Broken Access Control | Changing an object ID exposed another user's private data |
| 9 | Reset Password | A01 / A06 | The password-reset flow trusted a user identifier from the request |
| 10 | Cross-Site Scripting | A05 Injection | User input was reflected into the page without output encoding |
| 11 | SQL Injection | A05 Injection | Input was concatenated into a database query |

## Key takeaways
- Assignments 6 to 9 share one root cause: **the server trusted the client**. The fix is always server-side authorisation tied to the session, never to something the user can edit.
- XSS means output was not encoded; SQLi means input was concatenated into a query. Fix them with output encoding, a Content Security Policy and parameterised queries.
- Module 5 complete.
