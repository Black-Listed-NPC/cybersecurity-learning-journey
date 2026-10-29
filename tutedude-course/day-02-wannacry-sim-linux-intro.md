# Day 2 - Module 2 (Part 2) and Module 3 (Part 1): WannaCry Lab Study and Introduction to Linux

**Date:** 09 Oct 2026
**Modules:** Module 2 - Introduction (complete), Module 3 - Linux and Python Fundamentals (part 1)
**Study time:** 1h 24m

| Lecture | Module | Duration |
|---|---|---|
| WannaCry Attack (Setting up a Test Environment) | M2 | 21m |
| System Hacking and WannaCry Execution | M2 | 31m |
| Introduction to Linux | M3 | 32m |

> The WannaCry lesson was a recorded instructor demonstration in an isolated lab. My notes focus on the attack lifecycle and the defences.

## Covered today

### WannaCry lab - what the demonstration showed
**Scenario:** a mid-size hospital with an old, unpatched Windows PC in Radiology and a mostly "flat" network where every machine can reach every other machine. One weak machine becomes the entry point, and the worm then spreads to nursing-station PCs and a shared file server. Staff suddenly cannot open documents and ransom notes appear everywhere.

**Lab design (why it was built this way)**
- An attacker VM and a deliberately outdated Windows 7 victim VM on their own VirtualBox NAT network, completely separate from any real network.
- The victim held only dummy files, so the encryption could be observed safely.

**The attack lifecycle in three stages**
1. **Discovery** - a network scan reveals a host exposing SMB (TCP 445) on an old, unpatched Windows version.
2. **Exploitation** - the missing MS17-010 patch lets the attacker run code remotely with no password.
3. **Payload** - the ransomware runs, encrypts the files and displays the ransom demand.

**Where each stage could have been stopped**
| Stage | Defence that breaks it |
|---|---|
| Discovery | Network segmentation, host firewalls, no exposed SMB, IDS alerts on scanning |
| Exploitation | Patch MS17-010, disable SMBv1, retire unsupported OS versions |
| Payload / spread | EDR/antivirus, application allow-listing, offline backups, fast isolation of the infected host |

### Introduction to Linux
- **Operating system:** the program between the user and the hardware - file, memory and process management, I/O and devices.
- **Linux:** an open-source, Unix-like OS built on the Linux kernel (Linus Torvalds, 1991).
- **Architecture:**
  - **Kernel** - core functions and all communication between software and hardware.
  - **System libraries** - pre-compiled reusable code that programs call.
  - **System utilities** - small programs that each do one specialised job.
  - **Shell** - interprets my commands and passes them to the OS.
  - **Hardware layer** - CPU, RAM, disks.
- **Where Linux is used:** web servers, car infotainment, point-of-sale systems, traffic-light controllers and industrial sensors.
- **Distributions ("flavours"):** Ubuntu, Debian, Fedora, CentOS/RHEL, Kali, and others built for different purposes.
- **Linux vs Windows:** Windows uses drive letters (C:, D:) and fixed user types; Linux uses a single directory tree from `/`. The Linux source code is open, so bugs are found and fixed quickly, and Linux is a smaller malware target than Windows.
- **Kali Linux features:** 600+ preinstalled tools, free, open-source Git tree, FHS-compliant, 32/64-bit and ARM images (including Raspberry Pi).
- **First navigation commands:** `pwd`, `ls`, `cd`, `~` (home), `..` (parent), `mkdir`, `touch`, `cat`, `clear`.

## Key takeaways
- The same chain (find a weak host -> exploit -> run a payload) comes up again in Modules 4 to 6; WannaCry is the first concrete example.
- Every later tool (Nmap, Burp, Splunk, Wireshark) runs from the terminal, so getting comfortable with Linux early is essential.
