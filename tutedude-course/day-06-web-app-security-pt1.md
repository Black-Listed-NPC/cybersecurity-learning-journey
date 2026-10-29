# Day 6 - Module 5 (Part 1): How the Web Works and Web App Security Concepts

**Date:** 13 Oct 2026
**Module:** Module 5 - Application Security and Penetration Testing (part 1 of 5)
**Study time:** 1h 00m

| Lecture | Duration |
|---|---|
| How Websites Work? | 24m |
| WebApp Security Concepts (Cookies, Sessions, Authentication) | 23m |
| Hacking Your First Website | 13m |

## Covered today

### How websites work
- The browser sends a **request** to a web server; the server sends back a **response** that the browser renders.
- **Front end (client side):** what the browser renders - HTML (structure), CSS (style), JavaScript (interactivity).
- **Back end (server side):** processes the request, talks to databases and returns data.
- **DNS** turns a domain name into an IP address:
  1. The computer checks its local cache.
  2. It asks the **recursive DNS server** (usually the ISP's), which also has a cache.
  3. On a miss, the **root servers** point to the right **TLD server** (for example `.com`).
  4. The TLD server points to the domain's **authoritative name server**.
  5. The authoritative server returns the record, and that is where DNS changes are made.
- **Web server security issues:** default configurations, unpatched software, directory listing, verbose errors, unnecessary services and weak credentials - which is why **patch management** is part of web security.

### Web app security concepts
**Cookies**
- Small pieces of data the server asks the browser to store; sent back with every request to keep state over stateless HTTP.
- Attributes: `Name`, `Value`, `Expires`, `Secure` (HTTPS only), `HttpOnly` (no JavaScript access), `SameSite` (`Strict`/`Lax` - limits cross-site sending).
- Flow: login -> server sends `Set-Cookie: session_id=...` -> browser stores it -> browser sends it on every later request.

**Sessions**
- Server-side storage of user state (user ID, role, cart). The browser only holds a **session ID** in a cookie.

| | Cookie | Session |
|---|---|---|
| Stored | Browser | Server |
| Size | ~4 KB | Depends on server |
| Visible to user | Yes, editable | No |
| Security | Lower (can be stolen, e.g. via XSS) | Higher |

**Authentication mechanisms**
| Method | How it works | Security |
|---|---|---|
| Basic | Credentials in an HTTP header on every request | Low (only safe over HTTPS) |
| Form-based | Login form -> server creates session -> session ID cookie | Medium |
| Token-based (JWT) | Server returns a signed token, sent in the `Authorization` header | High |
| OAuth | A third party (Google, Facebook) authenticates and returns an access token | High |
| MFA | Two or more factors combined | Very high |

### Hacking your first website (demo)
A short demonstration of how trusting client-side data (a value in a cookie or a hidden form field) lets a user change things they should not. It previews the access-control bugs covered later in the module.

## Key takeaways
- **The cookie should hold only an opaque session ID - never the user's identity or role.** Anything stored on the client can be edited.
- Almost every web vulnerability in this module comes back to one mistake: the server trusting data that came from the client.
