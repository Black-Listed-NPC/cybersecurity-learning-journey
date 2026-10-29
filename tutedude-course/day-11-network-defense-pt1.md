# Day 11 - Module 6 (Part 1): Network Types, Topologies and Devices

**Date:** 18 Oct 2026
**Module:** Module 6 - Network Defense and Penetration Testing (part 1 of 4)
**Study time:** 1h 31m

| Lecture | Duration |
|---|---|
| Network Types and Topologies | 28m |
| Network Devices and Fundamentals | 1h 03m |

## Covered today

### Network types
| Type | Coverage | Example |
|---|---|---|
| PAN | A few metres around one person | Bluetooth phone and earbuds |
| LAN | One building or office | Office Ethernet/Wi-Fi |
| WLAN | Wireless LAN | Home Wi-Fi |
| MAN | A city or campus | City-wide cable network |
| WAN | Countries and continents | The internet, company branch links |

### Topologies
| Topology | Layout | Strength | Weakness |
|---|---|---|---|
| Bus | All devices on one cable | Cheap, simple | One cable fault takes everything down |
| Star | All devices connect to a central switch | Easy to manage, one bad cable affects one host | The central device is a single point of failure |
| Ring | Each device connects to two neighbours | Predictable performance | One break can stop the ring |
| Mesh | Many or all devices interconnected | Highly redundant | Expensive, complex |
| Tree / Hybrid | A mix of the above | Scales for large organisations | More design effort |

### Network devices and their role in security
| Device | Layer | Role |
|---|---|---|
| Hub | 1 | Repeats traffic to every port (no filtering, easy to sniff) |
| Switch | 2 | Forwards frames by MAC address; supports VLANs for segmentation |
| Router | 3 | Routes packets between networks by IP; ACLs filter traffic |
| Access point | 1-2 | Connects wireless clients to the wired network |
| Firewall | 3-7 | Allows or blocks traffic by rule; the boundary between trust zones |
| IDS / IPS | 3-7 | Detects (IDS) or blocks (IPS) suspicious traffic patterns |
| Load balancer / proxy | 4-7 | Spreads load, hides internal servers, can inspect traffic |

### Network fundamentals
- **OSI model:** Physical, Data Link, Network, Transport, Session, Presentation, Application. **TCP/IP model:** Network Access, Internet, Transport, Application.
- **IP addressing:** IPv4 is 32-bit (for example `192.168.1.10/24`). Private ranges: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. The subnet mask decides which part is the network and which part is the host.
- **TCP vs UDP:** TCP is connection-oriented and reliable (three-way handshake SYN -> SYN-ACK -> ACK); UDP is connectionless and fast (DNS, streaming).
- **Common ports:** 21 FTP, 22 SSH, 23 Telnet, 25 SMTP, 53 DNS, 80 HTTP, 110 POP3, 139/445 SMB, 143 IMAP, 443 HTTPS, 3306 MySQL, 3389 RDP.
- **Core services:** DHCP hands out addresses, DNS resolves names, ARP maps IP addresses to MAC addresses on the local network.

## Key takeaways
- Topology and segmentation decide how far an attacker can move. A flat network (the WannaCry hospital) lets one infection reach everything.
- Knowing which device works at which layer explains which control can stop which attack: switches and VLANs at Layer 2, routers and ACLs at Layer 3, firewalls and IPS higher up.
