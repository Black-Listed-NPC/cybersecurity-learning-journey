# Day 13 - Module 6 (Part 3): Nmap, Black Box and Grey Box VAPT

**Date:** 20 Oct 2026 (Dussehra - holiday, longer study session)
**Module:** Module 6 - Network Defense and Penetration Testing (part 3 of 4)
**Study time:** 2h 34m

| Lecture | Duration |
|---|---|
| Scanning: Nmap Service Discovery | 32m |
| Hands On: End-to-End Black Box VAPT | 1h 11m |
| Hands On: End-to-End Grey Box VAPT | 51m |

> All scanning below was done only against my own isolated lab VMs (Metasploitable 2 on a host-only network), for learning purposes.

## Covered today

### Nmap service discovery
**Workflow:** host discovery -> port scan -> service and version detection -> targeted NSE scripts -> save output -> map findings to known vulnerabilities.

| Command | Purpose |
|---|---|
| `nmap -sn 192.168.56.0/24` | Find live hosts |
| `nmap -sS -sV -p- -Pn <lab-ip>` | SYN scan of all 65,535 ports with version detection, skipping ping |
| `nmap -sC -sV <lab-ip>` | Default safe scripts and versions |
| `nmap -sS -sV -p21,22,80,443,445 <lab-ip>` | Only the chosen ports |
| `nmap --script vuln <lab-ip>` | Checks for known CVEs and weak configuration |
| `nmap -A <lab-ip>` | OS detection, versions, scripts, traceroute |
| `nmap -T3` / `-T4` | Timing: T3 normal, T4 for labs; avoid T5 on real networks |
| `-oN scan.txt -oX scan.xml` | Save output for the report |

**Reading the output:** `PORT / STATE / SERVICE / VERSION`. `open` means a service is listening; `filtered` usually means a firewall is in the way. The **version** is what links a service to known CVEs.

**NSE categories:** `auth`, `vuln`, `discovery`, `brute`, `exploit`. Start with `-sC`, then run targeted `--script` scans against the services you found.

### Hands-on: Black Box VAPT with Nessus
Nessus Advanced Scan, configured as an unauthenticated assessment:
1. New Scan -> Advanced Scan; name it after the asset.
2. **Discovery:** host ping turned off (some hosts block ICMP), port range set to all ports (1-65535).
3. **Assessment:** web application tests enabled.
4. **Credentials:** left empty on purpose - this is what makes it a black-box, outsider view.
5. Launch, then review the findings by severity.

Metasploitable 2 lit up with many critical issues. Grouped by root cause:
| Root cause | Examples on the lab VM | Remediation |
|---|---|---|
| Outdated or backdoored software | Old FTP, IRC and Samba versions | Update or replace; verify checksums |
| Default or weak credentials | Database, Tomcat manager, SSH, VNC | Change all defaults; enforce strong passwords |
| Cleartext protocols | Telnet, rlogin/rsh, plain FTP | Disable them; use SSH with key-based authentication |
| Unnecessary exposed services | Bind shell, distcc, RPC, NFS exports | Disable unused services; restrict NFS and enable root-squash |
| Misconfiguration | DNS zone transfer allowed, SMTP user enumeration | Restrict AXFR; disable VRFY/EXPN |

**Rule from the course handbook:** when validating, prove the issue with **read-only evidence** (who am I, hostname) - do not change files - and always explain *why* it worked and *how* to fix it.

### Hands-on: Grey Box VAPT
**Linux - credentialed patch audit (Nessus)**
- Prerequisites: SSH (22) reachable, a root or sudo-capable account, the correct OS identified.
- Scan template: Credentialed Patch Audit, with SSH credentials (password or key) and "elevate privileges with sudo" turned on.
- Result: the exact missing patches and unsupported package versions, which an unauthenticated scan cannot see.

**Linux - policy compliance audit (Nessus)**
- Template: Policy Compliance Auditing, with an `.audit` file that matches the OS (for example the CIS Ubuntu 20.04 or CIS RHEL 8 benchmark).
- Result: pass/fail per CIS control - password policy, services, logging, file permissions.

**Windows - configuration audit with HardeningKitty**
- A PowerShell module that runs **read-only** checks of local security policy, registry and system settings against hardening benchmarks.
- `Invoke-HardeningKitty -Mode Audit -Log -Report` produces a CSV report and a log file as audit evidence, without changing the system.

**Grey Box deliverables:** vulnerability report, CIS compliance report, patch audit summary, configuration audit summary.

## Key takeaways
- Black Box is the outsider's view. A credentialed Grey Box scan finds missing patches and configuration drift you cannot see from outside.
- Findings only help when they are prioritised by risk and come with a clear fix.
