# Unified Kill Chain (UKC)

## What is the Unified Kill Chain?

The Unified Kill Chain (UKC) is a cybersecurity framework created by Paul Pols in 2017.

It combines concepts from:

* Lockheed Martin Cyber Kill Chain
* MITRE Corporation ATT&CK Framework

The purpose of UKC is to provide a complete view of how attackers operate from reconnaissance to achieving their final objectives.

---

# Why UKC Matters

Traditional Kill Chains focus mainly on:

```text
Reconnaissance
↓
Delivery
↓
Exploitation
↓
Command & Control
```

Modern attackers perform many more activities:

```text
Credential Theft
Privilege Escalation
Lateral Movement
Defense Evasion
Data Exfiltration
Impact Operations
```

UKC accounts for these activities.

---

# Key Advantages of UKC

## Modern Framework

```text
Released: 2017
Updated: 2022
```

Designed for today's threat landscape.

---

## Extremely Detailed

Contains:

```text
18 Attack Phases
```

Compared to traditional frameworks that contain only a few stages.

---

## Covers Entire Attack Lifecycle

Tracks:

```text
Pre-Compromise
Initial Access
Post-Exploitation
Objectives
```

---

## Reflects Real Attacks

Attackers rarely move linearly.

Example:

```text
Compromise System
      ↓
Recon Internal Network
      ↓
Privilege Escalation
      ↓
Recon Again
      ↓
Lateral Movement
```

UKC models this behavior.

---

# Relationship With MITRE ATT&CK

## UKC

Answers:

```text
Where is the attacker in the attack lifecycle?
```

---

## MITRE ATT&CK

Answers:

```text
How is the attacker performing the attack?
```

---

## Together

```text
UKC
+
MITRE ATT&CK
=
Complete Detection Strategy
```

---

# Understanding Threat Modelling

## What is Threat Modelling?

Threat modelling is the process of identifying:

* Critical systems
* Weaknesses
* Threats
* Attack paths
* Mitigations

---

# Threat Modelling Process

```text
Identify Assets
       ↓
Find Vulnerabilities
       ↓
Assess Risk
       ↓
Implement Security Controls
       ↓
Improve Security
```

---

# Why Threat Modelling Matters

Helps organizations:

```text
Reduce Risk

Understand Attack Surface

Prioritize Defenses

Improve Security Posture
```

---

# Common Threat Modelling Frameworks

## STRIDE

Focuses on:

```text
Spoofing
Tampering
Repudiation
Information Disclosure
Denial of Service
Elevation of Privilege
```

---

## DREAD

Risk assessment framework.

---

## CVSS

Measures vulnerability severity.

---

# Unified Kill Chain Structure

The UKC can be simplified into three major goals:

```text
IN
↓
THROUGH
↓
OUT
```

---

# Goal 1: IN (Initial Foothold)

## Objective

Gain access to the target environment.

---

# IN Phase Overview

```text
Reconnaissance
↓
Weaponization
↓
Social Engineering
↓
Exploitation
↓
Persistence
↓
Defense Evasion
↓
Command & Control
↓
Pivoting
```

---

# Reconnaissance

## Purpose

Gather information about the target.

---

# Information Collected

```text
Users

Employees

Credentials

Services

Applications

Network Layout

Domains
```

---

# Common Techniques

## Passive Recon

Examples:

```text
WHOIS

LinkedIn

Google Dorking

Social Media
```

---

## Active Recon

Examples:

```text
Port Scanning

Service Enumeration

Banner Grabbing
```

---

# SOC Detection Opportunities

Monitor:

```text
Port Scans

Enumeration Attempts

DNS Enumeration

Recon Traffic
```

---

# Weaponization

## Purpose

Prepare attack infrastructure.

---

# Examples

```text
Malware Creation

Exploit Development

Payload Creation

C2 Infrastructure Setup
```

---

# Social Engineering

## Purpose

Manipulate users into helping the attack.

---

# Examples

## Phishing

```text
Malicious Attachments

Malicious Links
```

---

## Credential Harvesting

Fake login portals.

---

## Impersonation

Examples:

```text
IT Support

Vendor

Engineer
```

---

# Exploitation

## Purpose

Execute code by abusing vulnerabilities.

---

# Examples

```text
Reverse Shell Upload

Web Exploitation

RCE Vulnerabilities

Macro Execution
```

---

# Indicators

```text
Unexpected Processes

PowerShell Execution

Suspicious Child Processes
```

---

# Persistence

## Purpose

Maintain long-term access.

---

# Examples

```text
Backdoors

Services

Scheduled Tasks

Registry Run Keys

Web Shells
```

---

# Defense Evasion

## Purpose

Avoid detection.

---

# Security Controls Targeted

```text
Antivirus

EDR

IDS

IPS

Firewalls
```

---

# Common Techniques

```text
Obfuscation

Timestomping

Masquerading

Disabling Security Tools
```

---

# Why Defense Evasion Is Important

Understanding evasion methods helps improve detection engineering.

---

# Command & Control (C2)

## Purpose

Create communication between attacker and victim.

---

# Common C2 Protocols

```text
HTTP

HTTPS

DNS

TCP
```

---

# Capabilities

```text
Execute Commands

Upload Malware

Download Files

Steal Data
```

---

# Pivoting

## Purpose

