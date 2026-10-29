# Day 12 - Module 6 (Part 2): Network Security, Attacker Profiles, Kill Chain and Lab Build

**Date:** 19 Oct 2026
**Module:** Module 6 - Network Defense and Penetration Testing (part 2 of 4)
**Study time:** 1h 48m

| Lecture | Duration |
|---|---|
| Network Security Concepts | 36m |
| Attacker Profiles and Cyber Kill Chain | 39m |
| Black Box vs Grey Box VAPT | 14m |
| Nessus Installation and Setup | 8m |
| Setting Up Metasploitable in VirtualBox | 11m |

> All hands-on work below was done only in my own isolated lab VMs, for learning purposes.

## Covered today

### Network security concepts
- **Perimeter and internal controls:** firewalls between trust zones, a DMZ for public-facing servers, VLAN segmentation inside the network, and VPNs for remote access.
- **Detection:** IDS/IPS watching traffic; logs from network devices sent to a central SIEM.
- **Wi-Fi configuration that matters:** SSID broadcasting, security protocol (WPA3 > WPA2; never WEP), strong password, network mode, guest network isolation, MAC filtering (weak on its own), and remote management turned off.
- **Wi-Fi attacks:** rogue access points, evil twin, man-in-the-middle, password cracking (brute force, dictionary, rainbow tables), deauthentication attacks, eavesdropping, WPS weaknesses, KRACK.
- **Wi-Fi defences:** WPA3, firmware updates, strong unique passwords, no default router credentials, WPS disabled, monitoring for unknown access points.

### Attacker profiles and motivations
| Profile | Motivation / traits |
|---|---|
| Script kiddies | Limited skill, run ready-made tools, go after easy targets |
| Hacktivists | Political or social causes, want publicity |
| Cybercriminals | Money: malware, phishing, identity theft, fraud, extortion |
| State-sponsored | Espionage and geopolitics; highly skilled, hard to attribute |
| Insiders | Already have access; can be malicious or careless |
| Organised crime groups | Structured, well-funded, financially driven |
| Cyberterrorists | Disrupt critical infrastructure to cause fear |

**Insider-risk controls:** access controls, security awareness training, monitoring and auditing, an incident response plan, and employee support.

### Cyber Kill Chain
| Stage | What the attacker does | Where defenders can break it |
|---|---|---|
| 1. Reconnaissance | Gathers information (passive and active) | Limit public exposure, detect scans |
| 2. Weaponization | Turns a vulnerability into a payload | Threat intelligence |
| 3. Delivery | Email, web, USB, social engineering | Email filtering, user awareness |
| 4. Exploitation | Triggers the vulnerability | Patching, hardening |
| 5. Installation | Persistence, backdoors | EDR, application allow-listing |
| 6. Command and Control | Remote channel to the compromised host | Egress filtering, DNS/proxy monitoring |
| 7. Actions on Objectives | Exfiltration, lateral movement, damage, covering tracks | DLP, segmentation, logging |

### Advanced Persistent Threats (APT)
- **Advanced** - custom tools and sophisticated methods.
- **Persistent** - stays hidden for months or years with a "low and slow" approach.
- **Threat** - deliberate, well-funded (often nation-state) and aimed at serious damage.

### VAPT: Black Box vs Grey Box
| | Black Box (unauthenticated) | Grey Box (authenticated) |
|---|---|---|
| Tester knows | Nothing - no credentials or internal details | Valid credentials are provided |
| Simulates | An outsider, or an insider with network access only | An authenticated user, and host-level review |
| Finds | Open ports, exposed services, weak network controls | Missing patches, CIS benchmark gaps, weak configuration |
| Steps | Information gathering -> enumeration -> vulnerability discovery -> optional validation -> reporting | Credential setup -> authenticated scan -> CIS audit -> patch audit -> reporting |

- A real engagement starts with a signed **scope document** listing exactly which IPs, applications and test types are allowed. The course showed a sample annexure to explain this.

### Lab build
- Installed **Nessus** (vulnerability scanner) in the lab.
- Deployed **Metasploitable 2**, a deliberately vulnerable Linux VM made for training, on a host-only network that cannot reach my real network or the internet.

## Key takeaways
- Every stage of the kill chain is a chance to detect or stop an attack - defence does not have to win at the first step.
- Black Box answers "what can an outsider see?"; Grey Box answers "how well is each host hardened?"
