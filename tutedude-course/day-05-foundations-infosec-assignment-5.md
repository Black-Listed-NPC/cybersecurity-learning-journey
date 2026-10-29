# Day 5 - Module 4: Foundations of Information Security + Assignment 5

**Date:** 12 Oct 2026
**Module:** Module 4 - Foundations of Information Security (complete)
**Study time:** 1h 40m
**Assignment:** 5

| Lecture | Duration |
|---|---|
| Information Gathering (Active and Passive) | 34m |
| Common Threat Vectors: Malicious Code and more | 29m |
| Modern Attack Methodologies: From Social Engineering and more | 37m |

> All hands-on work below was done only in my own isolated lab VMs or on the course's practice targets, for learning purposes.

## Covered today

### Core security concepts
- **Information security vs cybersecurity:** InfoSec protects all information, digital and physical; cybersecurity protects digital information and is a subset of InfoSec.
- **CIA concerns and the controls that address them**
  | Goal | Concern | Control |
  |---|---|---|
  | Confidentiality | Snooping, dumpster diving, wiretapping, social engineering | Clean-desk policy, shredding, encryption, awareness training |
  | Integrity | Unauthorised modification, impersonation, MITM, replay | Least privilege, user education, encryption |
  | Availability | Power outages, hardware failure, destruction, service outages | Generators, redundant components, backup data centres, resilient design |
- **Access control process (AAA):** Identification (username, a claim) -> Authentication (password, proof) -> Authorization (ACLs, what you may do) -> Accounting (logging what you did).
- **Password controls:** length, complexity, expiry and history requirements.
- **MFA:** something you know + something you have + something you are.
- **Non-repudiation:** digital signatures prevent someone from denying an action.
- **Private data types:** PII (anything tied to a person) and PHI (health records, regulated by HIPAA).

### Threat, vulnerability, risk
- **Threat** - a possible malicious act; can be intentional, unintentional (human error) or natural.
- **Vulnerability** - a weakness in design, procedures or controls.
- **Threat + Vulnerability = Risk.** Risk can never be zero; the goal is to keep it within the organisation's tolerance.
- **Prioritising risk** by likelihood and impact: high/high = priority 1, low-likelihood/high-impact = 2, high/low = 3, low/low = 4.
- **Example assessment from the course:** phishing (likelihood high, impact medium), zero-day (low, medium), ransomware (medium, high), DoS (medium, low).
- **Four risk treatments:** avoid, transfer (e.g. insurance), mitigate (controls), accept (when fixing costs more than the risk itself).
- **Defense in depth:** overlapping layers - physical, network, endpoint, application, data, IAM, policies, and monitoring - so one failed control does not mean a breach.

### Information gathering (reconnaissance)
"If you know the enemy and know yourself, your victory will not stand in doubt." Attackers recon to plan; defenders recon to see what an attacker would see.
- **Passive (no direct contact, OSINT):** WHOIS, DNS records (`dig`, `nslookup`), certificate-transparency logs (crt.sh) and subdomain tools (Sublist3r, Amass), Google dorking, theHarvester, Shodan/Censys, breach-exposure checks, job ads and news articles.
- **Active (touches the target, detectable):** host discovery and port/version scans with Nmap, banner grabbing, web scanning (Nikto, directory brute-forcing), and SMB/FTP/SNMP enumeration - only ever against targets I am authorised to test.

### Common threat vectors and attack methods
- **Phishing family:** email phishing, vishing (voice), smishing (SMS), pharming (fake site), whaling (high-profile targets).
- **Malware:** virus (attaches to an executable), worm (self-replicates over networks), trojan (hidden inside something wanted), logic bomb (waits for a trigger), ransomware (encrypts and extorts), plus spyware, adware and scareware.
- **Social engineering:** hoaxes, shoulder surfing, dumpster diving.
- **Availability attacks:** DoS and DDoS, usually launched from a **botnet** of compromised "zombie" devices run by a botmaster.
- **Network attacks:** sniffing, spoofing (MAC/IP), man-in-the-middle.
- **Web and account attacks:** SQL injection, cross-site scripting, credential stuffing (reused passwords), malvertising, spam.

## Assignment completed
| # | Assignment | Focus |
|---|---|---|
| 5 | Information Gathering | passive and active recon against the course's practice target, findings documented |

## Key takeaways
- Most attacks start with information that was already public. Reducing what is exposed is a real defence.
- Thinking in terms of likelihood x impact makes it clear which risks to fix first.