Use one compromised system to reach others.

---

# Example

```text
Internet
    ↓
Web Server
    ↓
Database Server
    ↓
Domain Controller
```

The attacker uses each compromise to reach deeper assets.

---

# Goal 2: THROUGH (Network Propagation)

## Objective

Expand access inside the environment.

---

# THROUGH Phase Overview

```text
Pivoting
↓
Discovery
↓
Privilege Escalation
↓
Execution
↓
Credential Access
↓
Lateral Movement
```

---

# Discovery

## Purpose

Understand the internal environment.

---

# Information Gathered

```text
Users

Computers

Shares

Applications

Network Topology

Permissions
```

---

# Common Commands

Examples:

```text
whoami

net user

net group

ipconfig

arp
```

---

# Privilege Escalation

## Purpose

Gain higher permissions.

---

# Targets

```text
SYSTEM

ROOT

Administrator

Privileged Service Accounts
```

---

# Indicators

```text
Privilege Abuse

Token Manipulation

Exploit Usage
```

---

# Execution

## Purpose

Run malicious code.

---

# Examples

```text
Remote Payloads

Scheduled Tasks

Malicious Scripts

Remote Trojans
```

---

# Credential Access

## Purpose

Steal authentication secrets.

---

# Targets

```text
Passwords

Hashes

Tokens

Kerberos Tickets
```

---

# Common Techniques

```text
Credential Dumping

Keylogging

Browser Credential Theft
```

---

# Example Tool

## Mimikatz

Used for:

```text
Credential Dumping

LSASS Access

Hash Extraction
```

---

# SOC Detection Opportunities

Monitor:

```text
LSASS Access

Credential Dumping

Security Log Events
```

---

# Lateral Movement

## Purpose

Move between systems.

---

# Common Techniques

```text
RDP

SMB

PsExec

WMI

Remote Services
```

---

# Goal

Reach valuable assets.

Examples:

```text
Database Servers

Domain Controllers

File Servers
```

---

# Goal 3: OUT (Actions on Objectives)

## Objective

Achieve the attacker's final mission.

---

# OUT Phase Overview

```text
Collection
↓
Exfiltration
↓
Impact
↓
Objectives
```

---

# Collection

## Purpose

Gather valuable information.

---

# Targets

```text
Documents

Databases

Emails

Browser Data

Audio

Video
```

---

# Exfiltration

## Purpose

Remove data from the environment.

---

# Common Techniques

```text
Encrypted Archives

HTTPS Uploads

Cloud Storage Abuse

DNS Tunneling
```

---

# Detection Opportunities

Monitor:

```text
Large Outbound Transfers

Unknown External IPs

Data Compression Activity

Encrypted Uploads
```

---

# Impact

## Purpose

Damage integrity or availability.

---

# Examples

## Ransomware

```text
File Encryption
```

---

## Disk Wiping

```text
Destroy Data
```

---

## Account Removal

```text
Lock Users Out
```

---

## Denial of Service

```text
Disrupt Services
```

---

# Objectives

## Purpose

Complete the mission.

---

# Common Objectives

## Financial Gain

Examples:

```text
Ransomware

Banking Theft

Fraud
```

---

## Espionage

Examples:

```text
Trade Secrets

Government Information

Research Data
```

---

## Reputation Damage

Examples:

```text
Data Leaks

Public Disclosure

Website Defacement
```

---

# CIA Triad Mapping

## Confidentiality

Compromised by:

```text
Collection

Exfiltration
```

---

## Integrity

Compromised by:

```text
Data Manipulation

Defacement

Unauthorized Changes
```

---

## Availability

Compromised by:

```text
Ransomware

DoS

Data Destruction
```

---

# UKC Investigation Workflow

When investigating an alert, ask:

```text
What phase is the attacker in?

What evidence supports it?

What is their next likely step?

Can we stop them here?
```

---

# SOC Analyst Examples

## Port Scan Alert

Likely Phase:

```text
Reconnaissance
```

---

## Phishing Email

Likely Phase:

```text
Social Engineering
```

---

## Reverse Shell Spawned

Likely Phase:

```text
Exploitation
```

---

## Registry Run Key Created

Likely Phase:

```text
Persistence
```

---

## Beaconing To External IP

Likely Phase:

```text
Command & Control
```

---

## Mimikatz Execution

Likely Phase:

```text
Credential Access
```

---

## Failed Admin Login Attempts

Likely Phase:

```text
Privilege Escalation
```

---

## Large Data Transfer To Unknown IP

Likely Phase:

```text
Exfiltration
```

---

# Quick Revision

## UKC Goals

```text
IN
↓
THROUGH
↓
OUT
```

---

## IN

```text
Gain Access
```

Phases:

```text
Reconnaissance
Weaponization
Social Engineering
Exploitation
Persistence
Defense Evasion
Command & Control
Pivoting
```

---

## THROUGH

```text
Expand Access
```

Phases:

```text
Discovery
Privilege Escalation
Execution
Credential Access
Lateral Movement
```

---

## OUT

```text
Achieve Objective
```

Phases:

```text
Collection
Exfiltration
Impact
Objectives
```

---

## Remember

```text
Cyber Kill Chain
=
Attack Lifecycle

MITRE ATT&CK
=
Attacker Techniques

Unified Kill Chain
=
Complete Attack Journey
```
