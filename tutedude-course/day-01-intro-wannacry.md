# Day 1 - Module 1 and Module 2 (Part 1): Getting Started and Introduction

**Date:** 08 Oct 2026
**Modules:** Module 1 - Getting Started with Tutedude (complete), Module 2 - Introduction (part 1)
**Study time:** 1h 28m

| Lecture | Module | Duration |
|---|---|---|
| How to connect with mentors and resolve doubts | M1 | 3m |
| Introduction to me and the Course | M2 | 25m |
| Choose Your Cybersecurity Path | M2 | 37m |
| WannaCry Ransomware Introduction | M2 | 23m |

Started the Tutedude Cybersecurity course. Day 1 covered how mentorship works, what cybersecurity actually is, the main career paths, and the first part of the WannaCry case study.

## Covered today

### What cybersecurity is
- Cybersecurity is the body of technologies, processes and practices designed to protect networks, computers, programs and data from attack, damage or unauthorised access.
- Why it matters now: almost everything in the "digital era" (banking, health, elections, personal data) runs on connected systems. The Cambridge Analytica / 2016 US election case showed that misuse of data is as dangerous as a technical hack.
- **CIA triad** - the base of everything in the course:
  - **Confidentiality** - only authorised people can read the data.
  - **Integrity** - data is not changed without permission.
  - **Availability** - systems and data are reachable when needed.
- **Three pillars of cybersecurity:** People, Process, Technology. A tool alone does not protect anything if people are untrained or the process is missing.
- A short incident story ("Meet Wendy") showed how one incident pulls in a whole incident response team.

### Course roadmap
Linux and Python, foundations of information security, application security and pentesting, network defense and pentesting, data protection and cryptography, GRC (ISO, ISMS), emerging technologies (AI, IoT), SOC, SIEM with Splunk, and RCA / breach investigation.

### Choosing a cybersecurity path
| Role | What they do | Typical tools / certifications |
|---|---|---|
| Computer Forensic Analyst | Evidence collection, data recovery, analysis, documentation, reporting, court testimony | EnCase, FTK, Autopsy, Sleuth Kit; CHFI |
| SOC Analyst | Monitor alerts, triage, detect and respond to incidents | SIEM (Splunk, QRadar), IDS/IPS (Snort), EDR (CrowdStrike), firewalls |
| GRC Analyst | Policy development, risk assessments, compliance audits | GDPR, HIPAA, PCI DSS knowledge |
| Penetration Tester | Scope tests, find and validate vulnerabilities, report, retest | Nmap, Burp Suite, Wireshark, Metasploit, OWASP ZAP; CEH, OSCP, GPEN |
| Others | Incident Responder, Security Architect, Malware Analyst | - |

- **SOC career ladder:** L1 (monitoring and initial triage) -> L2 (detailed investigation, coordinating response) -> L3 (leads major incidents and threat intelligence).
- **GRC career ladder:** Risk / Compliance Analyst, IT Auditor -> Senior GRC Analyst, GRC Manager -> Chief Risk Officer / Chief Compliance Officer.
- **Red Team vs Blue Team:** the Red Team plays the adversary in a controlled, authorised setting; the Blue Team defends - identifies critical assets, monitors data flow and user behaviour, and hardens the environment.
- **Kali Linux:** Debian-derived distribution for pentesting and forensics, maintained by Offensive Security. Set it up as a VirtualBox VM using the course install guide (pre-built VirtualBox image, shared clipboard set to bidirectional, extra RAM and video memory).

### WannaCry - introduction
Studied the CERT-In advisory on WannaCry (2017):
- **Two components:** a **worm** that spreads across a LAN over SMB, and a **ransomware package** that encrypts files. It also spread through malicious email attachments.
- **Vulnerability:** the SMBv1 flaw fixed by Microsoft in **MS17-010** (the leaked exploit was called EternalBlue).
- **Ransom:** started at USD 300 and rose to USD 600 in Bitcoin; estimated global damage above USD 4 billion.
- **Behaviour:** encrypts a long list of file types (office files, archives, databases, source code, keys and certificates, VM disks), appends `.WCRY`, replaces the wallpaper and drops a ransom note available in 28 languages.
- **Indicators of compromise listed by CERT-In:** files named `tasksche.exe` / `mssecsvc.exe` appearing under `ProgramData` or `C:\Windows\`, a command that grants Everyone full access to files, and a numbered batch helper script.

## Key takeaways
- Prevention from the advisory: patch MS17-010, disable SMBv1, block SMB ports (UDP 137/138, TCP 139/445) at the perimeter, segment the network (router ACLs, private VLANs, host firewalls on TCP 445), keep offline backups, and disable Office macros.
- If infected: isolate the machine immediately, preserve the data (even if encrypted), and report to CERT-In and law enforcement.

## Reflection
WannaCry is a perfect opener: one unpatched service plus a flat network turned a single infection into a worldwide outage. It explains why every later module - patching, VAPT, SIEM, incident response - matters.
