# Pyramid of Pain

## What is the Pyramid of Pain?

The Pyramid of Pain is a cybersecurity model created by David Bianco that shows how difficult it is for an attacker to change different indicators when defenders detect them.

The higher you detect within the pyramid, the more effort and resources an attacker must spend to continue their operation.

---

# Why It Matters

For SOC Analysts, Threat Hunters, and Incident Responders, the Pyramid of Pain helps answer:

```text
What should we detect?

What indicators provide the greatest impact?

How much effort will attackers need to evade our detection?
```

---

# Pyramid Structure

```text
                TTPs
              (Tough)

               Tools
           (Challenging)

        Network Artifacts
           (Annoying)

         Host Artifacts
           (Annoying)

          Domain Names
             (Easy)

           IP Addresses
             (Easy)

             Hashes
           (Trivial)
```

---

# Detection Philosophy

Lower levels:

```text
Easy for defenders
Easy for attackers to change
```

Higher levels:

```text
Harder to detect
Much harder for attackers to change
```

---

# Level 1: Hash Values (Trivial)

## What is a Hash?

A hash is a fixed-length value generated from data using a hashing algorithm.

Hashes uniquely identify files and are commonly used to identify malware.

---

## Common Hashing Algorithms

### MD5

```text
128-bit hash
```

Example:

```text
d41d8cd98f00b204e9800998ecf8427e
```

---

### SHA-1

```text
160-bit hash
```

Example:

```text
40 hexadecimal characters
```

---

### SHA-256

```text
256-bit hash
```

Example:

```text
64 hexadecimal characters
```

---

# Why Hashes Are Weak Indicators

Changing even a single bit changes the hash completely.

Example:

```text
Original File
      ↓
MD5 Hash A

Modify 1 Character
      ↓
MD5 Hash B
```

---

## Attacker Effort

Very Low

An attacker can easily:

* Recompile malware
* Add random bytes
* Change metadata
* Repackage payloads

---

## Defender Usage

Useful for:

* Malware identification
* IOC tracking
* Threat intelligence correlation

---

## Common Hash Lookup Platforms

### [VirusTotal](https://www.virustotal.com?utm_source=chatgpt.com)

Used for:

* Malware analysis
* Hash lookups
* Community intelligence

---

### [OPSWAT MetaDefender Cloud](https://metadefender.opswat.com?utm_source=chatgpt.com)

Used for:

* File reputation
* Multi-engine scanning

---

# Level 2: IP Addresses (Easy)

## What Are IP Indicators?

IP addresses identify systems communicating across networks.

Attackers use IP addresses for:

* Command and Control (C2)
* Malware hosting
* Data exfiltration
* Phishing infrastructure

---

# Detection Examples

```text
Suspicious Outbound Connections

Known Malicious IPs

Threat Intelligence Matches
```

---

# Common Defensive Actions

```text
Block IP
Drop Traffic
Firewall Rule
Blacklist
```

---

# Why IPs Are Easy To Change

Attackers can simply:

* Rent new VPS servers
* Use cloud providers
* Use compromised hosts
* Rotate infrastructure

---

# Fast Flux

## Definition

Fast Flux is a technique that rapidly changes IP addresses associated with a domain.

---

## Purpose

Hide attacker infrastructure and make blocking difficult.

---

## Fast Flux Example

```text
malicious-domain.com
        ↓

IP 1
IP 2
IP 3
IP 4
```

IPs continuously rotate.

---

# Level 3: Domain Names (Easy)

## What Is A Domain?

A human-readable name that maps to an IP address.

Example:

```text
example.com
```

---

# Why Domains Matter

Malware often communicates with:

```text
C2 Servers
Malware Hosting Sites
Phishing Websites
```

---

# Domain-Based Detection

Sources:

* DNS Logs
* Proxy Logs
* Firewall Logs
* Web Server Logs

---

# URL Shorteners

Attackers often hide malicious domains behind URL shorteners.

Examples:

```text
bit.ly
tinyurl.com
goo.gl
ow.ly
x.co
```

---

# Punycode Attacks

## Definition

A technique that abuses Unicode characters to create domains that visually resemble legitimate websites.

---

## Example

Legitimate:

```text
adidas.de
```

Malicious:

```text
adıdas.de
```

Punycode:

```text
xn--addas-o4a.de
```

---

## Purpose

Trick users into visiting malicious websites.

---

# Level 4: Host Artifacts (Annoying)

## What Are Host Artifacts?

Evidence left behind on an infected system.

---

## Examples

### Suspicious Processes

```text
powershell.exe

cmd.exe

regsvr32.exe
```

---

### Registry Modifications

Persistence mechanisms.

---

### Dropped Files

Malicious executables.

Example:

```text
payload.exe
backdoor.dll
stealer.exe
```

---

### Scheduled Tasks

Persistence activity.

---

# Detection Sources

```text
Windows Event Logs

Sysmon

EDR

Registry Monitoring

File Monitoring
```

---

# Why Host Artifacts Hurt Attackers

Changing malware behavior requires:

```text
Rewriting Code
Testing
Redeployment
```

---

# Level 5: Network Artifacts (Annoying)

## What Are Network Artifacts?

Observable network behaviors generated by malware.

---

## Examples

### User-Agent Strings

```text
Mozilla/4.0 (Custom)
```

---

### URI Patterns

```text
/update.php

/gate.php

/login.php
```

---

### HTTP Requests

```text
GET

POST
```

---

### Command & Control Traffic

```text
Beaconing
Encrypted Channels
Callback Traffic
```

---

# Detection Sources

## PCAP Analysis

Tools:

```text
Wireshark
TShark
tcpdump
```

---

## IDS/IPS

Examples:

```text
Snort
Suricata
Zeek
```

---

# Example Detection Logic

```text
Unusual User-Agent

Frequent POST Requests

Periodic Beaconing

Unknown External Connections
```

---

# Why Network Artifacts Are Valuable

Attackers must modify communication patterns and infrastructure.

This takes considerably more effort than changing IPs or hashes.

---

# Level 6: Tools (Challenging)

## What Are Tools?

Software used by attackers during operations.

---

## Examples

### Malware

```text
Emotet
TrickBot
Agent Tesla
```

---

### RATs

```text
AnyDesk
TeamViewer
AsyncRAT
```

---

### Credential Dumpers

```text
Mimikatz
LaZagne
```

---

### Password Crackers

```text
Hashcat
John The Ripper
```

---

# Detection Methods

## Antivirus Signatures

Identify known malware.

---

## YARA Rules

Pattern matching for malware detection.

---

## Detection Rules

Examples:

```text
Sigma

Splunk

Elastic

Sentinel
```

---

# Fuzzy Hashing

## Definition

Technique used to determine similarity between files rather than exact matches.

---

## Purpose

Detect malware variants.

---

## Example

### SSDeep

Compares files and calculates similarity scores.

Useful when malware has been slightly modified.

---

# Why Tool Detection Is Powerful

Attackers may need to:

```text
Build New Malware
Purchase New Tools
Modify Existing Frameworks
```

This requires significant effort and resources.

---

# Level 7: TTPs (Tough)

## What Are TTPs?

Tactics, Techniques, and Procedures.

The complete methodology an attacker uses during an intrusion.

---

# Components

## Tactics

The objective.

Example:

```text
Persistence
Privilege Escalation
Exfiltration
```

---

## Techniques

How the objective is achieved.

Example:

```text
Pass-the-Hash

PowerShell Execution

Credential Dumping
```

---

## Procedures

Specific implementation details.

Example:

```text
Using Mimikatz for Credential Dumping
```

---

# MITRE ATT&CK

The most common framework used to track attacker TTPs.

Contains:

```text
Tactics

Techniques

Sub-Techniques
```

---

# Examples of TTP Detection

## Pass-the-Hash

Monitor:

```text
Windows Authentication Events

Lateral Movement Activity
```

---

## Credential Dumping

Monitor:

```text
LSASS Access

Mimikatz Activity
```

---

## PowerShell Abuse

Monitor:

```text
Encoded Commands

Suspicious Script Execution
```

---

# Why TTP Detection Causes Maximum Pain

Attackers cannot simply:

```text
Change a Hash
Change an IP
Buy a New Domain
```

Instead they must redesign their operational methodology.

---

# SOC Analyst Perspective

## Weak Detections

```text
Hashes

IPs

Domains
```

Useful but easy to evade.

---

## Strong Detections

```text
Host Artifacts

Network Artifacts

Tools

TTPs
```

Much harder for attackers to bypass.

---

# Threat Hunting Strategy

Always ask:

```text
What behavior is occurring?

What tool is being used?

What technique is being executed?

Can I detect the TTP instead of the IOC?
```

---

# Quick Revision

## Pyramid Levels

```text
Hashes
↓
IP Addresses
↓
Domain Names
↓
Host Artifacts
↓
Network Artifacts
↓
Tools
↓
TTPs
```

---

## Easy For Attackers To Change

```text
Hashes

IPs

Domains
```

---

## Hard For Attackers To Change

```text
Host Artifacts

Network Artifacts

Tools

TTPs
```

---

## Best Detection Target

```text
TTPs
```

Because detecting attacker behavior creates the highest operational cost for the adversary.

---

## Remember

```text
IOC Detection Finds Indicators

TTP Detection Finds Attackers
```
