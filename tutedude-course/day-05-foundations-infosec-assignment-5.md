# Day 5 — Module 4: Foundations of Information Security + Assignment 5

**Date:** 12 Oct 2026 · **Lectures:** Information Gathering (34m), Common Threat Vectors (29m), Modern Attack Methodologies (37m) · **Assignment:** 5 · *Module 4 complete ✅*

> All hands-on work below was done only in my own isolated lab VMs or on the course's dedicated TryHackMe rooms, for learning purposes.

## Covered today
### Core concepts
- **CIA triad** and its concerns/controls (snooping→clean-desk, MITM→encryption, etc.).
- **AAA:** Identification → Authentication → Authorization → Accounting.
- **Threat + Vulnerability = Risk**; goal is to *manage* risk, not eliminate it.

### Attacker profiles
Script kiddies, hacktivists, cybercriminals, state-sponsored, insiders, organised crime, cyberterrorists.

### Cyber Kill Chain
Reconnaissance → Weaponization → Delivery → Exploitation → Installation → Command & Control → Actions on Objectives. Breaking any one stage stops the attack.

### Information gathering (recon)
- **Passive (OSINT, undetectable):** WHOIS, `dig`/`nslookup`, crt.sh/Sublist3r subdomains, Google dorking, theHarvester, Shodan, breach checks.
- **Active (detectable):** `nmap -sn` host discovery, SYN/version/OS scans, banner grabbing, `nikto`, SMB/FTP/SNMP enumeration.

### Threats & malware
Phishing family (vishing, smishing, pharming, whaling), malware types (virus, worm, trojan, logic bomb, ransomware), DoS/DDoS, MITM, botnets, Wi-Fi attacks, and APTs.

## Assignment completed (approved)
| # | Task | Focus |
|---|------|-------|
| 5 | Information Gathering | passive + active recon against the course target; findings documented |

**Proof:** `Assignment 5.zip`
