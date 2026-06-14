# Network Traffic Analysis (NTA)

# What is Network Traffic Analysis?

Network Traffic Analysis (NTA) is the process of:

```text
Capturing Traffic
       ↓
Inspecting Traffic
       ↓
Analyzing Traffic
       ↓
Understanding Network Behavior
```

Its purpose is to gain visibility into:

```text
Internal Communications

External Communications

Network Performance

Security Threats

User Activity
```

NTA is NOT:

```text
Just Wireshark
```

NTA combines:

```text
Logs
+
Packet Inspection
+
Flow Statistics
+
Threat Intelligence
+
Correlation
```

to understand what is happening inside a network.

---

# Why Network Traffic Analysis Matters

Modern attacks almost always generate network traffic.

Examples:

```text
Malware Communication

Data Exfiltration

Command & Control

Lateral Movement

Credential Theft

Remote Access
```

Without network visibility:

```text
Attacker Activity
=
Invisible
```

---

# SOC Perspective

For SOC analysts, NTA helps:

```text
Detect Threats

Investigate Incidents

Validate Alerts

Establish Baselines

Find Anomalies
```

---

# Why Analyze Network Traffic?

## Performance Monitoring

Identify:

```text
Bandwidth Peaks

Congestion

Network Failures

Slow Applications
```

---

## Security Monitoring

Identify:

```text
Malware

Data Exfiltration

Beaconing

Lateral Movement

Unauthorized Connections
```

---

# Example: DNS Tunneling

Consider the following DNS requests:

```text
aj39skdm.malicious-tld.com

msd91azx.malicious-tld.com

cmd01.malicious-tld.com
```

At first glance:

```text
Normal DNS Queries
```

However:

```text
Different Subdomains

Same Domain

Repeated Requests
```

can indicate:

```text
DNS Tunneling
```

---

# What DNS Logs Reveal

DNS logs provide:

```text
Source IP

Destination IP

Queried Domain

Query Type

Timestamp
```

---

# What DNS Logs Don't Reveal

DNS logs often miss:

```text
Actual Payload

Command Data

Encoded Instructions

Exfiltrated Information
```

---

# DNS-Based Command & Control

Example:

```text
cmd1.evilc2.com TXT
```

Response:

```text
SSBsb3ZlIHlvdXIgY3VyaW91c2l0eQ==
```

This is Base64 encoded data.

Threat actors commonly use:

```text
TXT Records
```

for:

```text
Commands

Payload Delivery

Data Exfiltration
```

---

# Network Traffic Analysis Workflow

```text
Alert Generated
        ↓
Review Logs
        ↓
Identify Suspicious Host
        ↓
Capture Packets
        ↓
Inspect Content
        ↓
Confirm Threat
```

---

# Major NTA Use Cases

## Detect Suspicious Activity

Examples:

```text
Malware

Botnets

Scanning

Exfiltration
```

---

## Reconstruct Attacks

Determine:

```text
What Happened

When

How

Who Was Involved
```

---

## Validate Alerts

Determine whether:

```text
True Positive

False Positive
```

---

# What Can We Observe?

To understand traffic visibility, we use the:

```text
TCP/IP Model
```

---

# TCP/IP Layers

```text
Application
      ↓
Transport
      ↓
Internet
      ↓
Link
```

Each layer contains information useful for defenders.

---

# Application Layer

Contains:

```text
Application Headers

Application Payload
```

---

# Examples

Protocols:

```text
HTTP

HTTPS

DNS

SMTP

SMB

FTP
```

---

# HTTP Example

Request:

```text
GET /suspicious_package.zip
```

Response:

```text
200 OK
```

Logs may show:

```text
URL

Response Code

User Agent
```

---

# What Logs Miss

Logs typically do NOT contain:

```text
Downloaded File Contents
```

Only packet inspection reveals:

```text
ZIP Content

Malware

Payloads
```

---

# Why Payload Inspection Matters

Scenario:

```text
User Downloads ZIP
```

Logs show:

```text
Successful Download
```

Packet capture shows:

```text
Malware Inside ZIP
```

---

# Transport Layer

Responsible for:

```text
TCP

UDP
```

---

# Important Fields

```text
Source Port

Destination Port

Flags

Sequence Numbers

Acknowledgements
```

---

# TCP Three-Way Handshake

```text
Client → SYN

Server → SYN ACK

Client → ACK
```

