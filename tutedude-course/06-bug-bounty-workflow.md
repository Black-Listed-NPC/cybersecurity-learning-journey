# Day 17 – Module 5 (Part 4): Bug Bounty Workflow

**Course:** Tutedude Cybersecurity
**Lectures:** Bug Bounty Workflow Part 1 (Reconnaissance → PoC) (59m) · Bug Bounty Workflow Part 2 (CSRF & RCE) (46m)

---

## 1. What is Bug Bounty Hunting?

**Definition:** programs where companies pay independent security researchers to find and responsibly report vulnerabilities in their products.

**Purpose:**
- Improve product security before attackers find the same holes
- Encourage ethical hacking as an alternative to malicious hacking
- Reduce overall cyber risk for the company

**Platforms:** HackerOne, Bugcrowd, Intigriti, Synack.

---

## 2. The Bug Bounty Workflow (5 steps)

```
Reconnaissance → Vulnerability Discovery → Exploitation & PoC → Documentation → Submission & Follow-Up
```

### Step 1 – Reconnaissance
**Goal:** gather as much information about the target as possible before testing anything.

| Technique | Tools |
|-----------|-------|
| Subdomain enumeration | Amass, Subfinder |
| Directory brute-forcing | Gobuster, Dirsearch |
| Tech stack identification | Wappalyzer, BuiltWith |
| OSINT | Google Dorking, Shodan, WHOIS |

**Output:** a map of the target and its attack surface — ties back to the passive/active recon from Module 4.

### Step 2 – Vulnerability Discovery
A mix of manual and automated testing.

| Manual testing | Automated scanning |
|-----------------|---------------------|
| Input validation checks | Acunetix scanner |
| Authentication checks | Nmap (service discovery + vuln scripts) |
| Session management flaws | |

**Common vulnerability categories to look for:** XSS, SQL Injection, CSRF, IDOR (Insecure Direct Object Reference), SSRF (Server-Side Request Forgery), RCE (Remote Code Execution).

### Step 3 – Exploitation & Proof of Concept (PoC)
**Purpose:** confirm the vulnerability is real and understand its actual impact — not just theoretical.

**Safe testing practice:**
- Avoid any action that could damage production systems
- Use test/throwaway accounts wherever possible
- Stay strictly within the program's defined scope

**Building the PoC:** screenshots, network traffic logs (captured in Burp Suite or Wireshark), and relevant code snippets.

### Step 4 – Documentation & Reporting
Good documentation is what turns a finding into a fixed vulnerability — it enables clear communication with the security team and faster triage.

**Key elements of a report:**
- Title & summary
- Vulnerability description
- Impact assessment
- Steps to reproduce
- Proof of concept
- Suggested fix

### Step 5 – Submission & Follow-Up
Submitted through the bug bounty platform's portal.

**Tips:**
- Be clear and concise about the vulnerability and its impact
- Attach proof (screenshots, logs, code)
- Follow up promptly and professionally on any questions
- Keep all communication respectful and fact-focused

---

## 3. CSRF (Cross-Site Request Forgery)

**What it is:** CSRF tricks a logged-in user's browser into sending a request to a website they're already authenticated on, without the user intending it. Because the browser automatically attaches the user's session cookie to the request, the server can't tell the difference between a request the user meant to make and one a malicious page triggered on their behalf.

**Why it works:** cookies are sent automatically with every request to a domain, regardless of which page or site triggered that request. If a site doesn't check *why* a request was made (only *who* it came from), an attacker can forge one.

**Typical impact:** unwanted actions performed as the victim — changing an email/password, transferring funds, or modifying account settings — without the victim knowingly doing it.

