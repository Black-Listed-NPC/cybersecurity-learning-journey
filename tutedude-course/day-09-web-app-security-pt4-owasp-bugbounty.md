# Day 9 - Module 5 (Part 4): OWASP Top 10 Part 2 and Bug Bounty Workflow

**Date:** 16 Oct 2026
**Module:** Module 5 - Application Security and Penetration Testing (part 4 of 5)
**Study time:** 1h 16m

| Lecture | Duration |
|---|---|
| OWASP Top 10 (2025 Edition) Part 2 | 17m |
| Bug Bounty Workflow Part 1 (Reconnaissance to PoC) | 59m |

## Covered today

### OWASP Top 10 - Part 2
Finished the second half of the list (A06 to A10) with the defences for each:
- **Insecure Design** - threat modelling and secure design patterns during planning, not after release.
- **Authentication Failures** - strong password policy, MFA, secure session handling, lockout and rate limiting.
- **Integrity Failures** - signed updates and plugins, protected CI/CD pipelines, no deserialising of untrusted data.
- **Logging and Alerting Failures** - log security events (logins, failures, privilege changes), monitor them and alert on attacks. Without logs, incident response and forensics are nearly impossible.
- **Exceptional Conditions** - validate inputs, handle errors securely, never show internal details in error messages, and return to a safe state after a failure.

### Bug bounty programs
- Companies pay researchers for responsibly reporting vulnerabilities. This improves product security and lowers cyber risk.
- Platforms: **HackerOne, Bugcrowd, Intigriti, Synack**.

### Bug bounty workflow
1. **Reconnaissance** - map the target: subdomain enumeration (Amass, Subfinder), directory discovery (Gobuster, Dirsearch), technology identification (Wappalyzer, BuiltWith), OSINT (Google dorking, Shodan, WHOIS). Output: a target map and the attack surface.
2. **Vulnerability discovery** - manual testing (input validation, authentication checks, session management) plus automated scanning. Common classes: XSS, SQLi, CSRF, IDOR, SSRF, RCE.
3. **Exploitation and proof of concept** - confirm the issue exists and understand its impact **safely**: avoid damage to production and use your own test accounts. Evidence: screenshots, Burp/Wireshark logs, small code snippets.
4. **Documentation** - title and summary, description, impact assessment, steps to reproduce, proof of concept, suggested fix.
5. **Submission and follow-up** - submit through the platform, answer questions quickly, stay professional and factual.

### CTFs as practice
- Capture The Flag platforms: **TryHackMe, HackTheBox, PicoCTF**. Categories: web, crypto, pwn, forensics.
- Workflow: choose a platform -> pick a category -> analyse -> solve and get the flag -> write up the solution.
- Core toolkit: Burp Suite, Wireshark, Ghidra/IDA, John the Ripper/Hashcat, Python/Bash scripting, regular expressions, networking basics.

### Reporting rules
- Bug bounty reports are professional and actionable; CTF write-ups are educational, step by step.
- **Common mistakes:** missing reproduction steps, vague impact, no proof of concept.
- **Best practices:** read and respect the program scope, never test production unless explicitly allowed, keep tools updated, learn from public write-ups (HackerOne Hacktivity, Bugcrowd University, OWASP Testing Guide, PortSwigger Web Security Academy).

## Key takeaways
- A finding with no clear proof of concept or reproduction steps is almost as good as no finding.
- Recon -> discover -> PoC -> report is exactly the structure the assignments and the capstone follow.
