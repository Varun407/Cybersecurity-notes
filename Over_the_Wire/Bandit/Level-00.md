# Bandit Level 0

## Objective

Learn how to connect to a remote Linux system using SSH (Secure Shell).

The goal of this level is to successfully log in to the Bandit server.

---

# Concepts Learned

## What is SSH?

SSH (Secure Shell) is a secure network protocol used to remotely access and manage another computer over a network.

It provides:

* Encrypted communication
* Secure authentication
* Remote command execution
* File transfer capabilities

SSH is one of the most important tools used by:

* System Administrators
* SOC Analysts
* Security Engineers
* Penetration Testers
* Cloud Engineers

---

# Real-World Example

Imagine a company has a Linux web server running in a data center.

Instead of physically going to the server room, an administrator can connect remotely:

```bash
ssh admin@server-ip
```

After authentication, they receive a shell on the remote machine and can manage it from anywhere.

---

# SSH Connection Components

Example:

```bash
ssh username@hostname
```

### Components

| Component | Description                 |
| --------- | --------------------------- |
| ssh       | SSH client program          |
| username  | Account used for login      |
| @         | Separates username and host |
| hostname  | Remote system address       |

---

# Connecting to a Custom Port

By default SSH uses:

```text
Port 22
```

However, Bandit uses:

```text
Port 2220
```

To specify a different port:

```bash
ssh -p 2220 username@hostname
```

### Breakdown

| Option   | Meaning             |
| -------- | ------------------- |
| -p       | Specify port number |
| 2220     | Target SSH port     |
| username | User account        |
| hostname | Remote server       |

---

# Command Used

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

After executing:

1. SSH contacts the remote server.
2. Server presents its identity.
3. Client verifies the server fingerprint.
4. User enters password.
5. Authentication occurs.
6. Shell access is granted.

---

# First-Time SSH Connection

When connecting for the first time, SSH may display:

```text
The authenticity of host can't be established.
Are you sure you want to continue connecting (yes/no)?
```

This happens because:

* Your computer has never seen this server before.
* SSH wants to prevent man-in-the-middle attacks.

Accepting the fingerprint stores it in:

```text
~/.ssh/known_hosts
```

---

# Authentication Process

After connecting:

```text
bandit0@bandit.labs.overthewire.org's password:
```

The password is entered securely.

### Important

* Characters are not displayed.
* No asterisks (*) appear.
* This is normal behavior.

---

# Useful SSH Options

## Verbose Mode

```bash
ssh -v user@host
```

Shows detailed connection information.

Useful for troubleshooting.

---

## Very Verbose

```bash
ssh -vvv user@host
```

Provides extensive debugging output.

---

## Specify Identity File

```bash
ssh -i keyfile user@host
```

Uses a private key instead of a password.

Common in cloud environments.

---

## Specify Port

```bash
ssh -p 2220 user@host
```

Connects to a non-default SSH port.

---

# Files Related to SSH

## Known Hosts

```text
~/.ssh/known_hosts
```

Stores fingerprints of previously connected servers.

---

## SSH Configuration

```text
~/.ssh/config
```

Stores custom SSH settings.

Example:

```text
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit0
```

Then connect with:

```bash
ssh bandit
```

---

# SOC Analyst Perspective

A SOC analyst frequently encounters SSH-related events such as:

## Successful Logins

```text
Accepted password for user
```

## Failed Logins

```text
Failed password for user
```

## Brute Force Attempts

```text
Failed password for root
Failed password for admin
Failed password for test
```

Repeated failures often indicate password-guessing attacks.

---

# Key Takeaways

* SSH is the standard protocol for secure remote administration.
* Default SSH port is 22, but custom ports are common.
* The `-p` option specifies a custom port.
* SSH encrypts communication between client and server.
* First connections require host fingerprint verification.
* SSH is heavily used in cybersecurity, cloud computing, and system administration.

---

# Commands Learned

```bash
ssh
ssh -p
ssh -v
ssh -vvv
ssh -i
```

---

# Skills Gained

* Remote system access
* SSH authentication
* Working with custom ports
* Understanding host verification
* Basic Linux command-line interaction
* Security awareness regarding remote access protocols

---

# References

* OverTheWire Bandit Level 0
* OpenSSH Documentation
* Linux Manual Pages (`man ssh`)
