# Day 2 – Module 3: Linux & Python Fundamentals


| # | Lecture |
|---|---------|
| 1 | Introduction to Linux |
| 2 | File Permissions Concepts and Text Editors |
| 3 | Essential Linux File Management Commands |
| 4 | Introduction to Servers (Hindi) |
| 5 | Bash Scripting – Variables |
| 6 | Bash Scripting – Arrays & Conditional Statements |
| 7 | Python Fundamentals |

---

## 1. Introduction to Linux

- **Operating System (OS):** software between the user and the hardware. It handles file, memory and process management, I/O and peripherals.
- **Linux** is an open-source, Unix-like OS built on the **Linux kernel** (created by Linus Torvalds, 1991). The kernel is the "brain" that manages hardware and resources.
- **Why learn it:** it is the go-to OS for IT professionals, and it is open source, so it can be customised and hardened.
- **Where it is used:** web servers, car infotainment systems, point-of-sale systems, and critical infrastructure such as traffic lights and industrial sensors.

### Linux architecture

| Layer | Role |
|-------|------|
| Hardware | CPU, RAM, HDD and other devices |
| Kernel | Core of the OS; talks to the hardware |
| System libraries | Pre-compiled reusable code |
| System utilities | Small programs for individual tasks |
| Shell | Interface between the user and the kernel; interprets commands |

### Linux vs Windows

| | Linux | Windows |
|---|-------|---------|
| Storage | Single tree starting at `/` | Drives (`C:`, `D:`, `E:`) |
| Source access | Open; users can modify the kernel | Closed; only select groups have access |
| Security | Harder for malware to break in | Main target for viruses and malware |

### File hierarchy – common directories

| Directory | Purpose |
|-----------|---------|
| `/bin` | Binaries / executable programs |
| `/etc` | System configuration files |
| `/home` | User home directories |
| `/opt` | Optional / third-party software |
| `/tmp` | Temporary files (cleared on reboot) |
| `/usr` | User-related programs |
| `/var` | Variable data, such as logs |

### Kali Linux

- A Debian-based distribution built for **penetration testing and digital forensics**. It is maintained by Offensive Security.
- It ships with **600+ security tools**, is free and open source, is FHS compliant, and is available for 32/64-bit and ARM (for example Raspberry Pi).
- It is used by ethical hackers, pentesters and forensics people.
- It is not beginner-friendly if you are new to the command line.

### Basic navigation and commands

```bash
pwd              # print working directory
ls               # list files (ls -a shows hidden files)
cd <dir>         # change directory
cd ~             # go to home directory
cd ..            # go to parent directory
mkdir <dir>      # create a directory
touch <file>     # create an empty file
cat <file>       # print file contents
clear            # clear the terminal
```

---

## 2. File Permissions and Text Editors

### Permission types
- **r (read)** – view the file or list the directory
- **w (write)** – modify the file or create files in the directory
- **x (execute)** – run the file or enter the directory

### Reading a permission string

```
-rwx rw- r--
│ │   │   └── others: read only
│ │   └────── group:  read + write
│ └────────── user (owner): read + write + execute
└──────────── type: - = file, d = directory
```

Change permissions with `chmod`.

### Text editors
- **Command-line:** `vi`, `nano`, `pico`
- **GUI:** `mousepad`, `kwrite`

### Other things covered
- Download a tool from GitHub: `git clone <repo-url>`
- Install Python 3:
  ```bash
  sudo apt update -y
  sudo apt install python3 -y
  python --version
  ```

---

## 3. Essential File Management Commands

### Copy, move, delete

```bash
cp file1.txt /home/user/Documents/          # copy a file
cp file1.txt file2.txt /home/user/Documents/ # copy multiple files
cp -r /source/dir /destination/dir          # copy a directory (-r = recursive)
mv file1.txt /home/user/Documents/          # move (also used to rename)
rm file1.txt                                # delete a file
rm -r /directory/                           # delete a directory recursively
```

> `rm` has no recycle bin. Deleted files are gone, so double-check before `rm -r`.

### Viewing file content

| Command | What it does |
|---------|--------------|
| `cat file` | Prints the whole file (not good for big files) |
| `more file` | Page by page (space to scroll, `q` to quit) |
| `less file` | Like `more`, but you can scroll backwards too |
| `head file` | First 10 lines (`head -n 5 file` for 5 lines) |
| `tail file` | Last 10 lines (`tail -n 20 file`) |
| `tail -f file` | Follows a file live; great for logs |

