> ⚠️ **Disclaimer:** All attacks and exploits documented here were performed strictly in an isolated, offline virtual lab environment (VirtualBox VMs) for educational purposes as part of a structured cybersecurity course. No real systems, networks, or data were targeted. This content is for learning and awareness only.
# Lecture 1-2: Intro to CyberSecurity + WannaCry Ransomware

**Date:** 08 Oct 2026

## What I learned today

Today I started the Tutedude cybersecurity course. The instructor Harshit Bhardwaj gave an intro about himself (SOC analyst, forensics guy) and then talked about the digital world we live in and how much data is floating around, which also means more chances for hackers.

He covered different types of cyber attacks like ransomware, malware, phishing, DDoS, MITM (man in the middle), and malvertising. Also explained the CIA triad which is basically the base of cybersecurity:
- **Confidentiality** – keep data private, only the right people should see it
- **Integrity** – data should not get changed/tampered without permission
- **Availability** – the system/data should be accessible when needed

Also learned about the 3 pillars of cybersecurity: People, Processes, Technology. Makes sense because even the best tech fails if people are careless (like clicking random links lol).

Then we got a roadmap of the whole course – Python & Linux basics, app security, network defense, GRC (governance risk compliance), SOC operations, SIEM tools like Splunk, and root cause analysis of breaches.

We also got a list of different cybersecurity job roles explained:
- **SOC Analyst** – sits and watches alerts 24/7, responds to incidents, uses tools like Splunk, IBM QRadar, Snort, CrowdStrike
- **Computer Forensic Analyst** – recovers and investigates digital evidence, used in legal cases, uses tools like EnCase, FTK, Autopsy
- **GRC Analyst** – makes sure company follows rules/regulations (GDPR, HIPAA), does risk assessments and audits
- **Penetration Tester (Ethical Hacker)** – legally hacks into systems to find weak points before real hackers do, uses Metasploit, Burp Suite, Nmap
- **Red Team vs Blue Team** – Red Team attacks (simulates hackers), Blue Team defends. Both are needed to keep testing real security.

## WannaCry Ransomware (the big topic)

This was the main case study. WannaCry is a ransomware that hit computers worldwide in 2017.

**How it works:**
- It's basically a worm + ransomware combo
- It spreads through a Windows vulnerability called **EternalBlue** (SMB protocol bug) – this exploit was actually built by a US intelligence agency before it leaked
- It can also spread through malicious email attachments
- Once it gets in, it locks/encrypts your files and adds **.WCRY** to the filename
- Shows a screen demanding payment in Bitcoin ($300, going up to $600) with a countdown timer
- Changes your desktop wallpaper to a scary message
- Drops a "Please Read Me" text file with payment instructions

**How to defend against it:**
- Keep Windows patched (specifically patch MS17-010)
- Block SMB ports (445, 139 etc) on the network edge
- Take regular backups, keep them offline
- Don't open random email attachments or click unknown links
- Disable macros in Office files
- If infected: disconnect from network immediately, don't pay, report to CERT-In

## Hands-on Lab: WannaCry Simulation

This was the practical part. We set up a small test lab to actually simulate the attack safely (not on real systems, just practice VMs).

**Setup:**
- Installed VirtualBox + Kali Linux as the attacker machine
- Used a Windows 7 VM as the victim machine
- Put both machines on the same NAT network so they could talk to each other

**The attack, step by step:**
1. **Scanning** – used `nmap -O <ip range>` on Kali to scan the network and find which machine had port 445 open (SMB) and was running an old/unpatched OS. Found the Windows 7 target.
2. **Exploiting** – opened Metasploit, searched for `ms17-010`, found the `eternalblue` exploit module, loaded it with `use exploit/windows/smb/ms17_010_eternalblue`, set the target IP (RHOSTS), and ran it. This gave a **meterpreter** shell (basically remote access to the victim machine).
3. **Confirming access** – once inside, checked `getuid` (confirmed NT AUTHORITY/SYSTEM access, meaning full control) and browsed the victim's files/desktop.
4. **Uploading & running WannaCry** – uploaded the WannaCry.exe sample to the victim machine and executed it using `execute -f WannaCry.exe`. Watched it encrypt all the files and show the ransom popup, exactly like a real attack.

## Things I found interesting / want to explore more
- How EternalBlue actually works at the packet level
- Why SMBv1 is still around on old systems even though it's so risky
- Want to try this same lab myself and take my own screenshots

## My own words summary
Basically WannaCry is a worm that finds unpatched Windows machines on a network, breaks in without even needing a password (because of a flaw in SMB), then encrypts all the files and demands bitcoin. The scary part is how fast it spreads on its own once it's inside one machine. The lab made it click for me — seeing nmap find the open port, then metasploit using that one exploit to get full system access, was honestly wild to watch happen live.
