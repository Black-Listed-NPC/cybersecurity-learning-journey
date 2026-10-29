# Day 19 - Module 12: SIEM Architecture and Hands-On Splunk

**Date:** 26 Oct 2026
**Module:** Module 12 - SIEM Architecture and Hands-On Splunk (complete)
**Study time:** 2h 26m

| Lecture | Duration |
|---|---|
| Setting Up Splunk (Installation and Configuration) | 36m |
| Investigating Phishing Attack on Splunk | 55m |
| Wazuh Installation and Bruteforce Incident | 55m |

> All hands-on work below was done only in my own home lab VMs, for learning purposes.

## Covered today

### Why a SIEM
A SIEM collects logs from every source into one place, indexes them, and lets the SOC search, correlate, visualise and alert. Splunk was chosen for centralised log management, powerful search and detection rules, and the ability to scale.

### Splunk architecture
| Component | Role |
|---|---|
| **Universal Forwarder** | Lightweight agent on the endpoint; collects logs and sends them on |
| **Indexer** | Parses data into field-value pairs, works out the data type, stores events |
| **Search Head** | Where analysts search with SPL and build tables, charts and dashboards |

Small networks do not need a heavy forwarder - the universal forwarder can send straight to the Splunk server.
**Getting data in:** Upload (one-time files), Monitor (watch files and folders), Forward (from remote hosts).

### Home SOC lab build
- **Server:** Splunk Enterprise on an Ubuntu VM.
  ```bash
  sudo apt update && sudo apt upgrade -y
  sudo dpkg -i splunk-<version>-linux-amd64.deb
  sudo /opt/splunk/bin/splunk start --accept-license
  sudo /opt/splunk/bin/splunk enable boot-start
  ```
- **Ports:** 8000 (web UI), 8089 (management), 9997 (receiving logs from forwarders).
- In Splunk Web: Settings > Forwarding and Receiving > receive on **9997**; Settings > Indexes > create index `windows11`.
- **Endpoint:** a Windows 11 VM with the Universal Forwarder (.msi), pointed to the Ubuntu IP (management 8089, receiving 9997), sending the System, Security and Application event logs.
- **Verify:** Settings > Forwarder Management shows the host; `index=windows11` returns events. The lab works.

### SPL searches I practised
```spl
index=windows11 EventCode=4625
| stats count by Account_Name, Source_Network_Address
| sort -count

index=windows11 EventCode=4624 Logon_Type=10
| table _time, Account_Name, Source_Network_Address

index=windows11 (EventCode=4720 OR EventCode=4732)
| table _time, EventCode, Account_Name
```
| Event ID | Meaning |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4688 | New process created |
| 4720 | User account created |
| 4732 | User added to a security-enabled local group |

### Investigating a phishing attack in Splunk
How the investigation went: start from the reported email (sender, subject, links, attachment) -> search mail and proxy logs for everyone who received it or clicked -> pivot to endpoint logs for anything the attachment launched (new processes, PowerShell) -> check outbound connections to the malicious domain or IP -> build a timeline and list the IOCs (sender, domains, hashes, IPs) to block.

### Wazuh and a brute-force incident
- **Wazuh** is an open-source SIEM/XDR: manager, indexer, dashboard, and agents on the endpoints.
- After installing the server and enrolling an agent, a lab brute-force attempt against the endpoint showed up as a burst of authentication-failure alerts.
- **Detection logic:** many **4625** failures from one source in a short time = brute force; a **4625 burst followed by a 4624** from the same source = a likely successful compromise that needs escalation.
- **Response:** block the source, reset or lock the account, check what happened after the successful logon, and add MFA and lockout policies.

## Key takeaways
- A SIEM is how a SOC sees everything at once: collect -> index -> search -> correlate -> alert.
- The value is in the searches and correlation rules, not the installation. Knowing which Event IDs matter is half of log analysis.
- Module 12 complete.
