# Day 3 - Module 3 (Part 2): Linux Permissions, File Management and Servers

**Date:** 10 Oct 2026
**Module:** Module 3 - Linux and Python Fundamentals (part 2)
**Study time:** 1h 16m

| Lecture | Duration |
|---|---|
| File Permissions Concepts and Text Editors | 19m |
| Essential Linux File Management Commands | 36m |
| Introduction to Servers (Hindi) | 21m |

> All hands-on work below was done only in my own isolated lab VMs, for learning purposes.

## Covered today

### File permissions and ownership
- Three permissions - **read (r)**, **write (w)**, **execute (x)** - for three classes: **user (owner)**, **group**, **others**.
- Reading a permission string: `-rwxrw-r--`
  - `-` file (a `d` would mean directory)
  - `rwx` owner can read, write, execute
  - `rw-` group can read and write
  - `r--` others can only read
- `chmod` changes permissions (symbolic `u+x` or numeric `644`, `755`); `chown user:group file` changes ownership.
- **Text editors:** command-line (`nano`, `vi`, `pico`) and GUI (mousepad, Kwrite).
- Downloading tools from GitHub with `git clone <url>`, and installing Python with `sudo apt update` then `sudo apt install python3`.

### Essential file management
| Task | Commands |
|---|---|
| Copy / move / delete | `cp file dest`, `cp -r dir dest`, `mv file dest`, `rm file`, `rm -r dir` |
| View content | `cat`, `more` (page by page), `less` (scroll both ways), `head -n 5`, `tail -n 20` |
| Watch a log live | `tail -f /var/log/syslog` |
| Search for files | `find /home/ -name "*.txt"`, `find / -size +100M` |
| Search inside files | `grep "term" file`, `grep -r "term" /path/` |
| Compress | `tar -czvf archive.tar.gz folder/` |

**File systems**
- **ext4** - default for Linux system disks and servers.
- **NTFS** - Windows; Linux reads and writes it with `ntfs-3g`.
- **FAT32** - USB drives; works everywhere but has a 4 GB file-size limit.
- Mount and unmount: `sudo mount /dev/sdb1 /mnt/usb`, `sudo umount /mnt/usb` (always unmount before removing the device).

**System administration basics**
- Users: `sudo adduser john`, `sudo usermod -aG groupname john`. User data lives in `/etc/passwd`; password hashes in `/etc/shadow`.
- Packages: APT on Debian/Ubuntu (`apt update`, `apt install`), YUM/DNF on Red Hat/CentOS.
- Firewall: `sudo ufw enable`, `sudo ufw allow 22`.
- Processes: `ps aux`, `top`, `htop`. Disk: `df`, `du`, `iotop`.
- Services: `sudo systemctl start|enable <service>`.
- SSH: install `openssh-server`, then harden it by setting `PermitRootLogin no` in `/etc/ssh/sshd_config`.
- Logs: everything under `/var/log` - `syslog` for system activity, `auth.log` for authentication.

**Linux file hierarchy**
`/bin` executables, `/etc` configuration, `/home` user folders, `/opt` third-party software, `/tmp` temporary files, `/usr` user programs, `/var` logs and variable data.

### Introduction to servers
- A **server** provides services to other devices on the network. Types: print, file, authentication, database, email, web and application servers.
- **Quick file sharing:** `python3 -m http.server 9000` turns any folder into a simple web server (GET/HEAD only).
- **Apache:** `sudo apt install apache2`, `sudo systemctl enable --now apache2`, serve from `/var/www/html`, test at `http://localhost`.
- **Samba** (share files with Windows and macOS): install `samba`, add a share block to `/etc/samba/smb.conf`, then set a Samba password with `smbpasswd -a <user>`.
- **NFS** (Linux-to-Linux sharing): install `nfs-kernel-server`, define clients in `/etc/exports` with `rw,sync,no_subtree_check`, run `exportfs -a`, then mount on the client after installing `nfs-common`.

## Key takeaways
- Permissions and ownership are the first line of defence on any Linux host. A world-writable share (`chmod 777`) is convenient in a lab but dangerous in real life.
- Knowing where logs live (`/var/log`) and how to follow them (`tail -f`, `grep`) is the base skill for SOC work later.
