# Day 6 — Module 5 (Part 1): How the Web Works & Web App Security Concepts

**Date:** 13 Oct 2026 · **Lectures:** How Websites Work (24m), WebApp Security Concepts (23m), Hacking Your First Website (13m)

> All hands-on work below was done only in my own isolated lab VMs or on the course's dedicated TryHackMe rooms, for learning purposes.

## Covered today
### How websites work
- Front end (client-side: HTML/CSS/JS) vs back end (server-side processing).
- **DNS** resolves a domain to an IP via recursive → root → TLD → authoritative servers.
- Request/response model between browser and web server.

### Web app security concepts
- **Cookies:** attributes `Secure`, `HttpOnly`, `SameSite`, `Expires`; stored client-side (~4KB, editable).
- **Sessions:** server-side state tied to a session ID cookie.
- **Authentication mechanisms:** Basic, Form-based, Token-based (JWT), OAuth, MFA (something you know/have/are).
- Key security idea that recurs all module: **cookie = opaque session ID only; never trust client-side data for identity or role.**

### Hacking your first website
Intro practical showing how trusting client-side input leads directly to the bugs covered later (access control, injection).

## Key takeaways
- Sessions are safer than raw cookies because the data lives server-side.
- Almost every web vuln this module traces back to the server trusting the client.
