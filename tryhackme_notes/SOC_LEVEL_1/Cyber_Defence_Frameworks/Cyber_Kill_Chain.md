# Cyber Kill Chain

## What is the Cyber Kill Chain?

The Cyber Kill Chain is a framework developed by Lockheed Martin in 2011 to describe the stages an attacker follows during a cyber attack.

The idea is simple:

```text
If defenders can detect and stop an attacker
at any stage,

the attack fails.
```

---

# Why SOC Analysts Need It

The Cyber Kill Chain helps defenders:

* Understand attacker behavior
* Identify attack stages
* Improve detection coverage
* Build security controls
* Investigate incidents
* Break attacks before objectives are achieved

---

# Cyber Kill Chain Phases

```text
Reconnaissance
      ↓
Weaponization
      ↓
Delivery
      ↓
Exploitation
      ↓
Installation
      ↓
Command & Control
      ↓
Actions on Objectives
```

---

# Phase 1: Reconnaissance

## Purpose

The attacker gathers information about the target before launching the attack.

Think of this as:

```text
Research Phase
```

The attacker wants to learn:

* Employees
* Email addresses
* Technologies
* Public infrastructure
* Domains
* IP addresses
* Business operations

---

# OSINT (Open Source Intelligence)

OSINT is intelligence gathered from publicly available sources.

Sources include:

```text
Search Engines
Social Media
Blogs
Forums
News Articles
WHOIS Records
Public Databases
```

---

# Types of Reconnaissance

## Passive Recon

No direct interaction with the target.

Examples:

* LinkedIn research
* WHOIS lookups
* Google searches
* Social media collection

Hard to detect.

---

## Active Recon

Direct interaction with the target.

Examples:

```text
Port Scanning

Banner Grabbing

Social Engineering

Service Enumeration
```

More likely to generate logs and alerts.

---

# Common Recon Tools

## theHarvester

Collects:

```text
Emails
Names
Subdomains
IPs
URLs
```

---

## Hunter.io

Used for:

```text
Email Discovery
Domain Contacts
```

---

## OSINT Framework

Large collection of OSINT resources organized by category.

---

# SOC Detection Opportunities

Monitor for:

```text
Port Scans

Mass DNS Queries

Enumeration Attempts

Reconnaissance Traffic
```

---

# Phase 2: Weaponization

## Purpose

The attacker converts gathered intelligence into a weapon.

The payload is prepared before delivery.

---

# Important Terms

## Malware

Software designed to:

```text
Damage
Disrupt
Steal
Gain Access
```

---

## Exploit

Code that abuses a vulnerability.

---

## Payload

Malicious code executed on the victim system.

---

# Common Weaponization Activities

## Malicious Documents

Examples:

```text
Word Documents

Excel Files

PDF Files
```

Containing:

```text
Macros

VBA Scripts
```

---

## Malware Creation

Examples:

```text
Ransomware

Trojans

Worms

Backdoors
```

---

## Command & Control Setup

Attacker prepares infrastructure for:

```text
Remote Control

Data Theft

Additional Payload Delivery
```

---

# SOC Detection Opportunities

Monitor:

```text
Malware Samples

Sandbox Results

Suspicious Attachments

Threat Intelligence Feeds
```

---

# Phase 3: Delivery

## Purpose

The payload reaches the victim.

This is the transportation phase.

---

# Common Delivery Methods

## Phishing

Most common delivery method.

Victim receives:

```text
Malicious Link

Malicious Attachment
```

---

## Spear Phishing

Highly targeted phishing against a specific individual.

---

## USB Drop Attack

Attacker leaves infected USB devices in public places.

Examples:

```text
Parking Lots

Reception Areas

Coffee Shops
```

---

## Watering Hole Attack

The attacker compromises a website frequently visited by the target.

Victims unknowingly visit the infected site and become compromised.

---

# Delivery Workflow

```text
Attacker
    ↓
Delivery Method
    ↓
Victim Interaction
    ↓
Payload Executed
```

---

# SOC Detection Opportunities

Monitor:

```text
Email Gateways

Web Proxy Logs

Attachment Sandboxing

DNS Requests
```

---

# Phase 4: Exploitation

## Purpose

The malicious code executes successfully.

The attacker exploits a vulnerability or weakness.

---

# Common Exploitation Methods

## Macro Execution

Victim enables malicious macro.

---

## Known Vulnerabilities

Exploiting public CVEs.

Examples:

```text
Unpatched Systems

Outdated Applications
```

---

## Zero-Day Exploits

Previously unknown vulnerabilities.

No patch exists at the time of attack.

---

# Indicators of Exploitation

## Suspicious Processes

Examples:

```text
winword.exe → powershell.exe

excel.exe → cmd.exe
```

---

## Registry Modifications

Unexpected registry changes.

---

## Service Creation

New services created unexpectedly.

---

# SOC Detection Opportunities

Monitor:

```text
Process Trees

Command-Line Arguments

Registry Activity

Windows Event Logs
```

---

# Phase 5: Installation

## Purpose

The attacker establishes persistence.

Persistence ensures access remains after:

```text
Reboots

Logouts

Network Interruptions
```

---

# Common Persistence Methods

## Web Shells

