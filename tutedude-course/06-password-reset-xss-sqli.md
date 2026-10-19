# Day 12 – Module 5 Assignments 9–11: Password Reset Flaw, XSS, SQL Injection

**Course:** Tutedude Cybersecurity (TryHackMe practicals)
**Tasks:** Reset Password · Cross-Site Scripting · SQL Injection

> All three were done on the course's dedicated TryHackMe room against a purpose-built training app — not a real or third-party site.

---

## 1. Password Reset Vulnerability

**Objective:** find a flaw in the "forgot password" flow that lets you change another user's password without knowing their current one.

**How this class of bug typically happens:** a password-reset feature has to prove "this request really came from the account owner" *before* letting the password change go through. Common ways that check breaks:
- The reset request accepts a username/user ID as a plain parameter (in the URL, a hidden form field, or an API body) instead of deriving the target purely from a server-side token tied to that specific user.
- A reset token is predictable, reused, or not actually checked against who it was issued to.
- The reset link/OTP doesn't expire and isn't invalidated after first use.
- Client-side JavaScript enforces checks that the server never re-validates — easy to bypass by editing the request directly (this is why checking the client-side source first, as the task hints, often reveals the flaw).

**General technique:** trigger the reset flow, then inspect every request/response in Burp Suite. Look for any field that identifies *whose* password is being reset (a user ID, email, or hidden parameter) and see whether it's trusted as-is. If changing that value to another user's identifier is accepted without further proof of ownership, that's the flaw — this is effectively an **IDOR on a sensitive action**, not just on viewing data.

**Impact:** full account takeover of any user, including admin, with no credentials needed.

**Fix:** always generate a cryptographically random, single-use, short-lived reset token server-side, email/SMS it only to the account owner's registered contact, and validate that the token matches the account before allowing any password change — never trust a user ID coming from the client.

---

## 2. Cross-Site Scripting (XSS)

**Objective:** get the application to execute attacker-supplied JavaScript in a victim's browser.

**Recap from OWASP A05 (Injection family):** XSS happens when user input is reflected or stored by the app and rendered back into the page without being properly encoded/escaped, so the browser treats it as executable code instead of plain text.

**Types:**
| Type | Where the payload lives |
|------|--------------------------|
| **Reflected** | Bounced straight back in the response (e.g. a search box or error message) — needs the victim to click a crafted link |
| **Stored** | Saved on the server (e.g. a comment or profile field) and served to *every* visitor who views that page |
| **DOM-based** | Never touches the server — client-side JavaScript itself writes untrusted input into the page |

**General technique:** find an input that gets echoed back into the HTML (a search field, a comment box, a URL parameter) and test it with a simple, harmless proof-of-concept payload designed just to prove script execution, such as a basic `<script>` tag that pops a JavaScript alert box. If the alert fires, the input isn't being sanitized.

**Impact:** session/cookie theft, keylogging, defacement, or performing actions as the victim — basically anything their browser session can do.

**Fix:** encode output based on context (HTML-encode for HTML body, JS-encode inside `<script>`, URL-encode in links), use a Content-Security-Policy header, and mark session cookies `HttpOnly` so JavaScript can't read them even if XSS exists.

---

## 3. SQL Injection

**Objective:** find and exploit a SQLi flaw on `/search.php` to dump the database.

**Recap from OWASP A05 (Injection):** happens when user input is concatenated directly into a SQL query instead of being passed as a parameter, letting an attacker's input change the query's actual logic.

**General technique:**
1. Identify an input that feeds a database query — a search box is a classic spot, since search terms almost always get built into a `SELECT ... WHERE ... LIKE` query.
2. Test with a single quote (`'`) to see if it breaks the query (a SQL error or unexpected behavior confirms the input isn't sanitized).
3. From there, injection can be used to bypass logic (classic example: `' OR '1'='1' --`), or to extract data using `UNION SELECT` to pull columns from other tables once the number of columns and data types are known.
4. **Automated tools** (as the task notes) like **sqlmap** can automate detection and extraction once a vulnerable parameter is confirmed — `sqlmap -u "http://target/search.php?q=test" --dump` is the standard pattern for this.

**Impact:** full read (and sometimes write) access to the database — usernames, password hashes, personal data, or anything else stored there.

**Fix:** use parameterized queries / prepared statements everywhere (never build SQL by string concatenation), apply least-privilege database accounts, and use an ORM or input validation as defense in depth.

---

## My own words summary
These three tasks are really three sides of the same lesson: **never trust client-supplied input to carry out a sensitive decision.** The password reset bug trusts a client-supplied user ID, XSS trusts that user input won't be executed as code, and SQLi trusts that user input won't be executed as a database command. Burp Suite kept coming up as the one tool that makes all three practical — you can't spot a tampered parameter or a broken token check just by looking at the rendered page; you have to see the raw request.

## Things to explore more
- Try sqlmap properly on a lab target instead of doing SQLi manually, to see how much faster automated discovery is.
- Look at how `HttpOnly` and `CSP` headers would have limited the impact of the XSS task even if the flaw still existed.
