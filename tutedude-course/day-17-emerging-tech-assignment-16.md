# Day 17 - Module 9: Securing Emerging Technologies + Assignment 16

**Date:** 24 Oct 2026
**Module:** Module 9 - Securing Emerging Technologies (complete)
**Study time:** 2h 11m
**Assignment:** 16

| Lecture | Duration |
|---|---|
| The Dual-Edge of AI: Offensive Evolution and Defense | 14m |
| Securing LLMs: Understanding Privileged Intermediaries | 23m |
| Hands-on Lab: Breaking Chatbots with Prompt Injection | 45m |
| IoT Security Fundamentals: MQTT Packet Monitoring | 50m |

> All hands-on work below was done only in the course's dedicated practice labs, for learning purposes.

## Covered today

### The dual edge of AI
AI changes the threat landscape in two directions at once:
- **AI as the weapon (attack evolution)**
  - *Scaling persuasion:* phishing moves from generic, spray-and-pray templates to profiled, natural-language, emotionally tuned and real-time messages. Defence has to shift from spotting bad grammar to behavioural signals and strict email authentication (**SPF, DKIM, DMARC**).
  - *Synthetic deception:* deepfake voice and video used for CEO fraud (fake approval of wire transfers), bypassing KYC video checks, and fabricated evidence. Defence: liveness checks and out-of-band verification.
  - *Shadow AI:* employees pasting sensitive data into public AI tools, which risks data leakage, privacy and data-residency violations, and unchecked AI decisions. Defence: classify AI tools and enforce usage policies like any other enterprise software.
- **AI as the target (LLM security)** - a larger attack surface that mixes web, API and machine-learning risks.

### Securing LLMs - the "privileged intermediary"
- An LLM connected to internal data and APIs sits between the user and systems the user cannot reach directly. That is architecturally similar to **SSRF**: the attacker gets the trusted component to fetch data or act on their behalf.
- **Prompt injection** - crafted input that overrides the system's original instructions. It is like command injection, but against a probabilistic model. Consequences: leaked system prompts and context data, unauthorised API calls, bypassed content restrictions.
- **Excessive agency** - the model has powerful tools (read/write a database, send email, delete files) and can be talked into using them without per-action approval.
- **LLM-API attack anatomy:** malicious prompt -> the model decides to call a function -> it generates JSON arguments -> **the app executes them blindly** -> the result goes back into context -> the model summarises it for the attacker. The weak point is the application trusting the model's output as if it were a validated internal command.
- **Chaining:** harmless-looking APIs can be chained by the model's reasoning into a real attack.
- **Data poisoning** - malicious data in training or fine-tuning pipelines permanently skews the model's behaviour.
- **Testing method:** identify inputs (prompts, uploaded documents, plugins) -> map the APIs and data the model can reach -> probe with classic web attack ideas through natural language -> watch for behaviour changes or logic leaks.

### Governance for secure AI adoption
Four pillars: **human-in-the-loop** approval for high-impact actions, **least-privilege** API tokens, **audit logging** of every prompt/response pair, and **approved vendors** only (no shadow AI).

### Hands-on lab - breaking chatbots
Worked through the course's practice chatbot labs at two levels: first extracting information and showing excessive agency, then mapping the APIs the model could call and showing how input to the model reached them indirectly. The main lesson: **LLM security is not a separate discipline - it is web and API security applied to a component that can be persuaded.**

### IoT security - MQTT packet monitoring
- **MQTT** is a lightweight publish/subscribe protocol for IoT. Devices publish to **topics** on a **broker**, and subscribers receive the messages.
- Default port **1883** is cleartext; **8883** is MQTT over TLS.
- In Wireshark (`mqtt` filter) I could see CONNECT packets, topic names and payloads - including usernames and passwords when TLS is not used.
- **Common IoT weaknesses:** default credentials, no encryption, anonymous broker access, wildcard subscriptions (`#`) that expose every topic, and devices that are never patched.
- **Defences:** TLS, per-device authentication, topic-level ACLs, network segmentation of IoT devices, and firmware updates.

## Assignment completed
| # | Assignment | Focus |
|---|---|---|
| 16 | Fuzzing | finding hidden endpoints and unexpected inputs by fuzzing a test application and analysing the responses |

## Key takeaways
- Treat the LLM as an untrusted user: validate everything it outputs before acting on it, and give it the least privilege possible.
- Module 9 complete.
