# Assignment 15 — Task: Investigating an Attack
**Date:** 27 Oct 2026

Investigated a captured network traffic file (.pcap) containing an active ARP spoofing (Man-in-the-Middle) attack on TryHackMe.

---

## Objective
Analyze the packet capture to identify the attacker's MAC address sending malicious ARP requests, determine the targeted IP address being spoofed, count total ICMP ping requests, and extract the flag from packet data payloads.

---

## What I Did
1. Loaded the incident capture file into Wireshark for packet-level inspection.
2. Filtered for ARP traffic (`arp`) to spot excessive, repeated broadcast "Who has" requests disrupting normal resolution.
3. Isolated the rogue MAC address generating the flood and identified the gateway/target IP being claimed.
4. Filtered for ICMP echo requests (`icmp.type == 8`) to quantify the ping activity generated during the incident.
5. Inspected the data/payload section of the final ICMP packet in the sequence to retrieve the challenge flag.

---

## Commands & Useful Wireshark Filters
```bash
# Filter for ARP request frames
arp.opcode == 1

# Filter for ICMP Echo Request packets
icmp.type == 8

# Search packet byte payloads directly
frame contains "FLAG"
```

---

## Questions & Answers
* **What is the MAC Address of the device sending excessive ARP "Who has" requests?**
  * `[Attacker MAC Address from PCAP]`
* **What is the IP Address that the attacker is trying to spoof or claim?**
  * `[Target / Gateway IP from PCAP]`
* **How many ICMP (Ping) requests were sent in total?**
  * `[Total Count of ICMP Requests]`
* **Look at the Data portion of the last ICMP packet. What is the flag?**
  * `[FLAG extracted from final ICMP packet]`

---

## Proof Reference
* Proof file: `Assignment15.zip` (contains screenshots of answered TryHackMe questions, Wireshark filters, and flag).