### Searching

```bash
find /home/ -name "*.txt"           # find files by name
find / -size +100M                  # files larger than 100 MB
grep "search_term" file1.txt        # search inside a file
grep -r "search_term" /path/to/dir/ # search recursively
```

### File systems

| Type | Use it for |
|------|-----------|
| **ext4** | Default for Linux system disks and servers |
| **NTFS** | Windows compatibility, external drives |
| **FAT32** | Small USB drives, cross-platform (4 GB file size limit) |

### Mounting drives

```bash
sudo mount /dev/sdb1 /mnt/usb   # mount
sudo umount /mnt/usb            # unmount (always before removing the device)
```

### User management

```bash
sudo useradd john              # create user (low-level)
sudo adduser john              # create user (interactive, friendlier)
sudo usermod -aG groupname john # add user to a group
```

- `/etc/passwd` holds usernames and UIDs.
- `/etc/shadow` holds hashed passwords and account expiry info. Only root can read it.

### Package management

| Distro family | Install | Update |
|---------------|---------|--------|
| Debian / Ubuntu / Kali (APT) | `sudo apt install <pkg>` | `sudo apt update` |
| RedHat / CentOS (YUM/DNF) | `sudo yum install <pkg>` | `sudo yum update` |

### Security, processes, services

```bash
sudo ufw enable            # enable the firewall (UFW)
sudo ufw allow 22          # allow SSH traffic

ps aux                     # list running processes
top / htop                 # live process monitor (htop is nicer)

sudo systemctl start <service>   # start a service
sudo systemctl enable <service>  # start on boot
```

### SSH

```bash
sudo apt install openssh-server
sudo systemctl start ssh
```

Hardening tip: set `PermitRootLogin no` in `/etc/ssh/sshd_config`.

### Monitoring and logs
- `top` – CPU and memory, `iotop` – disk I/O
- `df` – disk space, `du` – disk usage per file or folder
- Logs live in `/var/log`. `syslog` covers system activity and `auth.log` covers authentication. View them with `tail -f /var/log/syslog`.

---

## 4. Introduction to Servers

A **server** is a computer that provides services to other devices on a network.

| Server type | Job |
|-------------|-----|
| Print | Manages and queues print jobs |
| File | Central storage and sharing of files |
| Authentication | Verifies user identity (the "security guard") |
| Database | Stores data and handles queries |
| Email | Handles incoming and outgoing mail |
| Web | Hosts websites |
| Application | Runs applications for clients |

### Quick file sharing with Python

```bash
python3 -m http.server 9000
```

Turns the current directory into a web server (supports GET and HEAD only). It is handy for transferring files, and it replaced `SimpleHTTPServer` from Python 2.

### Apache web server

```bash
sudo apt install apache2
sudo systemctl start apache2      # or stop
sudo systemctl enable apache2     # or disable (start on boot)
```

- Test at `http://localhost`.
- Website files live in `/var/www/html`.

### Samba (file sharing across Windows / macOS / Linux)

```bash
sudo apt update && sudo apt install samba
sudo systemctl status smbd
mkdir /home/<username>/sambashare/
sudo nano /etc/samba/smb.conf
```

Add at the bottom of `smb.conf`:

```ini
[sambashare]
comment = Samba share
path = /home/username/sambashare
read only = no
browsable = yes
```

Then set a Samba password with `sudo smbpasswd -a username`.

### NFS (Network File System; Linux to Linux sharing)

**Server side**
```bash
sudo apt install nfs-kernel-server
sudo mkdir /mnt/nfs_share
sudo chown nobody:nogroup /mnt/nfs_share/
sudo chmod 777 /mnt/nfs_share/          # lab only; too permissive for real use
# add to /etc/exports:
# /mnt/nfs_share <client_IP>(rw,sync,no_subtree_check)
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

**Client side**
```bash
sudo apt install nfs-common
sudo mkdir -p /mnt/nfs_clientshare
sudo mount <server_IP>:/mnt/nfs_share /mnt/nfs_clientshare
```

---

## 5. Bash Scripting – Variables

- **Bash** runs in the terminal on most Linux distros and macOS. A script is a sequence of commands in a file, used to automate tasks.
- Every script starts with the **shebang**: `#!/bin/bash`
- `echo` prints text (like `print` in Python).

