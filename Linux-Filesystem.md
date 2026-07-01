# Linux Filesystem

The Linux filesystem is a hierarchical directory structure used to organize files and directories on a Linux operating system.

Unlike Windows, Linux does not use drive letters such as `C:` or `D:`. Everything starts from a single top-level directory called the **root directory**.

---

# Filesystem Structure

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

The symbol `/` represents the root directory.

---

# Root Directory (/)

The root directory is the starting point of the entire Linux filesystem.

All files and directories exist under `/`.

Example:

```text
/
├── home
├── etc
└── var
```

---

# /home

Contains personal directories for users.

Example:

```text
/home/prince
/home/pooja
```

This is where user documents, downloads, and personal files are usually stored.

Example:

```bash
cd /home/prince
```

---

# /root

Home directory of the root user (administrator).

Example:

```text
/root
```

Do not confuse:

```text
/
```

with

```text
/root
```

The first is the root filesystem, while the second is the root user's home directory.

---

# /bin

Contains essential user commands required for system operation.

Examples:

```text
/bin/ls
/bin/cp
/bin/mv
/bin/cat
```

You can check their location:

```bash
which ls
```

Output:

```text
/usr/bin/ls
```

---

# /sbin

Contains system administration commands.

Examples:

```text
/sbin/reboot
/sbin/fsck
/sbin/shutdown
```

These commands are generally used by administrators.

---

# /etc

Contains system configuration files.

Examples:

```text
/etc/passwd
/etc/shadow
/etc/hostname
/etc/ssh/
```

Cybersecurity professionals frequently inspect this directory.

Example:

```bash
cat /etc/passwd
```

---

# /boot

Contains files required for system startup and bootloader configuration.

Examples:

```text
/boot/vmlinuz
/boot/grub
```

---

# /dev

Contains device files.

In Linux, hardware devices are represented as files.

Examples:

```text
/dev/sda
/dev/null
/dev/random
```

Useful examples:

```bash
echo "hello" > /dev/null
```

---

# /proc

Virtual filesystem containing information about running processes and kernel information.

Examples:

```text
/proc/cpuinfo
/proc/meminfo
/proc/version
```

Useful commands:

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

---

# /sys

Contains kernel and hardware information.

Used by system administrators and advanced users.

Example:

```text
/sys/class/net
```

---

# /tmp

Stores temporary files.

Files may be deleted automatically after reboot.

Example:

```text
/tmp/test.txt
```

Useful during penetration testing and scripting.

---

# /var

Contains files that change frequently.

Examples:

```text
/var/log
/var/cache
/var/spool
```

Cybersecurity professionals frequently analyze logs stored here.

Important files:

```text
/var/log/syslog
/var/log/auth.log
```

---

# /usr

Contains user applications and utilities.

Examples:

```text
/usr/bin
/usr/lib
/usr/share
```

Most installed software lives here.

---

# /opt

Used for optional or third-party software.

Examples:

```text
/opt/google
/opt/discord
```

---

# /media

Used for automatically mounted removable devices.

Examples:

```text
/media/prince/USB
/media/prince/DVD
```

---

# /mnt

Used for manually mounted filesystems.

Example:

```bash
sudo mount /dev/sdb1 /mnt
```

---

# Absolute Path

An absolute path starts from the root directory.

Example:

```text
/home/prince/Documents/notes.txt
```

---

# Relative Path

A relative path starts from the current directory.

Example:

```text
Documents/notes.txt
```

---

# Current Directory (.)

Represents the current directory.

Example:

```bash
ls .
```

---

# Parent Directory (..)

Represents the parent directory.

Example:

```bash
cd ..
```

---

# Hidden Files

Files beginning with `.` are hidden.

Examples:

```text
.bashrc
.profile
.gitconfig
```

View hidden files:

```bash
ls -la
```

---

# Filesystem Navigation Example

```bash
pwd
ls
cd Documents
pwd
cd ..
cd ~
```

---

# Why Linux Filesystem Knowledge Matters in Cybersecurity

Linux filesystem knowledge is essential for:

- Privilege escalation
- Log analysis
- User enumeration
- Malware analysis
- System administration
- Incident response
- Penetration testing

Important locations for security professionals:

| Directory | Purpose |
|-----------|---------|
| `/etc` | Configuration files |
| `/var/log` | Logs |
| `/home` | User files |
| `/tmp` | Temporary files |
| `/proc` | Process information |
| `/dev` | Devices |
| `/root` | Administrator files |

---

# Key Takeaways

- Linux uses a single hierarchical filesystem.
- Everything starts from the root directory `/`.
- Configuration files are stored in `/etc`.
- Logs are stored in `/var/log`.
- User files are stored in `/home`.
- Temporary files are stored in `/tmp`.
- Understanding the filesystem is fundamental for Linux administration and cybersecurity.