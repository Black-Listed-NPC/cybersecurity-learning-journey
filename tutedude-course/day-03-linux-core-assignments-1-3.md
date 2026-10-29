# Day 3 — Module 3: Linux Core Skills + Assignments 1–3

**Date:** 10 Oct 2026 · **Lectures:** M3 — File Permissions & Text Editors (19m), Essential File Management (36m), Intro to Servers (21m) · **Assignments:** 1, 2, 3

> All hands-on work below was done only in my own isolated lab VMs or on the course's dedicated TryHackMe rooms, for learning purposes.

## Covered today
### File permissions & ownership
- Three permission types — **read (r), write (w), execute (x)** — for **user / group / others**.
- Reading a string: `-rwxrw-r--` → file, owner `rwx`, group `rw-`, others `r--`.
- Changed permissions with `chmod` and ownership with `chown`.
- Text editors: `nano`, `vi` (CLI); mousepad/Kwrite (GUI).

### Essential file management
- `cp` / `mv` / `rm` (with `-r` for directories), `mkdir`, `touch`, `cat`.
- Viewing content: `cat`, `more`, `less`, `head -n`, `tail -n`, and `tail -f` for live logs.
- Searching: `find /path -name "*.txt"`, `grep "term" file`, `grep -r`.
- File hierarchy: `/bin /etc /home /opt /tmp /usr /var`.

### Introduction to servers
- Server types: print, file, authentication, database, email, web, application.
- Quick file sharing: `python3 -m http.server 9000`.

## Assignments completed (TryHackMe)
| # | Task | Focus |
|---|------|-------|
| 1 | Basic Linux Commands | navigation, `ls -a`, `cat`, `grep`, `ps aux`, `ip a` |
| 2 | Linux Permissions | permission strings, `chmod`, `chown`, users/groups |
| 3 | File System Commands | `cp`, `mv`, `rm`, `find`, `tar`, `/var/log` |

**Proof:** `Assignment 1.zip`, `Assignment 2.zip`, `Assignment 3.zip`