```bash
#!/bin/bash
MESSAGE="Shell Scripting is Fun!"
echo "$MESSAGE"
read name            # waits for user input
echo "Hello $name"
```

**Rules**
- **No spaces** around `=` (`name="Yash"`, not `name = "Yash"`).
- Use `$` to read a variable (`$name`).
- Multiple variables can be used in one `echo`.

---

## 6. Bash Scripting – Arrays & Conditionals

### Arrays
- An array stores multiple values under one name. **Indexing starts at 0.**

```bash
transport=('car' 'train' 'bike' 'bus')
echo "${transport[@]}"        # print all elements
echo "${transport[1]}"        # train
transport[1]='trainride'      # change an element
unset transport[1]            # remove an element
```

### Conditionals

```bash
if [ condition ]; then
    ...
elif [ condition ]; then
    ...
else
    ...
fi
```

---

## 7. Python Fundamentals

### Why Python for security?
- Automating tasks (malware scans, traffic analysis, vulnerability checks)
- Building custom security tools (IDS, incident-response scripts)
- Analysing logs and network traffic to spot anomalies

### Setup
- Check the version with `python -V`, or install from python.org.
- Course setup: **Anaconda + Jupyter Notebook**.

### Basics

```python
print("Hello, World!")
```

- **Indentation** defines code blocks (Python uses no `{}`).

### Data types

| Type | Example | Notes |
|------|---------|-------|
| `int` | `7` | Whole numbers |
| `float` | `7.0` | Decimals |
| `str` | `"hello"` | Single or double quotes |
| `list` | `[1, 2, "three"]` | Ordered, mutable, allows duplicates |
| `tuple` | `(1, "two", 3.0)` | Ordered, **immutable** |
| `dict` | `{"name": "Alice", "age": 30}` | Key-value pairs, mutable |
| `bool` | `True` / `False` | Result of comparisons |

Check a type with `type(x)`.

### Operators

```python
1 + 2 * 3 / 4.0      # arithmetic
11 % 3               # modulo -> 2
7 ** 2               # power -> 49
"hello" + " " + "world"   # string concat
"hello" * 3          # string repeat
[1,2] + [3,4]        # list join
[1,2,3] * 3          # list repeat
```

### String operations

```python
s = "Hello world!"
len(s)          # length
s.index("o")    # position of first "o"
s.count("l")    # how many times "l" appears
```

### Conditions and logic

- Comparison operators: `==  !=  <  <=  >  >=`
- Logic operators: `and`, `or`, `not`, and `in` (membership test)

```python
x = 2
if x == 2:
    print("x equals two!")
else:
    print("x does not equal two.")

name = "John"
if name in ["John", "Rick"]:
    print("Your name is either John or Rick.")
```

### Loops

```python
for x in range(5):        # 0,1,2,3,4
    print(x)

for x in range(3, 6):     # 3,4,5
    print(x)

count = 0
while count < 5:
    print(count)
    count += 1
```

---

## Practice and assignments

**Linux Assignment 1:** hidden files (`ls -a`), `chmod`, `mkdir` + `touch`, `cat`, `grep`, `ps aux | grep`, `ip a`, `adduser` + `passwd`, `apt install htop`, `tar -czf`, `tail /var/log/syslog`.

**Bash Assignment 2:** create the Fruits folder and file, and write scripts for leap year, even/odd, number in range 1–100, and a simple calculator.

**Python Assignment:** variables, data types, integer and float maths, string manipulation, booleans, type conversion, a pass/fail name checker, and these mini-projects:
- Booze Delivery Service simulation (age check, menu, order summary)
- Temperature Converter (Celsius / Fahrenheit / Kelvin)
- Discount Calculator

**Lab files provided:** `linux_practical.zip` and `Python_Labs.zip` (ATM, Calculator, Discount Calculator, Temp Converter, Booze Delivery notebooks).

---

## Key takeaways

1. Linux is kernel + shell + utilities. Kali is the Linux distro built for pentesting.
2. Permissions (`rwx` for user, group and others) are central to Linux security.
3. `grep`, `find`, `tail -f` and `/var/log` are the everyday tools for investigating a system.
4. Servers (Apache, Samba, NFS, Python `http.server`) are how files and services get shared, and also what attackers target.
5. Bash and Python are the two scripting languages for automating security work.
