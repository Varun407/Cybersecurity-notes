# Introduction to Operating System Security

## What is an Operating System?

An **Operating System (OS)** is software that acts as a bridge between hardware and applications.

### Examples of Operating Systems
- Windows
- Linux
- macOS
- Android
- iOS
- Chrome OS
- AIX
- Solaris

### Examples of Applications (Not Operating Systems)
- Thunderbird
- Firefox
- Chrome
- WhatsApp
- Telegram

---

## Hardware vs Operating System

### Hardware
Physical components of a computer:
- CPU
- RAM
- Keyboard
- Mouse
- Monitor
- Printer
- USB Drive

### Operating System
Manages hardware and allows applications to use system resources safely and efficiently.

```
Applications
      ↑
Operating System
      ↑
Hardware
```

---

# CIA Triad

Operating system security focuses on protecting:

## Confidentiality
Only authorized users can access data.

### Examples
- Personal photos
- Messages
- Passwords
- Banking information

---

## Integrity
Data should not be modified without authorization.

### Examples
- Prevent file tampering
- Prevent unauthorized changes

---

## Availability
Systems and data should be accessible when needed.

### Examples
- Accessing files anytime
- Using applications without interruption

---

# Common Operating System Security Issues

## 1. Weak Passwords

Authentication verifies a user's identity.

### Authentication Methods

#### Something You Know
- Password
- PIN

#### Something You Are
- Fingerprint
- Face Recognition

#### Something You Have
- Mobile Phone
- Security Token

---

### Common Weak Password Examples

- 123456
- password
- qwerty
- 123456789
- iloveyou
- monkey
- dragon

### Characteristics of Strong Passwords

- Long
- Unique
- Difficult to guess
- Mix of letters, numbers, and symbols

Example:
```
LearnM00r
```

---

## 2. Weak File Permissions

Follow the **Principle of Least Privilege**:

> Users should only have access to what they need.

### Risks

#### Confidentiality Risk
Unauthorized users can read sensitive files.

#### Integrity Risk
Unauthorized users can modify files.

---

## 3. Malicious Programs

Malware can affect confidentiality, integrity, and availability.

### Trojan Horse

- Appears legitimate
- Gives attackers access to a system

### Ransomware

- Encrypts files
- Makes data inaccessible
- Attacker demands payment for decryption

---

# Practical Linux Security Example

## Useful Linux Commands

### Check Current User

```bash
whoami
```

Displays the currently logged-in user.

---

### Connect to a Remote Linux System

```bash
ssh username@IP
```

Example:

```bash
ssh sammie@MACHINE_IP
```

---

### List Files

```bash
ls
```

Shows files and directories.

---

### View File Contents

```bash
cat filename
```

Example:

```bash
cat flag.txt
```

---

### View Command History

```bash
history
```

Shows previously executed commands.

Useful during investigations because users may accidentally expose sensitive information.

---

### Switch User

```bash
su - username
```

Example:

```bash
su - root
```

Used to switch to another user account.

---

# Key Security Lessons

- Operating systems protect hardware, applications, and user data.
- The CIA Triad is the foundation of security.
- Weak passwords are one of the most common attack vectors.
- Use strong and unique passwords for every account.
- Apply the Principle of Least Privilege.
- Malware can compromise confidentiality, integrity, and availability.
- Linux commands such as `whoami`, `ssh`, `ls`, `cat`, `history`, and `su` are essential for security investigations.
- Command history can reveal sensitive information accidentally exposed by users.

---

# Quick Revision

### CIA Triad
- Confidentiality
- Integrity
- Availability

### Authentication Factors
- Something you know
- Something you are
- Something you have

### Malware Examples
- Trojan Horse
- Ransomware

### Important Commands

```bash
whoami     # Current user
ssh        # Remote login
ls         # List files
cat        # Read file contents
history    # Command history
su         # Switch user
```
