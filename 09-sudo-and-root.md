# Sudo and Root in Linux

## Introduction

Linux is designed as a multi-user operating system where different users have different levels of access. To protect the operating system from accidental or unauthorized changes, Linux separates normal user privileges from administrative privileges.

The **root user** has unrestricted control over the entire system, while **sudo (Super User Do)** allows authorized users to temporarily perform administrative tasks without logging in directly as the root user.

Understanding the difference between **root** and **sudo** is essential for:

- Linux Administration
- Cybersecurity
- Ethical Hacking
- Penetration Testing
- DevOps
- Server Management

---

# What is the Root User?

The **root user** is the superuser in Linux.

Characteristics:

- User ID (UID) = 0
- Has complete control over the system
- Can read, modify, or delete any file
- Can install or remove software
- Can create or delete users
- Can change system settings
- Can stop or start system services

Example:

```bash
whoami
```

Output

```text
root
```

---

# Why is Root Powerful?

The root account can:

- Access all files
- Change passwords for any user
- Modify system configuration
- Manage hardware
- Install kernels
- Shutdown or reboot the system
- Configure networking
- Manage permissions

Because of these abilities, the root account should be used carefully.

---

# Risks of Using Root

Logging in directly as root is dangerous because:

- One wrong command can damage the entire system.
- Malware running as root can take complete control.
- There is no protection from accidental mistakes.

Example:

```bash
rm -rf /
```

This command attempts to delete the entire filesystem.

- Never run commands you do not understand.

---

# What is sudo?

`sudo` stands for **Super User Do**.

It allows a normal user to execute a command with administrative privileges.

Syntax

```bash
sudo command
```

Example

```bash
sudo apt update
```

Instead of logging in as root, only this command runs with elevated privileges.

---

# Why Use sudo?

Advantages:

- Better security
- Temporary administrative access
- Logs administrative actions
- Reduces accidental mistakes
- No need to share the root password

---

# Checking Your Current User

```bash
whoami
```

Example Output

```text
prince
```

---

# Checking Your User ID

```bash
id
```

Example

```text
uid=1000(prince)
gid=1000(prince)
groups=1000(prince),27(sudo)
```

If you belong to the **sudo** group, you can use administrative commands.

---

# Running Commands as Root

Example

```bash
sudo mkdir /test
```

Creates a directory in the root filesystem.

---

Example

```bash
sudo apt install nmap
```

Installs Nmap with administrator privileges.

---

# Becoming Root Temporarily

Open a root shell

```bash
sudo -i
```

or

```bash
sudo su
```

Prompt changes

```text
root@ubuntu:~#
```

Exit root

```bash
exit
```

---

# Difference Between sudo and su

## sudo

Runs a single command as root.

```bash
sudo apt update
```

---

## su

Switches to another user.

```bash
su username
```

Switch to root

```bash
su -
```

Requires the root password.

---

# sudo vs su

| sudo | su |
|------|----|
| Runs one command as root | Switches to another user |
| Uses your password | Usually requires the target user's password |
| More secure | Less secure if root login is enabled |
| Recommended | Used less frequently on modern systems |

---

# Checking sudo Permissions

```bash
sudo -l
```

Displays the commands you are allowed to execute with sudo.

---

# Sudo Group

Most Linux distributions use the **sudo** group (or **wheel** on some systems).

Check group membership

```bash
groups
```

Example

```text
prince sudo docker
```

---

# Adding a User to the sudo Group

Ubuntu/Debian

```bash
sudo usermod -aG sudo username
```

Fedora/RHEL

```bash
sudo usermod -aG wheel username
```

---

# Removing a User from sudo

Ubuntu

```bash
sudo deluser username sudo
```

---

# Changing the Root Password

```bash
sudo passwd root
```

---

# Locking the Root Account

Some Linux distributions disable direct root login.

Lock root

```bash
sudo passwd -l root
```

Unlock root

```bash
sudo passwd -u root
```

---

# The sudoers File

The file that controls sudo permissions is:

```text
/etc/sudoers
```

Never edit it directly with a normal text editor.

Use:

```bash
sudo visudo
```

This checks the file for syntax errors before saving.

---

# Logging sudo Commands

Most Linux systems record sudo activity.

Common log file

```text
/var/log/auth.log
```

or

```text
/var/log/secure
```

Useful for:

- Security audits
- Incident response
- Digital forensics

---

# Practical Examples

Update package list

```bash
sudo apt update
```

---

Install Git

```bash
sudo apt install git
```

---

Restart SSH service

```bash
sudo systemctl restart ssh
```

---

View protected file

```bash
sudo cat /etc/shadow
```

---

Change file ownership

```bash
sudo chown prince notes.txt
```

---

# Common Mistakes

## Running Everything as Root

Avoid working as root for everyday tasks.

Instead of

```bash
sudo -i
```

for hours, use

```bash
sudo command
```

only when needed.

---

## Editing Protected Files Without sudo

Incorrect

```bash
nano /etc/hosts
```

Correct

```bash
sudo nano /etc/hosts
```

---

## Forgetting exit

After using

```bash
sudo -i
```

remember to leave the root shell.

```bash
exit
```

---

# Cybersecurity Perspective

Attackers often try to gain **root privileges** because they provide complete control over a system.

Common privilege escalation techniques include:

- Exploiting vulnerable SUID binaries
- Misconfigured sudo permissions
- Weak file permissions
- Kernel vulnerabilities
- Password reuse
- Misconfigured services

As a defender, always:

- Grant sudo access only when necessary.
- Audit `/etc/sudoers` regularly.
- Monitor sudo logs.
- Apply the Principle of Least Privilege.

---

# Summary

The **root** account has complete administrative control over a Linux system, while **sudo** provides temporary administrative privileges to authorized users. Using `sudo` instead of working directly as root improves security, accountability, and system stability. Every Linux administrator and cybersecurity professional should understand how sudo works, how permissions are managed, and how to use administrative privileges safely.

---

