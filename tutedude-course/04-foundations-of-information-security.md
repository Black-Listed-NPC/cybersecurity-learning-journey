# Day 4 – Module 4: Foundations of Information Security

**Course:** Tutedude Cybersecurity
**Module 4 done:** 3/3 lectures (1h 40m): Information Gathering, Common Threat Vectors, and Modern Attack Methodologies.

**Contents**
1. [Information security basics](#1-information-security-basics)
2. [Attacker profiles](#2-attacker-profiles)
3. [Cyber Kill Chain](#3-cyber-kill-chain-cyber-attack-strategy)
4. [Information gathering (recon)](#4-information-gathering-recon)
5. [Common attacks and malware](#5-common-threat-vectors-attacks-and-malware)
6. [Wi-Fi configuration and attacks](#6-wi-fi-configuration-and-attacks)
7. [Advanced Persistent Threats](#7-advanced-persistent-threats-apt)
8. [Risk management and defense in depth](#8-risk-management-and-defense-in-depth)
9. [My own words and things to explore](#9-my-own-words)

---

## 1. Information security basics

**InfoSec** protects all information, digital and physical. **Cybersecurity** protects digital information (computers, handhelds, cloud, networks) and is a **subset** of InfoSec.

### CIA triad

| Goal | Meaning | How it is achieved |
|------|---------|--------------------|
| **Confidentiality** | Only authorised people can see data | Passwords, locks, tokens, classification, encryption, MFA |
| **Integrity** | Data is not changed without permission | Tracking and limiting changes, hashing, digital signatures |
| **Availability** | Systems and data stay accessible | Redundancy, fault-tolerant hardware, backups |

### Concerns and the control that protects against each

| Goal | Concern | Protection |
|------|---------|-----------|
| Confidentiality | Snooping (info left in the open) | Clean desk policy |
| Confidentiality | Dumpster diving | Shredding |
| Confidentiality | Wiretapping | Encryption |
| Confidentiality | Social engineering | Education and training |
| Integrity | Unauthorised modification | Principle of **least privilege** |
| Integrity | Impersonation | User education |
| Integrity | Man-in-the-Middle (MitM) | Encryption |
| Integrity | Replay (captured logins reused) | Encryption |
| Availability | Power outages | Redundant power, backup generators |
| Availability | Hardware failure | Redundant components |
| Availability | Destruction | Backup data centres (for example cloud) |
| Availability | Service outages | Resilient systems |

### Key definitions

- **Threat:** a malicious act, or the possibility of one, that seeks to steal or damage data or disrupt a system. Examples: viruses, DoS, data breaches, dishonest employees.
  - *Intentional:* malware, phishing, illegal account access
  - *Unintentional:* human error, for example forgetting to update the firewall or antivirus
  - *Natural:* disasters that damage data
- **Vulnerability:** a flaw in design, procedures or controls that can be exploited.
- **Risk:** the potential loss or damage if a threat exploits a vulnerability. It can't be removed completely, only managed. The goal is not a risk-free system but keeping risk as low as possible.

> **Threat + Vulnerability = Risk**

- **Types of risk:** *external* (attacks, phishing, ransomware, DDoS) and *internal* (insiders who are malicious or just untrained).

### Authentication and authorisation (AAA)

| Step | Meaning | Typical example |
|------|---------|-----------------|
| **Identification** | Claiming an identity (can be false) | Username |
| **Authentication** | Proving the claim | Password |
| **Authorisation** | Checking the action is allowed | Access control lists (ACLs) |
| **Accounting** | Tracking activity (login time, data sent, IP, services used) | Logs |

- **Password controls:** length, complexity, expiration, history (no reuse of old passwords).
- **MFA (3 factors):** something you **know**, something you **have**, something you **are**. Combining them gives multi-factor authentication.
- **Non-repudiation:** prevents someone denying an action. Digital signatures use encryption for this, and biometrics and video surveillance also help.

### Privacy

- **PII:** any information tied back to an individual.
- **PHI:** health records, regulated by HIPAA.
- Organisations must protect their own data, educate users, and protect data entrusted to them (such as client data).

---

## 2. Attacker profiles

| Profile | Key points |
|---------|-----------|
| **Script kiddies** | Low skill, use automated tools, little originality, pick easy targets, limited scope, no ethics |
| **Hacktivists** | Motivated by ideals, political or social activism, civil disobedience, want publicity, rely on anonymity |
| **Cyber criminals** | Money-driven: hacking, malware, phishing, identity theft, fraud, DDoS, data breaches, extortion, black-market sales |
| **State-sponsored** | Highly sophisticated, espionage, geopolitical motives, hard to attribute, often run APTs |
| **Insiders** | Authorised users (employees) who misuse access, intentionally or accidentally |
| **Organised cybercrime groups** | Structured, large scale, financial gain or power. Examples named: Russian syndicates, Chinese APT groups, North Korean groups |
| **Cyberterrorists** | Target critical infrastructure to cause chaos, panic and disruption. Politically or ideologically motivated |

**Defending against insiders:** access controls, security awareness training, monitoring and auditing, incident response planning, employee support.

---

## 3. Cyber Kill Chain (cyber-attack strategy)

Unauthorised access means using systems, networks or data without permission. The attack follows 6 stages:

| # | Stage | What happens | Key ideas |
|---|-------|--------------|-----------|
| 1 | **Reconnaissance** | Attacker gathers info about the target to plan and tailor the attack | Passive and active recon |
| 2 | **Weaponization** | Vulnerabilities are turned into malicious payloads or cyber weapons | Malicious payloads, delivery mechanisms, social engineering, customisation |
| 3 | **Exploitation** | Attacker uses a vulnerability to gain access or run code | Vulnerability exploitation, payload delivery, **privilege escalation**, post-exploitation actions |
| 4 | **Installation** | Attacker establishes a foothold on the system | Persistence, backdoors, remote access, privilege escalation, **lateral movement** |
| 5 | **Command & Control (C2)** | Communication channel between attacker and compromised systems | Botnets, persistence, post-exploitation. Detect and disrupt C2 traffic |
| 6 | **Actions on Objectives** | Attacker carries out the real goal | Data exfiltration, lateral movement, privilege escalation, staging further attacks, damage and disruption, **covering tracks**, continued persistence |

Why it matters for defence: stopping the attacker at **any** stage breaks the chain.

---

## 4. Information gathering (recon)

> *"If you know the enemy and know yourself, your victory will not stand in doubt."* (Sun Tzu). An attacker needs to know the target. A defender needs to know what the attacker will discover.

### Passive recon (no direct contact, not detectable)
Like looking at the target's territory from afar. Examples: public DNS lookups, job ads, news articles about the company.

| Task | Command / tool |
|------|----------------|
| WHOIS | `whois target.com` |
| DNS records | `dig target.com`, `dig -t MX target.com`, `dig -t TXT target.com`, `nslookup target.com` |
| Subdomains | `sublist3r -d target.com`, `amass enum -d target.com`, crt.sh (certificate transparency) |
| Google dorking | `site:target.com filetype:pdf confidential`, `site:target.com intitle:"index of"`, `site:target.com "password"` |
| Emails, domains | `theHarvester -d target.com -b all` |
| Tech stack | `whatweb target.com` |
| Breach exposure | haveibeenpwned.com, breachdirectory.org, public GitHub leaks |
| Exposed devices | Shodan (`shodan search "target.com"`), Censys |

### Active recon (direct contact, detectable)
Like checking the locks on doors and windows. Examples: connecting to HTTP/FTP/SMTP servers, calling the company (social engineering), entering the premises pretending to be a repairman.

| Task | Command / tool |
|------|----------------|
| Host discovery (ping sweep) | `nmap -sn 192.168.1.0/24` |
| Port scan (SYN) | `nmap -sS -p 1-1000 target.com` |
| Service version | `nmap -sV target.com` |
| OS detection | `nmap -O target.com` |
| Aggressive scan | `nmap -A target.com` |
| Banner grabbing | `nc -v target.com 80` then `HEAD / HTTP/1.0`; `nc -v target.com 22` |
| Web vulnerability scan | `nikto -h http://target.com` |
| Directory brute force | `gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt` |
| Web proxies | OWASP ZAP, Burp Suite |
| SMB shares | `smbclient -L \\target.com -N` |
| FTP anonymous login | `ftp target.com` (user `anonymous`) |
| SNMP | `snmpwalk -v2c -c public target.com` |
| Human recon | Vishing calls, phishing simulations |

> Only run active scans on systems you own or have written permission to test.

---

## 5. Common threat vectors: attacks and malware

### Phishing family

| Attack | Meaning |
|--------|---------|
| **Phishing** | Deceptive messages that trick people into revealing sensitive info |
| **Vishing** | Phishing by voice call (steal card numbers or identity) |
| **Smishing** | Phishing by SMS, usually with a malicious link |
| **Pharming** | Impersonating a legitimate website to steal credentials |
| **Whaling** | Phishing aimed at high-profile targets (executives, politicians, celebrities) |

### Malware types

| Type | Key points |
|------|-----------|
| **Virus** | Malicious code attached to another executable file or legitimate program |
| **Worm** | Self-replicates by exploiting vulnerabilities and needs no user action after the first infection. It slows networks and computers. WannaCry spread this way |
| **Trojan horse** | Does malicious things while pretending to be something useful, such as a game. The slides say it attaches to non-executable files such as images and audio |
| **Logic bomb** | Malicious code that waits for a trigger before activating, and can damage hardware components |
| **Ransomware** | Encrypts the victim's data with a key they don't have and demands payment, usually untraceable |
| **Spyware / adware / scareware** | Also named in the slides as malware types |

### Other attacks

| Attack | Key points |
|--------|-----------|
| **Social engineering** | Manipulates people into revealing info or acting unsafely. It exploits psychology, trust and natural behaviour |
| **Hoaxes** | Fake news, false virus alerts that tell you to delete files, fake competitions. They can be as disruptive as real breaches |
| **Shoulder surfing** | Watching someone enter PINs, codes or card numbers |
| **Dumpster diving** | Searching trash for sensitive info. Dispose of it properly (shred) |
| **DoS** | Interrupts network services so authorised users can't access them |
| **DDoS** | DoS from many coordinated sources, using a **botnet** |
| **Botnet** | Network of compromised devices ("bots" or "zombies") controlled by a **botmaster**. Can have thousands or millions of devices, and owners don't know |
| **SQL injection** | Attacker inserts SQL into web input fields. It exploits poorly sanitised input to run unauthorised queries and gain access to the database |
| **Sniffing** | Capturing all network traffic passing through the NIC, even traffic not addressed to you |
| **Spoofing** | Impersonating a trusted system (MAC address spoofing, IP spoofing) |
| **Man-in-the-Middle** | Intercepting communication between two parties to steal or alter information |
| **XSS (Cross-Site Scripting)** | Injecting malicious scripts into a web app that doesn't validate content before showing it to users |
| **Credential stuffing** | Reusing stolen username and password pairs on other sites, relying on password reuse |
| **Malvertising** | Malware delivered through legitimate-looking online ads |
| **Spamming** | Bulk unsolicited messages, often used to promote or deliver scams |

---

## 6. Wi-Fi configuration and attacks

### Configuration items
- **SSID:** the network name. Broadcasting it has security implications, and it can be spoofed.
- **Security protocols:** rules for secure communication (encryption, authentication, key exchange, integrity, access control, wireless protocols).
- **Password:** access control. Covers password policy, MFA, hashing, management, account recovery and password attacks.
- **Network mode:** router, bridge, access point, client, gateway, **monitor** and **promiscuous** modes.
- Also: channel selection, guest network, MAC address filtering, remote management.

### Wi-Fi attacks

| Attack | Meaning |
|--------|---------|
| **Rogue access point** | Unauthorised AP on the network. It can enable MitM and give unauthorised guests access |
| **Man-in-the-Middle** | Secretly intercepts, alters or relays communication. Public Wi-Fi is high risk. Digital certificates help |
| **Evil twin** | Fake AP that mimics a trusted network but is attacker-controlled. Used for interception, credential theft and phishing |
| **Password cracking** | Brute force, dictionary, rainbow tables, credential stuffing. **Salting** defends against rainbow tables |
| **Deauthentication** | Forged deauth frames disconnect users. This disrupts the network and can set up MitM or evil twin attacks |
| **Eavesdropping** | Passively capturing communication without consent |
| **WPS vulnerabilities** | Weaknesses in Wi-Fi Protected Setup |
| **KRACK** | Attack on the WPA2 key handshake |

### How to avoid Wi-Fi attacks
- Use strong protocols such as **WPA3**
- Update router firmware regularly
- Use strong, unique Wi-Fi passwords and change default router credentials
- Disable WPS if not needed
- Monitor the network for suspicious activity

---

## 7. Advanced Persistent Threats (APT)

- **Advanced:** advanced malware and exploits, skilled attackers who can build new tools, and access to surveillance, satellite imagery and even human intelligence.
- **Persistent:** can last years. Uses a **"low-and-slow"** approach to avoid detection. Well organised and well funded (a nation-state or organised crime).
- **Threat:** deliberate and focused, not opportunistic. Aims for real damage: financial loss, destroyed systems and infrastructure, even physical harm.

---

## 8. Risk management and defense in depth

### Risk assessment
- A process that evaluates an organisation's defences, identifies vulnerabilities, and determines the **likelihood** and **impact** of each threat. The output is a prioritised list of vulnerabilities.
- **Benefits:** lower long-term costs, fewer breaches, fewer regulatory issues, less downtime, less data loss.
- **Prioritising example:** 1 = high probability and high impact, 2 = low probability and high impact, 3 = high probability and low impact, 4 = low probability and low impact. Fix 1s first.

| Example risk | Likelihood | Impact |
|--------------|-----------|--------|
| Phishing | High | Medium |
| Zero-day vulnerabilities | Low | Medium |
| Ransomware | Medium | High |
| DoS | Medium | Low |

### 4 ways to treat risk

| Treatment | Meaning | Example |
|-----------|---------|---------|
| **Avoidance** | Change practices so the risk is irrelevant | Stop using vulnerable software |
| **Transference** | Shift the impact to another party (the risk still exists) | Insurance policy |
| **Mitigation** | Reduce likelihood or impact | Firewalls, IDS, encryption |
| **Acceptance** | Carry on despite the risk. Use when mitigation costs more than the risk | Don't spend £200,000 to prevent a £20,000 risk |

### Defense in depth
Overlapping layers of security with a common objective:

| Layer | Examples |
|-------|----------|
| Physical | Guards, cameras, locked server rooms, biometrics |
| Network | Firewalls, IDS/IPS, VPNs, segmentation |
| Endpoint | Antivirus, EDR, patching, device encryption |
| Application | WAF, secure coding, app testing, updates |
| Data | Encryption (at rest and in transit), access controls, masking, backups |
| IAM | MFA, SSO, RBAC, user provisioning and de-provisioning |
| Policies and procedures | Security policies, incident response plan, training, compliance |
| Monitoring and detection | SIEM, continuous monitoring, log management, anomaly detection |

**Scenario from the slides:** an attacker is stopped at every layer. Biometric locks stop physical access, the firewall and IDS/IPS stop network entry, EDR blocks malware on the workstation, the WAF blocks the web exploit, encryption makes stolen data useless, MFA and RBAC stop privilege escalation, and the incident response plan plus monitoring catch the rest.

---

## 9. My own words

### Things I found interesting / want to explore more
- Try the passive recon commands (`whois`, `dig`, `theHarvester`) on a safe and legal test domain.
- Look into how Shodan works in practice.
- Insiders are a real threat category, not just external hackers. I hadn't thought about that before.

### Summary
This module was about understanding *who* attacks us and *how* they plan it before they even touch the system. The CIA triad is the foundation everything else builds on. Recon (passive vs active) is the first real step of any attack. Passive is quiet and hard to trace, while active is more direct but can get you caught. Phishing in all its forms is still one of the easiest ways in because it targets people, not code.

### Key takeaways
1. Threat + vulnerability = risk. The goal is to manage risk, not eliminate it.
2. The kill chain has 6 stages, and breaking any one stage stops the attack.
3. Humans are often the weakest link, so training matters as much as tools.
4. Defense in depth means no single control is relied on alone.