Connection established.

---

# Session Hijacking Detection

Normal traffic:

```text
Seq=1
Seq=1461
Seq=2921
```

Abnormal traffic:

```text
Seq=34567232
```

Large jumps may indicate:

```text
Session Hijacking

Packet Injection

Spoofing
```

---

# SOC Detection Opportunities

Look for:

```text
Unexpected Sources

Invalid TCP Flags

Sequence Number Anomalies

Reset Storms
```

---

# Internet Layer

Responsible for:

```text
IP Routing
```

Protocols:

```text
IPv4

IPv6

ICMP
```

---

# Important Fields

```text
Source IP

Destination IP

TTL

Fragment Offset

Packet Length
```

---

# Fragmentation

Large packets are split into:

```text
Fragments
```

and reassembled later.

---

# Fragmentation Attacks

Attackers abuse fragmentation to:

```text
Evade IDS

Confuse Reassembly

Hide Payloads
```

---

# Overlapping Fragments

Example:

```text
Fragment 1 Offset=0

Fragment 2 Offset=1480

Fragment 3 Offset=1480
```

Fragment 3 overlaps Fragment 2.

This may indicate:

```text
Fragmentation Evasion Attack
```

---

# SOC Detection Opportunities

Look for:

```text
Tiny Fragments

Overlapping Fragments

Abnormal Fragment Counts
```

---

# Link Layer

Responsible for:

```text
Local Network Communication
```

---

# Common Protocols

```text
Ethernet

ARP

STP
```

---

# Important Fields

```text
Source MAC

Destination MAC
```

---

# ARP Poisoning

Attackers can poison ARP tables by claiming:

```text
I Own This IP Address
```

even when they don't.

---

# Example

Host:

```text
192.168.1.200
```

responds to every ARP request using the same MAC.

Result:

```text
Traffic Redirection
```

---

# MITM Through ARP Poisoning

```text
Victim
   ↓
Attacker
   ↓
Gateway
```

Allows:

```text
Sniffing

Credential Theft

Traffic Manipulation
```

---

# Traffic Sources

Network traffic originates from:

```text
Intermediary Devices

Endpoint Devices
```

---

# Intermediary Sources

Traffic passes through these devices.

Examples:

```text
Firewalls

Routers

Switches

Web Proxies

IDS

IPS

Access Points
```

---

# Common Infrastructure Protocols

```text
OSPF

BGP

EIGRP

SNMP

DHCP

ARP

SYSLOG
```

---

# Endpoint Sources

Endpoints generate most network traffic.

Examples:

```text
Workstations

Servers

IoT Devices

Printers

Mobile Devices

Cloud Instances
```

---

# Traffic Flows

Network traffic generally falls into:

```text
North-South

East-West
```

---

# North-South Traffic

Traffic entering or leaving the network.

```text
LAN
 ↓
Firewall
 ↓
Internet
```

---

# Examples

```text
HTTPS

DNS

VPN

SSH

SMTP

RDP
```

---

# Why North-South Matters

Often contains:

```text
Malware Downloads

C2 Traffic

Data Exfiltration
```

---

# East-West Traffic

Traffic inside the organization.

```text
Host ↔ Host

Server ↔ Server
```

---

# Examples

```text
SMB

Kerberos

LDAP

AD Replication

Database Traffic
```

---

# Why East-West Matters

Attackers use it for:

```text
Lateral Movement

Privilege Escalation

Internal Reconnaissance
```

---

# Common East-West Services

## Identity Services

```text
Kerberos

LDAP

Active Directory
```

---

## File Services

```text
SMB

NFS

Print Services
```

---

## Infrastructure Services

```text
DNS

DHCP

Routing Protocols
```

---

# Important Network Flows

## HTTPS

Modern enterprises often use:

```text
TLS Inspection
```

---

# HTTPS Inspection Flow

```text
Client
   ↓
Proxy
   ↓
Web Server
```

Proxy decrypts and inspects traffic.

---

# Benefits

Detect:

```text
Malware Downloads

Phishing Pages

Data Exfiltration
```

---

# DNS Flow

```text
Host
  ↓
Internal DNS
  ↓
Firewall
  ↓
External DNS
```

---

# Why Monitor DNS?

Detect:

```text
DNS Tunneling

Beaconing

Malicious Domains
```

---

# SMB + Kerberos Flow

User accesses:

