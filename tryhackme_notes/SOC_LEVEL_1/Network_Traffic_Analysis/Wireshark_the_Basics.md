# Wireshark: The Basics

# What is Wireshark?

Wireshark is an open-source network protocol analyzer used to:

```text
Capture Packets
       ↓
Inspect Traffic
       ↓
Analyze Protocols
       ↓
Investigate Network Activity
```

It is one of the most widely used tools in:

```text
SOC Operations

Incident Response

Threat Hunting

Network Troubleshooting

Malware Analysis

Digital Forensics
```

---

# Why Wireshark Matters

Most security incidents leave traces in network traffic.

Wireshark allows analysts to inspect:

```text
Who Communicated

What Was Transferred

Which Protocol Was Used

When It Happened

How The Communication Occurred
```

---

# SOC Perspective

Wireshark is commonly used to:

```text
Validate Alerts

Investigate Suspicious Hosts

Analyze Malware Traffic

Recover Files

Detect Data Exfiltration

Identify C2 Communication
```

---

# Wireshark vs IDS

Wireshark is NOT:

```text
An Intrusion Detection System
```

Wireshark:

```text
Captures Traffic

Displays Traffic

Analyzes Traffic
```

Analyst:

```text
Identifies Threats
```

Detection depends on analyst knowledge.

---

# Core Workflow

```text
Capture Traffic
       ↓
Apply Filters
       ↓
Inspect Packets
       ↓
Follow Streams
       ↓
Extract Evidence
       ↓
Investigate Threat
```

---

# Wireshark Interface Overview

The interface consists of five major sections.

---

# Toolbar

Contains shortcuts for:

```text
Open Files

Save Files

Export Data

Filtering

Navigation
```

---

# Display Filter Bar

Used to filter captured traffic.

Examples:

```text
http

dns

tcp

udp

ip.addr == 10.10.10.10
```

---

# Recent Files

Provides quick access to:

```text
Previously Opened PCAP Files
```

---

# Capture Interfaces

Used to select:

```text
Ethernet

Wi-Fi

Virtual Interfaces

VPN Interfaces
```

for packet capture.

---

# Status Bar

Displays:

```text
Packet Count

Capture Status

Applied Filters

Displayed Packets
```

---

# PCAP Files

Wireshark primarily works with:

```text
PCAP

PCAPNG
```

files.

These files contain captured network traffic.

---

# Opening Capture Files

Methods:

```text
File → Open

Drag & Drop

Double Click
```

---

# Packet Analysis Panes

Wireshark divides packet analysis into three panes.

---

# Packet List Pane

Provides packet summary:

```text
Packet Number

Timestamp

Source

Destination

Protocol

Info
```

---

# Packet Details Pane

Shows protocol breakdown.

Example:

```text
Ethernet

IP

TCP

HTTP
```

---

# Packet Bytes Pane

Displays:

```text
Hexadecimal Data

ASCII Data
```

Useful during:

```text
Forensics

Payload Analysis

Malware Investigation
```

---

# Packet Colouring

Wireshark automatically colorizes traffic.

Purpose:

```text
Quick Visual Identification
```

Examples:

```text
TCP

HTTP

DNS

Errors

Warnings
```

---

# Custom Colouring Rules

Analysts can create:

```text
Temporary Rules

Permanent Rules
```

to highlight suspicious traffic.

---

# Traffic Capture Controls

## Start Capture

```text
Blue Shark Fin
```

---

## Stop Capture

```text
Red Square
```

---

## Restart Capture

```text
Green Arrow
```

---

# Merging Capture Files

Wireshark can merge multiple PCAPs.

Useful when:

```text
Traffic Is Captured

From Multiple Sources
```

or

```text
Traffic Is Split Across Files
```

---

# Capture File Properties

Provides:

```text
File Hashes

Comments

Interfaces

Statistics

Timestamps
```

---

# Why File Properties Matter

Useful for:

```text
Evidence Validation

Chain Of Custody

Integrity Verification

Case Documentation
```

---

# Packet Dissection

Packet dissection is the process of decoding protocols and displaying packet contents in human-readable form.

---

# Packet Structure

Typical packet layers:

```text
Frame
 ↓
Ethernet
 ↓
IP
 ↓
TCP/UDP
 ↓
Application Protocol
 ↓
Application Data
```

---

# Layer 1 — Frame

Contains:

```text
Arrival Time

Frame Length

Capture Metadata
```

---

# SOC Relevance

Used for:

```text
Timeline Analysis

Traffic Correlation
```

---

# Layer 2 — Ethernet

Contains:

```text
Source MAC

Destination MAC
```

---

# SOC Relevance

Detect:

```text
ARP Spoofing

Rogue Devices

Layer 2 Attacks
```

---

# Layer 3 — IP

Contains:

```text
Source IP

Destination IP

TTL

Fragment Information
```

---

# TTL Analysis

TTL helps identify:

```text
Routing Paths

Packet Manipulation

Potential Spoofing
```

---

# Layer 4 — TCP / UDP

Contains:

```text
Ports

Flags

Sequence Numbers

Window Size
```

---

# SOC Relevance

Detect:

```text
Scanning

Session Hijacking

Packet Injection

Protocol Abuse
```

---

# Layer 5+ — Application Protocols

Examples:

```text
HTTP

HTTPS

DNS

FTP

SMTP

SMB
```

---

# HTTP Analysis

HTTP packets reveal:

```text
Methods

Headers

Cookies

URLs

Files
```

---

# Common HTTP Methods

```text
GET

POST

PUT

DELETE

HEAD
```

---

# Example

```text
GET /malware.zip
```

indicates file retrieval.

---

# HTTP Response Codes

## 200

```text
Success
```

---

## 301 / 302

```text
Redirect
```

---

## 403

```text
Forbidden
```

---

## 404

```text
Not Found
```

---

## 500

```text
Server Error
```

---

# ETag Analysis

ETag:

```text
Entity Tag
```

Used by web servers to identify resource versions.

---

# SOC Relevance

Useful when:

```text
Tracking File Changes

Verifying Cached Content

Investigating Web Activity
```

---

# Packet Navigation

Large captures may contain:

```text
Thousands

Millions

Of Packets
```

Navigation becomes critical.

---

# Packet Numbers

Every packet receives:

```text
Unique Packet ID
```

Example:

```text
Packet 38

Packet 33790
```

---

# Go To Packet

Allows direct navigation:

```text
Go → Go To Packet
```

---

# Find Packet

Search methods:

```text
String Search

Hex Search

Regular Expressions

Display Filters
```

---

# SOC Use Cases

Search for:

```text
Passwords

Usernames

Domains

Malware Strings

Suspicious Commands
```

---

# Marking Packets

Packets can be marked for investigation.

Useful during:

```text
Incident Response

Threat Hunting

Evidence Collection
```

---

# Packet Comments

Unlike packet marks:

```text
Comments Persist
```

inside capture files.

Useful for:

```text
Team Collaboration

Case Notes

Documentation
```

---

# Exporting Packets

Export only selected packets.

Benefits:

```text
Reduced Dataset

Focused Analysis

Evidence Sharing
```

---

# Export Objects

Wireshark can recover files transferred through protocols.

Examples:

```text
HTTP

SMB

DICOM

TFTP
```

---

# File Extraction Use Cases

Recover:

```text
Malware Samples

Documents

Images

Archives

Payloads
```

---

# Stream Reconstruction

One of Wireshark's most powerful features.

---

# Follow Stream

Supported protocols:

```text
TCP

UDP

HTTP

TLS

HTTP2
```

---

# Purpose

Rebuild entire conversations.

---

# Stream Workflow

```text
Individual Packets
        ↓
Reassembly
        ↓
Complete Conversation
```

---

# Example

Instead of viewing:

```text
Packet 1

Packet 2

Packet 3

Packet 4
```

you see:

```text
Entire HTTP Session
```

---

# Threat Hunting Benefits

Reveal:

```text
Credentials

Commands

URLs

Files

Malware Activity
```

---

# Filtering Fundamentals

Without filtering, analysis becomes difficult.

---

# Capture Filters

Applied BEFORE capture.

Benefits:

```text
Reduce Storage

Reduce Noise
```

---

# Example

```text
port 80

host 10.10.10.10
```

---

# Display Filters

Applied AFTER capture.

Most commonly used.

---

# Example Filters

## HTTP

```text
http
```

---

## DNS

```text
dns
```

---

## TCP

```text
tcp
```

---

## UDP

```text
udp
```

---

## Specific IP

```text
ip.addr == 192.168.1.10
```

---

## Specific Port

```text
tcp.port == 443
```

---

# Apply As Filter

Quickly create filters directly from fields.

Example:

```text
Right Click → Apply As Filter
```

---

# Conversation Filter

Displays all packets belonging to:

```text
Specific Host

Specific Session
```

---

# Colourise Conversation

Highlights traffic without filtering.

Useful for:

```text
Tracking Sessions

Visual Correlation
```

---

# Prepare As Filter

Creates filter without immediately applying it.

Useful for:

```text
Complex Queries
```

---

# Apply As Column

Adds important fields as columns.

Examples:

```text
TTL

Hostnames

TCP Window Size

User Agent
```

---

# Expert Information

Wireshark automatically identifies anomalies.

Severity levels:

```text
Chat

Note

Warning

Error
```

---

# Expert Info Use Cases

Detect:

```text
Malformed Packets

Retransmissions

TCP Issues

Protocol Errors
```

---

# Important Warning

Expert Info is not perfect.

It may produce:

```text
False Positives

False Negatives
```

Always validate findings manually.

---

# SOC Investigation Workflow

```text
Receive Alert
        ↓
Open PCAP
        ↓
Review Statistics
        ↓
Apply Filters
        ↓
Locate Suspicious Packets
        ↓
Follow Streams
        ↓
Extract Evidence
        ↓
Confirm Threat
```

---

# Common Threat Hunting Activities

## HTTP Investigation

Look for:

```text
Suspicious Downloads

Unknown Domains

Encoded Data
```

---

## DNS Investigation

Look for:

```text
DNS Tunneling

Beaconing

DGA Domains
```

---

## SMB Investigation

Look for:

```text
Lateral Movement

File Transfers

Credential Abuse
```

---

## TCP Analysis

Look for:

```text
Scanning

Reset Storms

Session Anomalies
```

---

# Detection Opportunities

## File Downloads

```text
HTTP GET

ZIP

EXE

DLL
```

---

## Malware Delivery

```text
Payload Downloads

Exploit Kits
```

---

## Data Exfiltration

```text
Large Transfers

Repeated Connections

Encoded Data
```

---

## Command & Control

```text
Periodic Connections

DNS Tunneling

HTTP Beacons
```

---

# Quick Revision

## Wireshark

```text
Packet Analysis Tool
```

---

## PCAP

```text
Captured Network Traffic
```

---

## Packet List

```text
Traffic Summary
```

---

## Packet Details

```text
Protocol Breakdown
```

---

## Packet Bytes

```text
Raw Data
```

---

## Follow Stream

```text
Reconstruct Conversations
```

---

## Display Filter

```text
Show Specific Traffic
```

---

## Export Objects

```text
Recover Files
```

---

## Expert Info

```text
Protocol Warnings
```

---

# Final Takeaway

```text
Logs Tell You

Something Happened

Wireshark Shows You

Exactly What Happened
```

For SOC analysts, Wireshark is one of the most important tools for packet analysis, threat hunting, malware investigations, incident response, protocol analysis, and network forensics. Mastering filters, stream reconstruction, packet dissection, and file extraction forms the foundation of effective network traffic analysis.
