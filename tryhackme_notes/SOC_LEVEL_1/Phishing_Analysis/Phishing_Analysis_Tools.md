# Phishing Analysis Tools & Investigation Workflow

## Why This Matters

Phishing emails remain one of the most successful attack vectors because they target humans rather than technical vulnerabilities.

A SOC analyst must be able to:

```text
Identify Phishing Emails

Extract Indicators of Compromise (IOCs)

Analyze Attachments Safely

Investigate URLs

Determine Threat Severity

Generate Detection Rules
```

The goal is not only to identify one malicious email but also to prevent future attacks across the organization.

---

# Phishing Investigation Workflow

A typical phishing investigation follows this process:

```text
Receive Suspicious Email
            ↓
Analyze Headers
            ↓
Analyze Body Content
            ↓
Extract URLs
            ↓
Extract Attachments
            ↓
Check Reputation
            ↓
Sandbox Analysis
            ↓
Collect IOCs
            ↓
Create Detection Rules
```

---

# Information Collection Checklist

Before analysis begins, analysts collect all relevant artifacts.

---

# Email Header Artifacts

## Sender Email Address

Example:

```text
attacker@example.com
```

Helps identify:

```text
Spoofing

Look-Alike Domains

Known Malicious Senders
```

---

## Sender IP Address

Used to determine:

```text
Source Infrastructure

Geographic Location

Hosting Provider

Threat Actor Infrastructure
```

---

## Reverse DNS Lookup

Maps:

```text
IP Address
        ↓
Hostname
```

Useful for:

```text
Infrastructure Attribution

Threat Intelligence Correlation
```

---

## Subject Line

Can reveal:

```text
Urgency

Social Engineering Themes

Campaign Tracking
```

Examples:

```text
Invoice Attached

Account Suspended

Password Expiring
```

---

## Recipient Address

May appear in:

```text
To

CC

BCC
```

Helps determine:

```text
Target Scope

Campaign Size
```

---

## Reply-To Address

Frequently abused.

Example:

```text
From:
support@company.com

Reply-To:
attacker@gmail.com
```

---

## Date and Time

Important for:

```text
Timeline Creation

Campaign Correlation

Threat Hunting
```

---

# Email Body Artifacts

Analysts must collect:

---

## URLs

Including:

```text
Embedded Links

Buttons

Redirect Links

Shortened URLs
```

---

## Attachment Names

Examples:

```text
invoice.docm

payment.pdf

report.zip
```

---

## File Hashes

Prefer:

```text
SHA256
```

over:

```text
MD5
```

because it provides stronger uniqueness.

---

# Safe Analysis Principles

Never directly interact with suspicious content.

Avoid:

```text
Opening Attachments

Clicking URLs

Executing Files
```

Always analyze in isolated environments.

---

# Email Header Analysis

Headers contain the hidden technical information behind email delivery.

Think of headers as:

```text
Digital Shipping Records
```

---

# Key Questions During Header Analysis

```text
Who Sent The Email?

Where Did It Come From?

How Was It Routed?

Was It Spoofed?
```

---

# Email Header Analysis Tools

## Google Admin Toolbox Messageheader

Purpose:

```text
SMTP Header Analysis
```

Provides:

```text
Routing Information

Delivery Delays

Mail Flow Analysis
```

---

## Message Header Analyzer

Purpose:

```text
Visual Header Parsing
```

Benefits:

```text
Easy-To-Read Layout

Header Visualization

Delivery Chain Inspection
```

---

## MailHeader.org

Purpose:

```text
Structured Header Analysis
```

Provides:

```text
Sender IP

Relay Chain

DNS Information

Security Analysis
```

---

# Why Use Multiple Tools?

Different parsers highlight different information.

Example:

```text
Tool A
=
Better Header Visualization

Tool B
=
Better Relay Analysis

Tool C
=
Better Security Indicators
```

Using multiple tools improves accuracy.

---

# Email Infrastructure Components

## MUA

### Mail User Agent

Applications used to read emails.

Examples:

```text
Outlook

Thunderbird

Gmail

Yahoo Mail
```

---

## MTA

### Message Transfer Agent

Responsible for transporting email.

Examples:

```text
Postfix

Exim

Microsoft Exchange
```

---

# Email Flow Architecture

```text
User
 ↓
MUA
 ↓
SMTP
 ↓
MTA
 ↓
Internet
 ↓
Recipient MTA
 ↓
Recipient MUA
```

---

# Sender IP Investigation

After extracting sender IPs:

```text
Investigate Reputation
```

---

# IPInfo

Provides:

```text
Geolocation

ASN Information

Hosting Provider

Network Ownership
```

Useful for:

```text
Threat Attribution

Infrastructure Analysis
```

---

# URL Investigation

## URLScan

Purpose:

```text
Safe Website Analysis
```

URLScan visits websites inside a sandbox.

---

# Information Collected

```text
DNS Requests

Loaded Scripts

Cookies

DOM Content

Screenshots

Network Traffic
```

---

# SOC Benefits

Allows analysts to:

```text
Inspect Websites

Without Visiting Them Directly
```

---

# Reputation Analysis

## Cisco Talos Reputation Center

Used to evaluate:

```text
Domains

IPs

URLs
```

---

# Reputation Categories

```text
Good

Neutral

Poor

Malicious
```

---

# Email Body Analysis

The body often contains the actual attack.

Typical objectives:

```text
Credential Theft

Malware Delivery

Financial Fraud
```

---

# URL Extraction

Instead of manually searching HTML:

```text
Automate Extraction
```

---

# URL Extractor

Purpose:

```text
Extract All URLs
```

from raw email content.

---

# CyberChef URL Extraction

CyberChef can:

```text
Extract URLs

Decode Content

Analyze Encoded Data
```

Useful when URLs are hidden inside:

```text
HTML

Base64

Obfuscated Content
```

---

# URL Investigation Workflow

```text
Extract URL
      ↓
Expand Shortened Link
      ↓
Analyze Reputation
      ↓
Inspect In Sandbox
      ↓
Collect IOCs
```

---

# URL Shorteners

Attackers frequently use:

```text
bit.ly

tinyurl

t.co
```

to conceal destinations.

---

# Why Expand URLs?

Example:

```text
t.co/abc123
```

may redirect to:

```text
malicious-login-site.com
```

---

# Attachment Analysis

Attachments are common malware delivery mechanisms.

Examples:

```text
DOC

DOCM

XLSX

PDF

ZIP

RAR

EXE
```

---

# Safe Attachment Handling

```text
Save File

Calculate Hash

Check Reputation

Sandbox Analysis
```

Never execute directly.

---

# Hashing

A hash acts as a digital fingerprint.

Example:

```text
SHA256
=
CC6F1A04...
```

---

# Why Hashes Matter

Used for:

```text
Malware Identification

IOC Sharing

Threat Intelligence Matching
```

---

# File Reputation Services

## Cisco Talos File Reputation

Provides:

```text
Known Malware Status

Threat Reputation

Threat Intelligence Data
```

---

## VirusTotal

One of the most widely used malware analysis platforms.

---

# VirusTotal Capabilities

```text
Multi-Engine AV Scanning

URL Analysis

Hash Lookup

Behavioral Information
```

---

## ReversingLabs

Enterprise-grade file reputation platform.

Provides:

```text
Threat Classification

Malware Intelligence

Risk Scoring
```

---

# Malware Sandboxes

A malware sandbox executes suspicious files inside an isolated environment.

Purpose:

```text
Observe Behavior Safely
```

---

# Information Obtained

## Network Activity

```text
Domains Contacted

IPs Contacted

Download Attempts
```

---

## Persistence

```text
Registry Changes

Scheduled Tasks

Startup Entries
```

---

## Host Activity

```text
Process Creation

File Creation

Service Installation
```

---

## Indicators of Compromise

```text
Domains

IPs

Hashes

Mutexes

Registry Keys
```

---

# Any.Run

Interactive malware sandbox.

Features:

```text
Real-Time Monitoring

Live Process View

Network Inspection

Interactive Analysis
```

---

# Hybrid Analysis

Community malware analysis platform.

Provides:

```text
Behavioral Reports

Threat Classification

Indicators
```

---

# Joe Sandbox

Advanced malware analysis solution.

Features:

```text
MITRE ATT&CK Mapping

YARA Support

Sigma Support

Threat Hunting Features

Execution Graphs
```

---

# IOC Collection

Every phishing investigation should extract:

```text
Domains

URLs

IP Addresses

Hashes

File Names

Email Addresses
```

These become detection indicators.

---

# PhishTool

## What Is PhishTool?

PhishTool is a dedicated phishing analysis platform.

Combines:

```text
Email Metadata

Threat Intelligence

OSINT

Automated Analysis
```

into a single interface.

---

# Data Extracted Automatically

```text
Sender

Recipient

IP Addresses

SMTP Chain

Domains

Attachments

URLs
```

---

# URL Analysis

PhishTool automatically extracts:

```text
All URLs

Redirect Chains

Domain Intelligence
```

---

# Attachment Analysis

Automatically identifies:

```text
File Names

Hashes

Metadata
```

and can integrate with:

```text
VirusTotal
```

for reputation checking.

---

# Classification Workflow

After analysis:

```text
Tag Email
      ↓
Assign Verdict
      ↓
Add Notes
      ↓
Close Case
```

---

# Common Verdicts

```text
Spam

Phishing

Malware

Business Email Compromise

Whaling
```

---

# SOC Detection Opportunities

Collected indicators can be converted into:

---

## Email Rules

Block:

```text
Malicious Senders

Known Domains

Suspicious Subjects
```

---

## Web Filters

Block:

```text
Phishing URLs

Malicious Domains
```

---

## EDR Detection Rules

Detect:

```text
Known Hashes

Malicious Processes

Persistence Activity
```

---

## SIEM Correlation Rules

Alert when:

```text
Known IOC Appears

Malicious IP Connects

Hash Detected
```

---

# Threat Hunting Opportunities

Hunt for:

```text
Same Sender Domain

Same Subject Pattern

Same URL

Same Attachment Hash

Same Infrastructure
```

across historical logs.

---

# IOC Categories

## Network IOCs

```text
Domains

IPs

URLs
```

---

## Host IOCs

```text
Hashes

Processes

Registry Keys

Files
```

---

## Email IOCs

```text
Sender Address

Reply-To Address

Subject Line

Header Artifacts
```

---

# Investigation Workflow (SOC Perspective)

```text
User Reports Email
          ↓
Collect Header Artifacts
          ↓
Collect Body Artifacts
          ↓
Analyze URLs
          ↓
Analyze Attachments
          ↓
Sandbox Execution
          ↓
Collect IOCs
          ↓
Threat Intelligence Lookup
          ↓
Create Detections
          ↓
Close Incident
```

---

# Quick Revision

## Header Analysis Tools

```text
Google Messageheader

Message Header Analyzer

MailHeader.org
```

---

## IP Analysis

```text
IPInfo
```

---

## URL Analysis

```text
URLScan

CyberChef

URL Extractor
```

---

## File Reputation

```text
VirusTotal

Cisco Talos

ReversingLabs
```

---

## Malware Sandboxes

```text
Any.Run

Hybrid Analysis

Joe Sandbox
```

---

## Phishing Analysis Platform

```text
PhishTool
```
