# MITRE ATT&CK Framework

## What is MITRE?

MITRE is a non-profit organization that conducts research and develops frameworks, tools, and standards used throughout the cybersecurity industry.

Some of MITRE's major cybersecurity projects include:

```text
ATT&CK
CAR
D3FEND
ENGAGE
AEP
ATLAS
AADAPT
```

MITRE is also responsible for maintaining:

```text
CVE
(Common Vulnerabilities and Exposures)
```

which is the global catalog of publicly known vulnerabilities.

---

# Why MITRE Matters

MITRE provides:

```text
Common Language

Threat Intelligence Standards

Detection Frameworks

Defensive Frameworks

Adversary Emulation Resources
```

This allows security teams worldwide to communicate consistently.

---

# MITRE ATT&CK Framework

## What is ATT&CK?

ATT&CK stands for:

```text
Adversarial Tactics,
Techniques,
and
Common Knowledge
```

It is a knowledge base of real-world attacker behavior.

Instead of focusing on malware families or threat actor names, ATT&CK focuses on:

```text
What attackers do
```

---

# ATT&CK Purpose

ATT&CK helps organizations understand:

```text
How attackers gain access

How attackers maintain access

How attackers move through networks

How attackers steal data

How attackers achieve objectives
```

---

# ATT&CK Core Concepts

## Tactic

### Definition

The attacker's objective.

```text
WHY the attacker is doing something
```

Example:

```text
Credential Access
```

Goal:

```text
Steal credentials
```

---

## Technique

### Definition

The method used to achieve the objective.

```text
HOW the attacker achieves the goal
```

Example:

```text
Credential Dumping
```

Technique ID:

```text
T1003
```

---

## Sub-Technique

A more detailed version of a technique.

Example:

```text
Credential Dumping
        ↓
LSASS Memory
```

---

## Procedure

The exact implementation used.

Example:

```text
Mimikatz

ProcDump

Custom Malware
```

---

# ATT&CK Structure

ATT&CK organizes attacker behavior into tactics.

Each tactic contains:

```text
Techniques
      ↓
Sub-Techniques
```

---

# Enterprise ATT&CK Matrix

The ATT&CK Matrix is the most widely used view.

It represents the attack lifecycle.

```text
Reconnaissance
↓
Resource Development
↓
Initial Access
↓
Execution
↓
Persistence
↓
Privilege Escalation
↓
Defense Evasion
↓
Credential Access
↓
Discovery
↓
Lateral Movement
↓
Collection
↓
Command and Control
↓
Exfiltration
↓
Impact
```

---

# Important ATT&CK Tactics

## Reconnaissance

### Goal

Gather information about the target.

Examples:

```text
Employee Enumeration

Domain Research

Open Source Intelligence

Phishing Target Identification
```

---

## Initial Access

### Goal

Gain entry into the target environment.

Examples:

```text
Phishing

Exploiting Public-Facing Applications

Valid Accounts

Drive-by Compromise
```

---

## Execution

### Goal

Run malicious code.

Examples:

```text
PowerShell

Command Shell

Scripts

Malicious Documents
```

---

## Persistence

### Goal

Maintain long-term access.

Examples:

```text
Scheduled Tasks

Services

Registry Run Keys

Create Account
```

---

## Privilege Escalation

### Goal

Gain elevated permissions.

Examples:

```text
Token Manipulation

Exploitation

Bypass UAC
```

---

## Defense Evasion

### Goal

Avoid detection.

Examples:

```text
Hide Artifacts

Obfuscation

Disable Security Tools

Timestomping
```

Example Technique:

```text
Hide Artifacts

ID:
T1564
```

---

## Credential Access

### Goal

Steal credentials.

Examples:

```text
Credential Dumping

Keylogging

Brute Force

Password Spraying
```

---

## Discovery

### Goal

Understand the environment.

Examples:

```text
Account Discovery

Network Discovery

File Discovery

Process Discovery
```

---

## Lateral Movement