Examples:

```text
shell.php

shell.aspx

shell.jsp
```

Allow remote control through a web server.

---

## Backdoors

Provide ongoing access.

Examples:

```text
RATs

Meterpreter Sessions
```

---

## Windows Services

Attackers create or modify services.

MITRE ATT&CK:

```text
T1543.003
Create or Modify System Process
```

---

## Registry Run Keys

Malware executes automatically at login.

Examples:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run

HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

---

## Startup Folder

Programs automatically launch when a user logs in.

---

# Timestomping

## Purpose

Hide malware activity.

---

## How It Works

Attackers modify:

```text
Creation Time

Modified Time

Access Time
```

Making malware appear legitimate.

---

# SOC Detection Opportunities

Monitor:

```text
Service Creation

Registry Changes

Startup Entries

File Timestamp Anomalies
```

---

# Phase 6: Command & Control (C2)

## Purpose

The attacker establishes communication with the compromised host.

This enables remote control.

---

# Beaconing

The infected host periodically contacts the attacker's server.

Example:

```text
Victim
   ↓
C2 Server
   ↓
Victim
   ↓
C2 Server
```

Repeated communication is called:

```text
Beaconing
```

---

# Common C2 Channels

## HTTP

Port:

```text
80
```

---

## HTTPS

Port:

```text
443
```

Blends into normal traffic.

---

## DNS Tunneling

Uses DNS traffic for communication.

Benefits:

```text
Stealthy

Often Allowed Through Firewalls
```

---

# SOC Detection Opportunities

Monitor:

```text
Beaconing Patterns

Suspicious DNS Requests

Repeated External Connections

Unknown Domains
```

Tools:

```text
Wireshark

Zeek

Suricata

EDR
```

---

# Phase 7: Actions on Objectives

## Purpose

The attacker achieves the mission objective.

Everything before this phase supports reaching this goal.

---

# Common Objectives

## Credential Theft

Examples:

```text
Passwords

Browser Credentials

Tokens
```

---

## Privilege Escalation

Gain elevated access.

Example:

```text
User → Administrator
```

---

## Internal Reconnaissance

Discover:

```text
Servers

Shares

Users

Applications
```

---

## Lateral Movement

Move between systems.

Examples:

```text
RDP

SMB

PsExec
```

---

## Data Exfiltration

Steal sensitive information.

Examples:

```text
Customer Data

Financial Data

Intellectual Property
```

---

## Backup Deletion

Examples:

```text
Shadow Copies

Backups
```

Often observed before ransomware deployment.

---

## Data Destruction

Examples:

```text
File Corruption

Database Wiping

System Sabotage
```

---

# SOC Detection Opportunities

Monitor:

```text
Large Data Transfers

Privilege Escalation Events

Lateral Movement

Backup Deletion

Credential Access
```

---

# Breaking the Kill Chain

The goal of defenders is to interrupt the attack before it reaches the final stage.

Example:

```text
Detect Phishing
        ↓
Block Delivery
        ↓
Attack Fails
```

Or:

```text
Detect C2 Beaconing
        ↓
Isolate Host
        ↓
Attack Fails
```

---

# Limitations of the Cyber Kill Chain

Although useful, the model has limitations.

---

## Focuses Mainly on Malware

Modern attacks may use:

```text
Cloud Abuse

Identity Attacks

Living-Off-The-Land Techniques
```

---

## Limited Coverage of Insider Threats

An insider already has legitimate access.

Traditional Kill Chain does not model these scenarios well.

---

## Modern Threats Are More Complex

Attackers:

```text
Use Multiple TTPs

Rotate Infrastructure

Abuse Legitimate Services
```

---

# Cyber Kill Chain vs MITRE ATT&CK

## Cyber Kill Chain

Answers:

```text
Where is the attacker in the attack lifecycle?
```

Focuses on stages.

---

## MITRE ATT&CK

Answers:

```text
How is the attacker performing the attack?
```

Focuses on techniques and behaviors.

---

# SOC Analyst Investigation Mindset

Whenever investigating an incident ask:

```text
Which Kill Chain phase are we observing?

What evidence supports it?

Can we stop the attack here?

What detections are missing?
```

---

# Quick Revision

## Cyber Kill Chain

```text
Reconnaissance
↓
Weaponization
↓
Delivery
↓
Exploitation
↓
Installation
↓
Command & Control
↓
Actions on Objectives
```

---

## Reconnaissance

```text
Information Gathering
OSINT
Email Harvesting
Scanning
```

---

## Weaponization

```text
Create Malware
Create Exploits
Prepare Payload
```

---

## Delivery

```text
Phishing
USB Drops
Watering Hole
```

---

## Exploitation

```text
Code Execution
Vulnerability Abuse
```

---

## Installation

```text
Persistence
Backdoors
Web Shells
Run Keys
```

---

## Command & Control

```text
Beaconing
HTTP
HTTPS
DNS Tunneling
```

---

## Actions on Objectives

```text
Credential Theft
Privilege Escalation
Lateral Movement
Data Exfiltration
Destruction
```

---

## Remember

```text
Kill Chain = Attack Lifecycle

Defender Goal =
Break The Chain Before Objectives Are Reached
```
