# Module 8 — Governance, Risk & Compliance (Part 2) — Assignment 15
**Date:** 27 Oct 2026

Investigated a captured network traffic file (.pcap) containing an active ARP spoofing (Man-in-the-Middle) attack on TryHackMe.

---

## What I learned today

### Assignment 15: Task — Investigating an Attack

* **Objective:** Analyze an incident capture file in Wireshark to locate the attacker's MAC address executing an ARP spoofing attack, determine the IP being claimed, count the ICMP ping packets, and extract the exfiltrated flag from packet data payloads.

* **What I did:**
  1. Opened the capture file in Wireshark to evaluate network activity.
  2. Filtered for ARP frames (`arp`) to identify abnormal broadcast behavior and excessive "Who has" requests.
  3. Identified the specific rogue MAC address transmitting unsolicited/flood ARP requests claiming the target gateway IP.
  4. Applied display filters for ICMP (`icmp`) to count total Echo (ping) requests exchanged during the attack sequence.
  5. Selected the last ICMP packet in the stream, examined its Data section in ASCII/hex view, and recovered the hidden challenge flag.

```bash
# Useful Wireshark display filters applied
arp.opcode == 1
arp.duplicate-address-frame
icmp.type == 8
data.data contains "FLAG"
```

* **Questions & Answers:**
  * **What is the MAC Address of the device sending excessive ARP "Who has" requests?**
    * Identified via the sender MAC address in the repetitive ARP request frames.
  * **What is the IP Address that the attacker is trying to spoof or claim?**
    * The target default gateway / victim IP specified in the ARP request target fields.
  * **How many ICMP (Ping) requests were sent in total?**
    * Total packet count matched via `icmp.type == 8` filter.
  * **Look at the Data portion of the last ICMP packet. What is the flag?**
    * Extracted from the ASCII payload of the final ICMP request frame.

* **Proof / Screenshot reference:** Documented in `Task.pdf` (submitted on TryHackMe with all questions answered and flag revealed).
* **Proof archive:** `tutedude-course/Assignment 15.zip`

---

## Things I found interesting / want to explore more
- How quickly an unauthorized device on the local network can alter switch and host ARP tables using unsolicited replies.
- The use of ICMP data payloads as covert channels for data exfiltration without raising typical alert thresholds.
- Implementing Dynamic ARP Inspection (DAI) and DHCP Snooping on managed switches to completely prevent this attack vector at Layer 2.

---

## My own words summary
Today's lab was a solid blue-team exercise in packet-level incident response. Filtering ARP requests made the attacker's spoofing attempt obvious right away, and inspecting the payload bytes of the ICMP packets demonstrated how easily protocols can be abused for data exfiltration if they aren't monitored closely.