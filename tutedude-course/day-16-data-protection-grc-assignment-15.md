# Day 16 - Module 7 (Part 2) and Module 8: Data Protection, GRC + Assignment 15

**Date:** 23 Oct 2026
**Modules:** Module 7 - Data Protection and Cryptography (complete), Module 8 - Governance, Risk and Compliance (complete)
**Study time:** 2h 37m
**Assignment:** 15

| Lecture | Module | Duration |
|---|---|---|
| Data Protection and Security Principles (Part 2) | M7 | 1h 00m |
| GRC Fundamentals: An Overview | M8 | 25m |
| Governance: Principles and Frameworks | M8 | 37m |
| Risk Management: Identification and Mitigation | M8 | 13m |
| Compliance: Standards and Regulatory Requirements | M8 | 8m |
| The DPDP Act 2023: Privacy and Data Protection | M8 | 15m |

## Covered today

### Module 7 - Data Protection (Part 2)
- **Risk ranking:** likelihood x impact; risk assessment produces a prioritised list of what to fix.
- **Risk treatment with real examples:**
  - *Accept* - management formally accepts a low-impact internal issue because fixing it costs too much.
  - *Avoid* - decommission a legacy app on an unsupported OS.
  - *Mitigate* - MFA and least-privilege access on critical systems.
  - *Transfer* - cyber insurance.
- **Defense in depth** applied to data: physical, network, endpoint, application, data (encryption at rest and in transit, masking, backups), IAM (MFA, SSO, RBAC, provisioning and deprovisioning), policies, and monitoring.
- **Privacy:** protect the organisation's own data, data entrusted by clients, and teach users to protect their personal information. PII vs PHI.

### Module 8 - Governance, Risk and Compliance
**Governance** - the structure, policies and methods top management uses to protect information assets:
- Strategy aligned with business goals; policies and procedures; risk management; performance metrics (KPIs); compliance.

**The governance document hierarchy**
| Document | Nature | Example |
|---|---|---|
| Policy | Mandatory internal direction | Access Control Policy, Acceptable Use Policy |
| Standard | Specific mandatory requirements | ISO 27001, PCI DSS |
| Procedure | Step-by-step instructions | Incident handling steps |
| Guideline | Recommended, not mandatory | NIST password guidelines, OWASP Top 10 |
| Baseline | Minimum security level | CIS benchmark configuration |
| Regulation / Law | Legally binding | GDPR, HIPAA, CCPA |

**Writing a policy:** define scope -> research laws and standards -> draft -> review and approve -> implement and train -> maintain. Worked examples: an Acceptable Use Policy and a Password Policy.

**Building a GRC program:** define objectives (for example "reduce cyber risk by 50% in 12 months") -> risk assessment -> policies -> governance structure and roles -> controls (firewall, SIEM, IDS/IPS, training) -> monitor -> continuous improvement. Also covered what GRC looks like in the financial sector (AML, PCI DSS, GLBA).

**Risk management**
- Inputs: threat, vulnerability, impact, likelihood. For example: tsunami + seaside office = high impact but negligible likelihood; ransomware + university data = high likelihood.
- **Qualitative analysis:** high/medium/low or red/amber/green ratings.
- **Quantitative analysis:** monetary values for data-driven decisions.
- Risks must be monitored continuously: add new ones, retire old ones, and check that responses still work.

**Compliance types:** legal (GDPR, HIPAA), regulatory (PCI DSS, AML), internal (password and whistleblower policies), contractual (SLAs, vendor contracts).

**Frameworks**
- **ISO 27001** - the international standard for an ISMS; covers people, process and technology; risk-based; **Annex A** lists 93 controls in four themes (organisational, people, physical, technological); organisations can be certified against it.
  - GRC is the "why" and the whole picture; ISO 27001 is the "how" and the proof.
- **NIST CSF 2.0** - Govern, Identify, Protect, Detect, Respond, Recover. The course included NIST and ISO assessment worksheets.

**India's Digital Personal Data Protection (DPDP) Act, 2023**
- Regulates how digital personal data is collected, processed and stored.
- **Data Principal** - the individual. Rights: access, correction and erasure, grievance redressal (through the Data Protection Board of India).
- **Data Fiduciary** - decides why and how data is processed; accountable for protecting it.
- **Data Processor** - processes data on the fiduciary's instructions.
- Principles: lawful and transparent processing, purpose limitation, data minimisation, accuracy, storage limitation, security safeguards and accountability.

## Assignment completed
| # | Assignment | Focus |
|---|---|---|
| 15 | Investigating an Attack | PCAP investigation in Wireshark - identified a man-in-the-middle (ARP spoofing) attack and documented the evidence |

## Key takeaways
- Technical controls without governance get skipped; governance without technical controls is just paperwork. GRC connects the two.
- Modules 7 and 8 complete.
