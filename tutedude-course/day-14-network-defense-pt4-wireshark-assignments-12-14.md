# Day 14 - Module 6 (Part 4): Wireshark Investigation + Assignments 12-14

**Date:** 21 Oct 2026
**Module:** Module 6 - Network Defense and Penetration Testing (complete)
**Study time:** 46m
**Assignments:** 12, 13, 14

| Lecture | Duration |
|---|---|
| Analysis: Detailed Wireshark Investigation | 46m |

> All hands-on work below was done only in my own isolated lab VMs or on the course's practice targets, for learning purposes.

## Covered today

### Wireshark basics
- Wireshark captures packets from a network interface, or opens saved `.pcap`/`.pcapng` files, and decodes every protocol layer.
- Panes: packet list (summary), packet details (each layer expanded), packet bytes (raw hex).
- **Capture filters** limit what is recorded; **display filters** limit what is shown.

### Display filters I used
| Filter | Shows |
|---|---|
| `ip.addr == 10.0.0.5` | All traffic to or from one host |
| `ip.src == x` / `ip.dst == x` | One direction only |
| `tcp.port == 445` | SMB traffic |
| `http.request.method == "POST"` | Form submissions (logins, uploads) |
| `dns` / `arp` / `icmp` | One protocol |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Connection attempts - a port scan looks like a burst of these |
| `ftp` / `telnet` | Cleartext protocols, where credentials are visible |

### Investigation workflow
1. **Statistics > Protocol Hierarchy** - what kinds of traffic are in the capture.
2. **Statistics > Conversations / Endpoints / IPv4** - top talkers, and which host sent the most bytes.
3. **Statistics > Destinations and Ports** - unusual ports or destinations.
4. Filter down to suspicious hosts, then **Follow > TCP/HTTP Stream** to rebuild the session as plain text.
5. **File > Export Objects (HTTP/SMB)** - recover files that were transferred.
6. Write down timestamps for the incident timeline.

### What attacks look like in a capture
- **Port scan:** one source sending SYNs to many ports, answered by RST (closed) or SYN-ACK (open).
- **Cleartext login:** FTP/Telnet/HTTP credentials readable in the stream - the reason to use SSH/SFTP/HTTPS.
- **ARP spoofing (MITM):** one MAC address claiming to be several IPs, or gratuitous ARP replies changing the gateway's MAC.
- **Data exfiltration / C2:** regular "beaconing" to one external IP, or unusually large outbound transfers.

### Practice
Worked through the course's Blue Team fundamentals Wireshark challenge questions: which protocol ran on an unusual port, which host was pinged, how many DNS responses were captured, and which host sent the most bytes. In the second capture, I traced an attacker's FTP activity and access to a Windows host.

## Assignments completed
| # | Assignment | Focus |
|---|---|---|
| 12 | Advanced Nmap | full-port and targeted scanning to find a service on a non-standard port |
| 13 | GreyBox VAPT | credentialed Nessus assessment and reporting of the critical findings |
| 14 | Network Traffic Analysis | PCAP triage in Wireshark - finding the suspicious hosts and activity |

## Key takeaways
- Every scan and exploit from earlier in the module leaves a clear signature in the packets. Wireshark is where attack traffic becomes visible.
- This bridges offensive work (Modules 5-6) into defensive analysis (SOC, SIEM and forensics later).
- Module 6 complete.
