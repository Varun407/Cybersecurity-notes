# Operating Systems Introduction - Revision Notes

## What is an Operating System (OS)?

An Operating System (OS) is the software that acts as a bridge between:

```text
User
↓
Applications
↓
Operating System
↓
Hardware
```

**Examples:**

* Windows
* Linux (Ubuntu, Debian, Fedora)
* macOS
* Android
* iOS

---

# Privilege Levels

## Kernel Space

* Highest privilege level
* Direct access to hardware
* Runs the kernel
* Manages CPU, RAM, storage, and devices

## User Space

* Where applications run
* Limited permissions
* Cannot directly access hardware
* Uses system calls to communicate with the kernel

**Examples:**

* Browser
* Media Player
* Text Editor

---

# Core Responsibilities of an OS

## Process Management

* Creates processes
* Schedules CPU time
* Prioritizes tasks
* Terminates processes

**Example:** Running multiple applications simultaneously.

---

## Memory Management

* Allocates RAM
* Protects memory spaces
* Reclaims unused memory
* Uses virtual memory when RAM is low

---

## File System Management

* Manages files and folders
* Handles file paths and names
* Controls permissions
* Maintains metadata

---

## User Management

* Manages user accounts
* Handles authentication
* Controls permissions and access

---

## Device Management

* Loads device drivers
* Manages hardware communication
* Provides hardware abstraction

**Examples:**

* Keyboard
* Mouse
* Printer
* USB devices

---

# Operating System Security

## Authentication

Verifies user identity using:

* Passwords
* Fingerprints
* Face recognition

## Permissions

Controls:

* Read
* Write
* Execute

## Isolation

* Separates applications and processes
* Improves security and stability

## System Protection

* Protects critical system files and settings

---

# OS Interfaces

## GUI (Graphical User Interface)

Uses:

* Windows
* Icons
* Menus
* Buttons

**Advantages:**

* Easy to use
* Beginner friendly

---

## CLI (Command Line Interface)

Interaction through text commands.

```bash
ls
pwd
cd
mkdir
```

**Advantages:**

* Faster
* More control
* Supports automation

---

# Types of Operating Systems

## Desktop OS

Used for:

* Personal computing
* Gaming
* Productivity

**Examples:**

* Windows
* macOS
* Ubuntu Desktop

---

## Server OS

Used for:

* Web hosting
* Databases
* Cloud services

**Examples:**

* Ubuntu Server
* Debian
* Windows Server

---

## Mobile OS

Used for:

* Smartphones
* Tablets

**Examples:**

* Android
* iOS

---

## Embedded OS

Used for:

* Routers
* Smart TVs
* IoT devices

**Examples:**

* OpenWrt
* Ubuntu Core

---

## Virtual & Cloud OS

Used for:

* Virtual Machines
* Cloud environments
* Containers

**Examples:**

* Ubuntu LTS
* Amazon Linux
* Rocky Linux

---

# Linux Filesystem

## ext4

Most commonly used Linux filesystem.

**Features:**

* Reliable
* Fast
* Journaling support

Other filesystems:

* XFS
* Btrfs

---

# Key Terms

### Operating System (OS)

Software that manages hardware and software resources.

### Kernel

Core component of the OS that manages hardware and system resources.

### Process

A running instance of a program.

### GUI

Graphical interface using windows, icons, and menus.

### CLI

Text-based interface using commands.

### Authentication

Verification of a user's identity.

### Permissions

Rules that determine access rights.

### Isolation

Separation of processes for security and stability.

---

# Cybersecurity Relevance

Understanding operating systems is essential for:

* Linux Fundamentals
* Windows Fundamentals
* System Administration
* Networking
* Privilege Escalation
* Ethical Hacking
* Incident Response

**Remember:** The OS manages everything between applications and hardware.
