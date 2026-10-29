# Day 1 — Modules 1 & 2: Getting Started + Introduction

**Date:** 08 Oct 2026 · **Lectures:** M1 (3m) + M2 part 1 (1h25m)

Started the Tutedude Cybersecurity course. Day 1 covered how the mentorship works, choosing a cybersecurity career path, and the first half of the WannaCry case study.

## Covered today
- **Course intro & mentorship:** how to connect with mentors and resolve doubts.
- **Choose Your Cybersecurity Path:** the main role tracks — SOC/Blue Team, VAPT/Offensive, GRC, and Forensics/DFIR — and the skills each needs.
- **The CIA triad** as the foundation of everything: Confidentiality, Integrity, Availability.
- **WannaCry — introduction:** the 2017 ransomware worm, how it combined a ransomware payload with the **EternalBlue** SMB exploit (MS17-010) to self-propagate across unpatched Windows hosts, and why a flat, unpatched hospital-style network amplified the damage.

## Key takeaways
- Ransomware = encrypt victim files, then demand payment (WannaCry asked $300–$600 in Bitcoin, caused an estimated $4B+ in damage globally).
- The two parts of WannaCry: a **worm** (spreads via SMB) + a **ransomware package** (encrypts, appends `.WCRY`).
- Primary defences that would have stopped it: timely patching, network segmentation, disabling legacy SMBv1, and backups.

## Reflection
A strong opener — WannaCry is the perfect example of how one unpatched service plus a flat network turns a single infection into an organisation-wide outage. It framed why every later module (patching, VAPT, SIEM, IR) actually matters.
