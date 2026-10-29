# Day 2 — Module 2 Finish + Module 3 Starts: WannaCry Simulation & Intro to Linux

**Date:** 09 Oct 2026 · **Lectures:** M2 part 2 (WannaCry test env + execution, 52m) + M3 Intro to Linux (32m)

> All hands-on work below was done only in my own isolated lab VMs or on the course's dedicated TryHackMe rooms, for learning purposes.

## Covered today
### WannaCry attack simulation (lab walkthrough)
Studied the end-to-end simulation in an isolated NAT lab: a **Kali** attacker and a **Windows 7** victim.
- **Scanning:** used Nmap to find the victim and confirm SMB (port 445) open on an unpatched Windows 7 host.
- **Exploitation:** the EternalBlue module for MS17-010 was used to get a reverse shell on the victim.
- **Payload:** the WannaCry sample was transferred and executed, encrypting the victim's files and dropping the ransom note.
- **Point of the exercise:** see the full lifecycle — recon → exploit → payload — and then reason about the defences that break each stage.

### Introduction to Linux
- Linux = open-source, Unix-like OS built on the Linux kernel (Linus Torvalds, 1991).
- **Architecture:** kernel, system libraries, system utilities, shell, hardware layer.
- Why it matters for security: lightweight, open source, powers most servers/infrastructure, and is the home of pentesting distros.
- **Kali Linux:** Debian-derived distro built for pentesting/forensics, 600+ preinstalled tools, maintained by Offensive Security.

## Key takeaways
- The same recon→exploit→payload chain shows up again in Modules 4–6; WannaCry is just the first concrete example.
- Getting comfortable in Linux early is essential — every later tool (Nmap, Metasploit, Burp, Splunk) runs from the terminal.
