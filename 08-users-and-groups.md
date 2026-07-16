# Users and Groups in Linux

## Introduction

Linux is a multi-user operating system, meaning multiple users can work on the same system simultaneously. To ensure security and proper access control, Linux organizes users into **users** and **groups**.

Each user has a unique identity, and groups help manage permissions for multiple users at once.

Understanding users and groups is essential for:

- Linux Administration
- Server Management
- System Security
- DevOps
- Ethical Hacking
- Penetration Testing

---

# Why Users and Groups Matter

Users and groups help:

- Control access to files and directories
- Prevent unauthorized access
- Separate administrative and normal users
- Manage shared resources
- Improve system security

Example:

A web server can have one user for running services and another for administration, reducing security risks.

---

# Types of Users

Linux has three main types of users.

## 1. Root User

The root user is the superuser with complete control over the system.

Characteristics:

- User ID (UID) = 0
- Can access all files
- Can install or remove software
- Can create and delete users
- Can change system settings

Check current user:

```bash
whoami
```

Output

```text
root
```

---

## 2. Regular User

A regular user has limited permissions.

Example:

```text
prince
```

Regular users:

- Create files
- Run applications
- Cannot modify system files without permission

---

## 3. System Users

System users are created automatically for services.

Examples:

```text
www-data
mysql
postgres
daemon
```

These users usually cannot log in.

---

# User Identification

Each user has:

| Item | Description |
|------|-------------|
| Username | Login name |
| UID | User ID |
| GID | Primary Group ID |
| Home Directory | Personal folder |
| Login Shell | Default shell |

Example

```bash
id
```

Output

```text
uid=1000(prince)
gid=1000(prince)
groups=1000(prince),27(sudo)
```

---

# User Information Files

## /etc/passwd

Stores basic user information.

View:

```bash
cat /etc/passwd
```

Example

```text
prince:x:1000:1000:Prince:/home/prince:/bin/bash
```

Fields:

| Field | Meaning |
|-------|---------|
| prince | Username |
| x | Password placeholder |
| 1000 | UID |
| 1000 | GID |
| Prince | Comment |
| /home/prince | Home Directory |
| /bin/bash | Login Shell |

---

## /etc/shadow

Stores encrypted passwords.

View (requires root):

```bash
sudo cat /etc/shadow
```

Example

```text
prince:$6$...
```

Only root can access this file.

---

## /etc/group

Stores group information.

```bash
cat /etc/group
```

Example

```text
sudo:x:27:prince
```

Fields:

| Field | Meaning |
|-------|---------|
| sudo | Group name |
| x | Password placeholder |
| 27 | GID |
| prince | Members |

---

# Groups in Linux

A group is a collection of users.

Advantages:

- Easier permission management
- Shared file access
- Better security

Example

```
Developers

├── Alice
├── Bob
└── Charlie
```

Assign permissions once to the group instead of each user individually.

---

# Primary and Secondary Groups

## Primary Group

Assigned when a user is created.

Check:

```bash
id username
```

---

## Secondary Groups

Additional groups a user belongs to.

Example

```text
sudo
docker
developers
```

---

# Viewing Users

Current user

```bash
whoami
```

Logged-in users

```bash
who
```

Detailed login information

```bash
w
```

Current user's UID and groups

```bash
id
```

---

# Creating Users

Create a new user

```bash
sudo useradd john
```

Create with home directory

```bash
sudo useradd -m john
```

Create with Bash shell

```bash
sudo useradd -m -s /bin/bash john
```

---

# Setting Password

```bash
sudo passwd john
```

Follow the prompts to set a password.

---

# Deleting Users

Delete user only

```bash
sudo userdel john
```

Delete user and home directory

```bash
sudo userdel -r john
```

---

# Modifying Users

Change login shell

```bash
sudo usermod -s /bin/zsh john
```

Lock account

```bash
sudo usermod -L john
```

Unlock account

```bash
sudo usermod -U john
```

---

# Creating Groups

Create a group

```bash
sudo groupadd developers
```

---

# Deleting Groups

```bash
sudo groupdel developers
```

---

# Modifying Groups

Rename a group

```bash
sudo groupmod -n dev developers
```

---

# Adding Users to Groups

```bash
sudo usermod -aG developers john
```

The `-aG` options mean:

- `-a` → Append (don't remove existing groups)
- `-G` → Secondary groups

Check group membership

```bash
groups john
```

---

# Removing Users from Groups

```bash
sudo gpasswd -d john developers
```

---

# Changing Ownership

Change owner

```bash
sudo chown john file.txt
```

Change owner and group

```bash
sudo chown john:developers file.txt
```

---

# Changing Group

```bash
sudo chgrp developers file.txt
```

---

# Switching Users

Switch to another user

```bash
su john
```

Switch to root

```bash
sudo -i
```

Return to previous user

```bash
exit
```

---

# Sudo

`sudo` allows a permitted user to execute commands as another user, usually root.

Example

```bash
sudo apt update
```

Advantages:

- Better security than logging in directly as root
- Logs administrative actions
- Reduces accidental system damage

---

# Practical Examples

Create a user

```bash
sudo useradd -m alice
```

Set password

```bash
sudo passwd alice
```

Create group

```bash
sudo groupadd pentesters
```

Add user to group

```bash
sudo usermod -aG pentesters alice
```

Verify

```bash
groups alice
```

---

# Common Mistakes

## Forgetting `-a` with `usermod`

Incorrect

```bash
sudo usermod -G developers john
```

This replaces all existing secondary groups.

Correct

```bash
sudo usermod -aG developers john
```

---

## Deleting User Without Removing Home Directory

```bash
sudo userdel john
```

Leaves `/home/john` behind.

Use

```bash
sudo userdel -r john
```

---

## Running Everything as Root

Avoid using the root account for everyday tasks.

Use `sudo` only when needed.

---


# Summary

Linux manages access through users and groups. Each user has a unique identity, and groups simplify permission management for multiple users. Commands such as `useradd`, `usermod`, `groupadd`, `passwd`, and `chown` are essential for managing accounts securely. Understanding users and groups is a fundamental skill for Linux administration, DevOps, and cybersecurity.

---

