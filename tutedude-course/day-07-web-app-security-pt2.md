# Day 7 - Module 5 (Part 2): Hosting with Apache and Website Defacement Lab

**Date:** 14 Oct 2026
**Module:** Module 5 - Application Security and Penetration Testing (part 2 of 5)
**Study time:** 1h 25m

| Lecture | Duration |
|---|---|
| Ubuntu Setup and Linux File Sharing | 21m |
| Introduction to Apache: Hosting Your First Website | 16m |
| Website Defacement Practical | 48m |

> All hands-on work below was done only in my own isolated lab VMs, for learning purposes.

## Covered today

### Ubuntu setup and file sharing
- Built an Ubuntu Server VM to act as the "web server" for the lab.
- Revisited file sharing: Python `http.server` for quick transfers, **Samba** for Windows/macOS clients, **NFS** for Linux clients.

### Hosting a website with Apache
```bash
sudo apt install apache2
sudo systemctl enable apache2
sudo systemctl start apache2
# site files live in /var/www/html
```
Replaced the default `index.html` with my own page and confirmed it at `http://localhost`.

### Website defacement - how a misconfiguration leads to it
The course used two lab documents to show how real defacements happen. I studied them from the defender's side.

**Lab 1 - FTP misconfiguration**
- The FTP server (vsftpd) was deliberately configured so that a local FTP user landed directly in the web root (`/var/www/html`) **with write access**, and a weak, guessable password was set for the lab.
- A service scan of the server shows FTP (21) next to HTTP (80) - an immediate red flag.
- With the weak credentials, anyone can replace `index.html`, and the public website changes instantly.
- **Why this happens in real life:** default or weak FTP passwords, anonymous FTP with write access, developer credentials leaked in public repositories or breach dumps, and FTP users chrooted into the web root.

**Lab 2 - WordPress misconfiguration on a practice VM**
- A deliberately vulnerable practice VM ran FTP, SSH and an Apache/WordPress site.
- The lesson showed how small weaknesses chain together: an exposed WordPress login, a weak admin password, admin features that can run code, password hashes readable after compromise, and an over-permissive `sudo` rule. Together these lead from the website to full control of the server, and the defacement is only the visible last step.

### Hardening checklist I wrote from these labs
| Weakness | Fix |
|---|---|
| FTP with write access into the web root | Never map FTP to the web root; deploy through CI/CD or SFTP with least privilege |
| Weak or default passwords | Strong unique passwords, lockout/rate limiting, MFA on admin panels |
| Plain FTP (cleartext) | Replace with SFTP/FTPS; disable anonymous login |
| Exposed CMS admin | Restrict `/wp-admin` by IP, keep core, plugins and themes updated |
| Over-broad sudo rights | Review `sudo -l` for every user; grant only the commands needed |
| Unused services | Disable anything the server does not need |

## Key takeaways
- A web server is only as safe as the services running next to it.
- Defacement is usually not "advanced hacking" - it is weak credentials plus a misconfiguration.
