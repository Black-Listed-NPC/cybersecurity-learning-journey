# Day 8 - Module 5 (Part 3): Burp Suite and OWASP Top 10 (2025) Part 1

**Date:** 15 Oct 2026
**Module:** Module 5 - Application Security and Penetration Testing (part 3 of 5)
**Study time:** 1h 10m

| Lecture | Duration |
|---|---|
| Setting Up Burp Suite | 13m |
| OWASP Top 10 (2025 Edition) Part 1 | 57m |

> All hands-on work below was done only in my own isolated lab VMs or on the course's practice targets, for learning purposes.

## Covered today

### Burp Suite setup
- Burp is an intercepting proxy: the browser sends traffic to Burp, and Burp forwards it to the server.
- Setup: configure the browser (or Burp's built-in browser) to use the proxy `127.0.0.1:8080`, then install Burp's CA certificate so HTTPS traffic can be inspected.
- **Proxy > Intercept** - pause a request and read or change it before it reaches the server.
- **HTTP history** - every request and response, for review later.
- **Repeater** - resend one request again and again with small changes to see how the server reacts.
- Used it to look at real request structure: method, path, headers, cookies, body.

### OWASP and the Top 10
- **OWASP** (Open Web Application Security Project) is a non-profit founded in 2001 that publishes free resources for building secure software.
- The **OWASP Top 10** ranks the most critical web application risks using real-world data from security firms and vulnerability databases.

### OWASP Top 10 - 2025 edition
| ID | Risk | One-line meaning | Example from the course |
|---|---|---|---|
| A01 | Broken Access Control | Users act outside their intended permissions | Changing a URL parameter to view another user's data |
| A02 | Security Misconfiguration | Insecure defaults, open storage, verbose errors, missing headers | Default admin password left unchanged; directory listing on |
| A03 | Software Supply Chain Failures | Compromised or unverified dependencies, build or update pipeline | SolarWinds Orion (2020-21): malicious code inside a trusted update |
| A04 | Cryptographic Failures | Cleartext data, weak algorithms, bad password storage | Passwords sent over HTTP instead of HTTPS |
| A05 | Injection | Untrusted input interpreted as a command or query | SQL injection in a login form |
| A06 | Insecure Design | The design itself is flawed, before any code | Unlimited password-reset attempts with no rate limit |
| A07 | Authentication Failures | Weak identity confirmation and session handling | Allowing "123456"; no MFA on sensitive accounts |
| A08 | Software or Data Integrity Failures | No integrity checks on updates, plugins, CI/CD, deserialisation | Loading plugins from a CDN without checking signatures |
| A09 | Logging and Alerting Failures | Attacks are not logged or nobody is alerted | Failed logins not logged, so brute force goes unseen |
| A10 | Mishandling of Exceptional Conditions | Unexpected states are handled insecurely | Error pages leaking stack traces; the app failing "open" |

Part 1 of the lecture went deep on the first half of the list, especially A01 (access control) and A05 (injection).

## Key takeaways
- Burp is the main tool for every web assignment that follows.
- A01 Broken Access Control and A05 Injection are the categories behind most of this module's assignments.