### Goal

Move to other systems.

Examples:

```text
RDP

PsExec

SMB

Remote Services
```

---

## Collection

### Goal

Gather target information.

Examples:

```text
Documents

Emails

Browser Data

Screenshots
```

---

## Command and Control

### Goal

Communicate with compromised hosts.

Examples:

```text
HTTP

HTTPS

DNS

WebSockets
```

---

## Exfiltration

### Goal

Steal data.

Examples:

```text
Cloud Storage

Encrypted Archives

DNS Tunneling
```

---

## Impact

### Goal

Disrupt operations.

Examples:

```text
Ransomware

Disk Wipe

Data Destruction

DoS
```

---

# ATT&CK IDs

Every ATT&CK technique has a unique identifier.

Examples:

```text
T1003
Credential Dumping

T1564
Hide Artifacts

T1136
Create Account
```

These IDs are used globally.

---

# Why ATT&CK IDs Matter

Instead of saying:

```text
The attacker used a credential theft technique.
```

You can say:

```text
T1003 - Credential Dumping
```

This removes ambiguity.

---

# ATT&CK Navigator

## What is Navigator?

A visualization tool built around ATT&CK.

Allows analysts to:

```text
Highlight Techniques

Map Threat Groups

Track Detection Coverage

Perform Gap Analysis
```

---

# ATT&CK in Security Operations

## SOC Analysts

Use ATT&CK to:

```text
Investigate Alerts

Understand Attacker Activity

Prioritize Incidents
```

---

## Detection Engineers

Use ATT&CK to:

```text
Map SIEM Rules

Improve Coverage

Identify Detection Gaps
```

---

## Incident Responders

Use ATT&CK to:

```text
Reconstruct Attacks

Build Timelines

Understand Adversary Actions
```

---

## Threat Intelligence Teams

Use ATT&CK to:

```text
Track Threat Actors

Analyze Campaigns

Map TTPs
```

---

## Red Teams

Use ATT&CK to:

```text
Emulate Adversaries

Test Security Controls

Validate Detection Logic
```

---

# Threat Intelligence and ATT&CK

## Why ATT&CK Is Important for CTI

Threat intelligence reports often contain:

```text
Threat Actor

Malware

Infrastructure

Observed TTPs
```

ATT&CK converts these into standardized behavior.

---

# Example Threat Actor Analysis

## APT33

### Overview

Suspected Iranian threat group.

Active since:

```text
2013+
```

Known for targeting:

```text
Aviation

Energy

Government
```

---

# Example Mapping

## Cloud Accounts

Technique:

```text
T1078.004
Cloud Accounts
```

Used to abuse:

```text
Microsoft 365

Cloud Services
```

---

# Associated Tool

```text
Ruler
```

Used with compromised Office 365 accounts.

---

# Example Mitigation

```text
User Account Management
```

Actions:

```text
Remove Inactive Accounts

Review Permissions

Disable Unused Accounts
```

---

# Example Detection

Detection Strategy:

```text
DET0546
```

Purpose:

```text
Detect Abused Cloud Accounts
```

---

# Threat Group Example

## Mustang Panda

Group ID:

```text
G0129
```

Country:

```text
China
```

---

# Known Behavior

Uses:

```text
Phishing

Scheduled Tasks

Defense Evasion

Credential Theft
```

---

# Reconnaissance Technique

```text
T1598
Phishing for Information
```

---

# Known Tool

```text
Cobalt Strike
```

Can be used for:

```text
Access Token Manipulation

Command & Control

Post Exploitation
```

---

# MITRE CAR

## What is CAR?

CAR stands for:

```text
Cyber Analytics Repository
```

---

# Purpose

Transforms ATT&CK techniques into:

```text
Detection Analytics

Detection Logic

SIEM Queries
```

---

# Why CAR Matters

ATT&CK tells us:

```text
What attackers do
```

CAR tells us:

```text
How to detect it
```

---

# CAR Components

Includes:

```text
Detection Theory

Pseudocode

Splunk Queries

EQL Examples

Detection Rationales
```

---

# Example

```text
CAR-2020-09-001
```

Focus:

```text
Scheduled Task File Access
```

---

# CAR Analytic Types

Examples:

```text
Situational Awareness

Anomaly Detection

Threat Detection
```

---

# Example

```text
CAR-2019-07-001
```

Technique:

```text
Access Permission Modification
```

Tactic:

```text
Defense Evasion
```

Type:

```text
Situational Awareness
```

---

# MITRE D3FEND

## What is D3FEND?

D3FEND stands for:

```text
Detection

Denial

Disruption

Framework

Empowering

Network

Defense
```

---

# ATT&CK vs D3FEND

## ATT&CK

Shows:

```text
Attacker Techniques
```

---

## D3FEND

Shows:

```text
Defensive Countermeasures
```

---

# Example

## ATT&CK

```text
Credential Theft
```

---

## D3FEND

```text
Credential Rotation

Multi-Factor Authentication

Account Monitoring
```

---

# Example D3FEND Technique

## Credential Rotation

ID:

```text
D3-CRO
```

Purpose:

```text
Prevent Reuse of Stolen Credentials
```

---

# User Behavior Analysis

A D3FEND defensive category.

Example Sub-Technique:

```text
User Geolocation Logon Pattern Analysis

D3-UGLPA
```

---

# Purpose

Detect:

```text
Impossible Travel

Abnormal Login Locations

Account Compromise
```

---

# Digital Artifact Used

```text
Network Traffic
```

---

# Other MITRE Projects

## ENGAGE

Adversary engagement framework.

Helps:

```text
Deception

Threat Hunting

Adversary Interaction
```

---

## ATT&CK Emulation Plans (AEP)

Provides:

```text
Real Adversary Simulations
```

Used by:

```text
Purple Teams

Red Teams

Detection Engineers
```

---

## CALDERA

Automated adversary emulation platform.

Supports:

```text
Red Teaming

Purple Teaming

Detection Validation
```

Uses ATT&CK techniques directly.

---

# ATLAS

## Purpose

Threat framework for:

```text
Artificial Intelligence

Machine Learning Systems
```

---

# Example

Technique:

```text
LLM Prompt Obfuscation

AML.T0068
```

Tactic:

```text
Defense Evasion
```

---

# AADAPT

## Purpose

Threat framework for:

```text
Blockchain

Cryptocurrency

Digital Assets
```

---

# Example Technique

```text
Scrape Blockchain Data

ADT3025
```

---

# ATT&CK Investigation Workflow

When investigating alerts, ask:

```text
What ATT&CK tactic is involved?

What ATT&CK technique is being used?

Which ATT&CK ID matches?

What detection opportunities exist?

What mitigations are available?
```

---

# SOC Analyst Examples

## Phishing Email

```text
Initial Access
```

---

## PowerShell Alert

```text
Execution
```

---

## Mimikatz Detection

```text
Credential Access

T1003
```

---

## Scheduled Task Created

```text
Persistence
```

---

## Beaconing Traffic

```text
Command and Control
```

---

## Data Transfer to External Host

```text
Exfiltration
```

---

# Quick Revision

## ATT&CK

```text
Attacker Behavior Framework
```

Answers:

```text
How attackers operate
```

---

## CAR

```text
Detection Analytics Framework
```

Answers:

```text
How to detect attackers
```

---

## D3FEND

```text
Defensive Countermeasure Framework
```

Answers:

```text
How to stop attackers
```

---

## CALDERA

```text
Automated Adversary Emulation
```

---

## ATLAS

```text
AI Threat Framework
```

---

## AADAPT

```text
Blockchain Threat Framework
```

---

# Final Takeaway

```text
ATT&CK
=
Attacker Playbook

CAR
=
Detection Playbook

D3FEND
=
Defender Playbook

Together
=
Threat-Informed Defense
```
