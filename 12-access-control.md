# Access Control in Linux

## Introduction

Access control is the process of restricting and managing access to files, directories, devices, and system resources. It ensures that only authorized users and processes can perform specific actions, helping protect data from unauthorized access, modification, or deletion.

Linux implements several layers of access control, starting with file ownership and permissions and extending to advanced security frameworks such as Access Control Lists (ACLs), SELinux, and AppArmor.

Access control is essential for:

- Linux Administration
- Cybersecurity
- Ethical Hacking
- Penetration Testing
- Digital Forensics
- DevOps

---

# What is Access Control?

Access control determines:

- Who can access a resource?
- What actions can they perform?
- Under what conditions is access allowed?

Example:

```
File: payroll.xlsx

Owner:
Alice

Permissions:
Read and Write

Group:
HR Team

Others:
No Access
```

Only authorized users can view or modify the file.

---

# Why is Access Control Important?

Proper access control helps:

- Protect sensitive data
- Prevent unauthorized changes
- Reduce security risks
- Enforce organizational policies
- Prevent privilege escalation
- Improve system stability

---

# Access Control Components

Linux access control is based on four main components:

- Authentication
- Authorization
- Permissions
- Ownership

---

# Authentication

Authentication verifies the identity of a user.

Common authentication methods:

- Username and password
- SSH keys
- Multi-Factor Authentication (MFA)
- Smart cards
- Biometrics

Example

```bash
login
```

The user must provide valid credentials before gaining access.

---

# Authorization

Authorization determines what an authenticated user is allowed to do.

Examples:

- Read a file
- Edit a configuration file
- Install software
- Restart services

Example

```bash
sudo apt update
```

Only users with sudo privileges can execute the command.

---

# Ownership

Every Linux file has:

- Owner
- Group

View ownership

```bash
ls -l
```

Example

```text
-rw-r--r-- 1 prince developers report.txt
```

Owner

```
prince
```

Group

```
developers
```

---

# Permissions

Linux uses three basic permissions.

| Permission | Symbol | Value |
|------------|--------|------|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |

Permissions apply to:

- Owner
- Group
- Others

Example

```
rwxr-xr--
```

---

# Permission Checking Order

Linux checks permissions in this order:

```
Owner

↓

Group

↓

Others
```

Once a matching category is found, Linux uses that permission set.

---

# Access Control Using chmod

Grant execute permission

```bash
chmod +x script.sh
```

Remove write permission

```bash
chmod -w file.txt
```

Numeric example

```bash
chmod 755 script.sh
```

---

# Access Control Using chown

Change file owner

```bash
sudo chown john report.txt
```

Change owner and group

```bash
sudo chown john:developers report.txt
```

---

# Access Control Using Groups

Groups simplify permission management.

Example

```
Developers

├── Alice
├── Bob
└── Charlie
```

Assign permissions once to the group instead of each user individually.

---

# Access Control Lists (ACLs)

Traditional Linux permissions allow only:

- One owner
- One group
- Others

ACLs provide more flexible permissions.

Example

Grant read permission to a specific user

```bash
setfacl -m u:john:r report.txt
```

View ACL

```bash
getfacl report.txt
```

ACLs are useful when multiple users need different permissions on the same file.

---

# Mandatory Access Control (MAC)

Mandatory Access Control enforces security policies defined by the operating system.

Users cannot bypass these policies.

Examples:

- SELinux
- AppArmor

Used in enterprise and security-focused Linux systems.

---

# Discretionary Access Control (DAC)

Linux uses DAC by default.

The owner of a file decides:

- Who can read
- Who can write
- Who can execute

Example

```bash
chmod 644 report.txt
```

The owner controls the permissions.

---

# Role-Based Access Control (RBAC)

RBAC assigns permissions based on user roles.

Example

```
Administrator

↓

Full Access
```

```
Developer

↓

Source Code Access
```

```
Guest

↓

Read Only
```

RBAC simplifies permission management in large organizations.

---

# Principle of Least Privilege

Users should receive only the permissions required to perform their tasks.

Example

A web server should not have permission to modify system files.

Benefits:

- Reduced attack surface
- Better security
- Easier auditing

---

# Practical Examples

View permissions

```bash
ls -l
```

Check current user

```bash
whoami
```

Check groups

```bash
groups
```

View user information

```bash
id
```

Change permissions

```bash
chmod 640 report.txt
```

Change ownership

```bash
sudo chown john report.txt
```

Grant ACL permission

```bash
setfacl -m u:alice:rw report.txt
```

View ACL

```bash
getfacl report.txt
```

---

# Common Mistakes

### Using 777 Permissions

```bash
chmod 777 file.txt
```

This allows anyone to read, write, and execute the file.

Avoid unless absolutely necessary.

---

### Giving Excessive sudo Access

Only trusted users should belong to the sudo group.

---

### Ignoring ACLs

When standard permissions are insufficient, use ACLs instead of making files world-writable.

---

# Cybersecurity Perspective

Access control is one of the first things security professionals check during system audits.

Common issues include:

- World-writable files
- Weak permissions
- Misconfigured ACLs
- Excessive sudo privileges
- Incorrect ownership
- Writable system files

Attackers often exploit poor access control to gain unauthorized access or escalate privileges.

---

# Summary

Access control is a fundamental security mechanism in Linux that regulates who can access system resources and what actions they can perform. Linux primarily uses **Discretionary Access Control (DAC)** through ownership and permissions, while advanced mechanisms like **ACLs**, **SELinux**, and **AppArmor** provide additional security. Proper access control helps protect systems from unauthorized access, supports the Principle of Least Privilege, and is essential for secure Linux administration and cybersecurity.

---