**Defenses (what to look for when testing, and what to recommend when reporting):**
- Anti-CSRF tokens (a unique, unpredictable token tied to the user's session that must be included in each state-changing request)
- `SameSite` cookie attribute set to `Lax` or `Strict`
- Re-authentication (password confirmation) for sensitive actions
- Checking the `Origin`/`Referer` header on state-changing requests

---

## 4. RCE (Remote Code Execution)

**What it is:** the most severe class of web vulnerability — it lets an attacker run arbitrary commands or code on the target server itself, rather than just manipulating data in the application. This is the end goal many other vulnerabilities (insecure deserialization, unrestricted file upload, command injection, vulnerable plugins) can chain into.

**How it typically arises:**
- Unsanitized input passed into a system command (command injection)
- Insecure deserialization of untrusted data
- Unrestricted file upload that lets an attacker upload and then execute a malicious script
- Exploiting a known vulnerability in outdated software or a plugin (this is exactly what the WordPress lab from Day 15 demonstrated — an admin-panel exploit was used to get code execution)

**Impact:** full compromise of the server — an attacker can read/modify/delete data, pivot to other systems, or use the box as a foothold, as seen in the privilege-escalation chain from the WordPress defacement lab.

**Defenses:**
- Never pass unsanitized user input into system calls or `eval()`-style functions
- Validate and restrict file uploads (type, size, and never execute from the upload directory)
- Keep all software, plugins, and dependencies patched and updated
- Run services with the least privilege necessary, so even a successful RCE is contained

---

## 5. Introduction to CTFs (Capture The Flag)

**Definition:** cybersecurity competitions where players solve challenges to "capture" a flag (a hidden string that proves the challenge was solved).

**Why bug bounty hunters practice CTFs:**
- Builds skills across web, network, reverse engineering, and cryptography
- Teaches new exploitation techniques in a legal, built-for-practice environment
- Improves problem-solving speed

**CTF workflow:** choose a platform (TryHackMe, HackTheBox, PicoCTF) → pick a category (Web, Crypto, Pwn, Forensics) → analyze the challenge → exploit and extract the flag → document the solution.

### Tools & skills referenced
| Category | Item | Purpose |
|----------|------|---------|
| Tool | Burp Suite | Web vulnerability scanner and proxy |
| Tool | Wireshark | Network protocol analyzer |
| Tool | Ghidra / IDA | Reverse engineering compiled software |
| Tool | John the Ripper / Hashcat | Password cracking / hash recovery |
| Skill | Scripting (Python, Bash) | Automating tasks, writing custom tools |
| Skill | Regular expressions | Pattern matching in text/logs |
| Skill | Reverse engineering | Analyzing compiled code/binaries |
| Skill | Networking basics | Understanding protocols and traffic |

---

## 6. Reporting Standards & Common Mistakes

**Bug bounty reports** should be professional, well-structured, and give clear, actionable information.
**CTF writeups** are more educational — step-by-step, explaining tools used and the reasoning behind each step.

**Common mistakes to avoid:**
- Missing reproduction steps
- Vague descriptions of impact
- No proof-of-concept evidence

**Best practices:**
- Always read and follow the program's scope before testing anything
- Test responsibly — avoid production environments unless explicitly permitted
- Keep tools updated
- Learn continuously from public writeups
- Practice regularly through CTFs

**Resources mentioned:** HackerOne Hacktivity, Bugcrowd University, OWASP Testing Guide, PortSwigger Web Security Academy, TryHackMe, HackTheBox.

---

## My own words summary
This tied together everything from the last few modules into one real workflow: recon (Module 4) finds the attack surface, OWASP Top 10 (Day 16) tells you what categories of bugs to look for, Burp Suite is the tool that captures the proof, and now CSRF/RCE are two concrete examples of what "exploitation" actually looks like. CSRF abuses the fact that cookies get sent automatically and nothing checks *intent*; RCE is the worst-case outcome of almost any other flaw, since it hands the attacker the whole server — which is exactly what happened step by step in the WordPress lab. The biggest non-technical takeaway is that a bug report lives or dies on documentation: a real vulnerability with no reproduction steps or PoC is as good as not finding it at all.

## Things to explore more
- Try a CSRF lab on PortSwigger's Web Security Academy to see a working PoC form.
- Look at a beginner RCE room on TryHackMe to see how file upload → shell actually plays out in Burp.