```text
\\FILESERVER\SHARE
```

Authentication:

```text
Kerberos
```

Access:

```text
SMB Session
```

---

# Why Monitor SMB?

Detect:

```text
Lateral Movement

Credential Theft

Unauthorized Access
```

---

# How Can We Observe Traffic?

Three primary sources:

```text
Logs

Packet Capture

Flow Statistics
```

---

# Logs

Logs provide:

```text
Events

Connections

Authentication

Requests
```

---

# Examples

## Linux Auth Log

```text
Accepted password for user
```

---

## Apache Log

```text
GET /index.html
```

---

# Advantages

```text
Low Storage

Easy Search

Long Retention
```

---

# Limitations

Usually lack:

```text
Payload Data

Packet Context

Full Headers
```

---

# Full Packet Capture (PCAP)

Provides:

```text
Entire Packet
```

including:

```text
Headers

Payload

Timing

Protocol Details
```

---

# Methods of Packet Capture

## Network TAP

Physical hardware device.

---

# Network TAP Characteristics

```text
Inline Device

Copies Traffic

No Delay

Link Layer Operation
```

---

# Advantages

```text
Near Zero Impact

Reliable

Accurate
```

---

# Port Mirroring (SPAN)

Switch duplicates traffic.

Example:

```text
Source Port
      ↓
Mirror Port
```

---

# Advantages

```text
No Additional Hardware
```

---

# Disadvantages

```text
May Affect Performance

Can Drop Packets Under Load
```

---

# Packet Capture Best Practices

## Placement

Capture where visibility is highest.

---

## Duration

Storage requirements grow rapidly.

Example:

```text
1 Gbps

≈ 10.8 TB/day
```

---

## TAP vs SPAN

```text
TAP
=
Performance

SPAN
=
Convenience
```

---

# NTA Tools

## Wireshark

Most popular packet analysis tool.

---

## TCPdump

Command-line packet capture.

---

## Snort

Signature-based IDS.

---

## Suricata

High-performance IDS/IPS.

---

## Zeek

Network Security Monitoring platform.

---

# Network Statistics

Instead of packets, collect:

```text
Metadata
```

about traffic.

---

# Why Statistics Matter

Detect:

```text
Beaconing

Exfiltration

Scanning

Lateral Movement
```

without storing full packets.

---

# NetFlow

Developed by Cisco.

Collects:

```text
Source IP

Destination IP

Ports

Bytes

Packets

Duration
```

---

# NetFlow Advantages

Small storage footprint.

Good for:

```text
Behavior Analytics

Traffic Trending

Threat Hunting
```

---

# IPFIX

Successor to NetFlow.

Advantages:

```text
Vendor Neutral

Flexible

Custom Fields
```

---

# NetFlow vs PCAP

## NetFlow

Shows:

```text
Who Talked To Who
```

---

## PCAP

Shows:

```text
Exactly What Was Said
```

---

# SOC Investigation Workflow

```text
Alert
   ↓
Check Logs
   ↓
Review NetFlow
   ↓
Capture Packets
   ↓
Analyze Protocols
   ↓
Identify Threat
   ↓
Respond
```

---

# Detection Opportunities

## DNS

```text
Tunneling

Beaconing

Malicious Domains
```

---

## HTTP/HTTPS

```text
Malware Downloads

Phishing

Suspicious User Agents
```

---

## SMB

```text
Lateral Movement

Unauthorized Access
```

---

## TCP

```text
Session Hijacking

Packet Injection
```

---

## ARP

```text
Spoofing

MITM Attacks
```

---

# Quick Revision

## NTA

```text
Capture + Inspect + Analyze
```

---

## North-South

```text
LAN ↔ Internet
```

---

## East-West

```text
Internal Traffic
```

---

## Logs

```text
Summary Information
```

---

## PCAP

```text
Complete Visibility
```

---

## TAP

```text
Hardware Packet Copy
```

---

## SPAN

```text
Switch-Based Packet Copy
```

---

## NetFlow

```text
Traffic Metadata
```

---

## IPFIX

```text
Enhanced NetFlow
```

---

# Final Takeaway

```text
Logs Tell You

Something Happened

NetFlow Tells You

Who Talked To Who

Packet Capture Tells You

Exactly What Happened
```

Effective Network Traffic Analysis combines all three to detect threats, investigate incidents, understand attacker behavior, and provide complete visibility into modern networks.
