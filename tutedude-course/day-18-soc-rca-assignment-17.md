# Day 18 - Modules 10 and 11: SOC Operations, Incident Response and Forensics + Assignment 17

**Date:** 25 Oct 2026
**Modules:** Module 10 - Security Operations Center: Overview and Roles (complete), Module 11 - RCA and Cyber Breach Investigation (complete)
**Study time:** 4h 07m
**Assignment:** 17

| Lecture | Module | Duration |
|---|---|---|
| SOC Operations: People, Processes, and Defense | M10 | 41m |
| Advanced Detection Frameworks and Splunk | M10 | 33m |
| Incident Response Management | M11 | 1h 17m |
| Digital Forensics Process | M11 | 1h 22m |
| Data Acquisition (Volatile and Non-Volatile) | M11 | 16m |

## Covered today

### Module 10 - Security Operations Center
- A **SOC** is a dedicated team that monitors the organisation's network and resources 24/7 to **detect** (unauthorised access, policy violations, intrusions) and **respond** (support incident response and root cause analysis).
- **Three pillars:** People, Process, Technology.
- **People - analyst tiers**
  | Tier | Job |
  |---|---|
  | L1 | First responders: alert triage, escalate real threats |
  | L2 | Deep investigation, correlating data from many sources |
  | L3 | Threat hunting; leads containment, eradication and recovery |
- **Process - alert triage with the 5 Ws:** What (type of activity), When (timestamp), Where (source host/IP), Who (user or account), Why (impact). Harmful alerts become tickets with all 5 Ws and screenshots, then are escalated.
- **Technology:** SIEM (collects and correlates logs; modern ones add UEBA, threat intelligence and ML), EDR (endpoint visibility and automated response), firewalls.
- People are what separate real threats from noise. Like a fire brigade that would waste the day on cooking-smoke alarms, a SOC that relies only on automation chases false positives.

**Advanced detection frameworks**
| | IOC (Indicator of Compromise) | IOA (Indicator of Attack) |
|---|---|---|
| Based on | Artifacts: hashes, IPs, domains, file names, registry keys | Behaviour: Word spawning PowerShell, many failed logins then a success |
| Timing | After compromise | Before or during the attack |
| Evasion | Easy (change the hash) | Hard |
| Use | Block known threats | Catch unknown attacks |

- **TTPs** (Tactics, Techniques, Procedures) describe *how* attackers operate; **MITRE ATT&CK** is the common catalogue of them.
- Put together: TTPs explain what the attacker is trying to do, IOAs catch how they behave, and IOCs confirm what they left behind.
- **Metrics:** **MTTD** (mean time to detect) and **MTTR** (mean time to respond). IOA/TTP-based detection lowers MTTD; clear playbooks and automation lower MTTR.
- **Splunk components** (preview of Module 12): Forwarder -> Indexer -> Search Head; data in by Upload, Monitor or Forward.

### Module 11 - Incident Response Management
- **Event vs incident:** a port scan in the firewall log is an *event*; the same scan leading to a compromise is an *incident*.
- **Incident types:** security (malware, phishing, web attacks), network (DDoS, MITM, lateral movement, C2), endpoint (privilege escalation, rootkits), data (leakage, exfiltration, misconfigured storage), insider.
- **Impact areas:** business, technical, legal and regulatory, reputational.
- **Information sources:** alerts (SIEM, EDR, IDS), logs (who, what, when, from where), and network flow (NetFlow, PCAP).
- **Unauthorised-access indicators:** logins from unusual locations, impossible travel, new admin accounts, access outside business hours, abnormal downloads. Response: disable accounts, reset passwords, review authentication logs, hunt for persistence.
- **IR lifecycle (NIST):**
  1. **Preparation** - a ready team, playbooks and a "jump bag" (acquisition software, bootable Linux, drives, network tap, laptop).
  2. **Detection and Analysis** - classify the incident by impact and extent.
  3. **Containment, Eradication and Recovery** - short-term containment without touching the disk (it must be imaged first), then imaging and long-term containment, removing attacker artifacts and fixing the root cause, then restoring and monitoring.
  4. **Post-incident activity** - a lessons-learned report and meeting covering what failed *and* what worked.
- **Do not tip off the attacker:** do not upload their binaries to public AV services or touch their IPs before containment is ready.
- A course example showed a rootkit hiding a process from one tool while another still revealed the open socket. Cross-check with more than one tool.

### Digital forensics process
- **Locard's exchange principle:** every contact leaves a trace. Opening one text file leaves evidence of the program, the file, the time and the user.
- **Chain of custody:** every handler, date, time and transfer of the evidence is documented.
- **Deleted files:** the metadata is marked free but the content remains until it is overwritten, so it can be recovered; with lost metadata, **file carving** can still recover the content.
- **Order of volatility:** CPU registers/cache -> RAM -> router data -> disk -> remote data -> network topology -> offsite backups.
- **Write blockers** (hardware or software) make evidence read-only and must be validated; **disk duplicators** image or clone drives; **Faraday bags** block signals to mobile devices.
- **Evidence sources:** desktops and laptops, servers, VMs, logs.
- **Logs:** system, application, network, security, audit and event logs. Centralise them (syslog or agents), sync time with NTP, store them tamper-proof. Analysis: baseline -> pattern -> correlation -> keyword search -> trends.

### Data acquisition
- **Volatile** (RAM, network connections, running processes) is collected first, live.
- **Non-volatile** (disks) is collected by **imaging** (disk to file) or **cloning** (disk to disk).
- Verify the original image with hashes, store it safely, and **do all analysis on copies**.

## Assignment completed
| # | Assignment | Focus |
|---|---|---|
| 17 | SSRF | Server-Side Request Forgery on a practice application - how a server can be tricked into making requests to internal resources, and how to prevent it (allow-lists, blocking internal ranges) |

## Key takeaways
- The attacks from Modules 5 and 6 are exactly what a SOC detects and what RCA reconstructs afterwards.
- Good IR means: do not alert the attacker, contain without destroying evidence, and fix the root cause so it cannot happen again.
- Modules 10 and 11 complete.
