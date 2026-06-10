# Email Security & Phishing Prevention

## Why Email Security Matters

Email remains one of the most abused communication channels in cybersecurity.

Attackers use email to:

```text
Deliver Malware

Steal Credentials

Conduct Fraud

Launch Phishing Campaigns

Gain Initial Access
```

Because of this, organizations deploy multiple layers of protection to verify sender legitimacy and prevent spoofing.

---

# Email Security Architecture

Modern email security relies on several technologies working together:

```text
SPF
 ↓
DKIM
 ↓
DMARC
 ↓
S/MIME
 ↓
Email Filtering
 ↓
Sandboxing
```

Each technology solves a different problem.

---

# Core Email Security Controls

## SPF

### Sender Policy Framework

Purpose:

```text
Verify Who Is Allowed To Send Email
```

SPF checks whether the sending server is authorized to send emails on behalf of a domain.

---

# SPF Question

SPF answers:

```text
Is This Mail Server Allowed
To Send Email For This Domain?
```

---

# How SPF Works

```text
Email Arrives
       ↓
Extract Sender Domain
       ↓
Query DNS SPF Record
       ↓
Check Sending IP
       ↓
Return Result
```

---

# SPF Record Example

```text
v=spf1 ip4:127.0.0.1 include:_spf.google.com -all
```

---

# SPF Components

## v=spf1

```text
SPF Version Identifier
```

---

## ip4:127.0.0.1

```text
Authorized IPv4 Address
```

---

## include:_spf.google.com

```text
Trust Google's Mail Servers
```

---

## -all

```text
Reject All Unauthorized Senders
```

This is the strongest SPF enforcement option.

---

# SPF Include Mechanism

Organizations often use cloud providers.

Example:

```text
Google Workspace

Microsoft 365

HubSpot

Chargebee
```

Instead of listing every IP address, SPF can reference another SPF record.

Example:

```text
include:_spf.google.com
```

---

# SPF Verification Results

## Pass

```text
Sender Authorized
```

---

## Neutral

```text
No Strong Decision
```

---

## None

```text
No SPF Record Found
```

---

## SoftFail

```text
Suspicious Sender
```

Email is accepted but flagged.

---

## Fail

```text
Unauthorized Sender
```

Email rejected.

---

## TempError

```text
Temporary DNS Issue
```

---

## PermError

```text
Permanent SPF Configuration Error
```

---

# Why SOC Analysts Care About SoftFail

SoftFail often appears in:

```text
Phishing Emails

Spoofing Attempts

Misconfigured Mail Systems
```

---

# SPF Investigation Workflow

```text
Extract Domain
      ↓
Retrieve SPF Record
      ↓
Check Authorized Servers
      ↓
Compare Sender IP
      ↓
Review SPF Result
```

---

# SPF Analysis Tools

## Dmarcian SPF Surveyor

Used for:

```text
SPF Validation

Syntax Checking

Visualization
```

---

## Google Messageheader Analyzer

Provides:

```text
SPF Results

Mail Routing

Header Analysis
```

---

# SPF Limitations

SPF validates:

```text
Where Mail Came From
```

but not:

```text
Message Integrity

Content Authenticity
```

This is why DKIM exists.

---

# DKIM

## DomainKeys Identified Mail

Purpose:

```text
Verify Message Integrity
```

---

# DKIM Question

DKIM answers:

```text
Was This Email Modified?

Did It Really Come From This Domain?
```

---

# How DKIM Works

Uses:

```text
Public Key Cryptography
```

---

# DKIM Workflow

```text
Sender Creates Signature
          ↓
Attach Signature To Email
          ↓
Recipient Retrieves Public Key
          ↓
Verify Signature
          ↓
Accept Or Reject
```

---

# DKIM Components

## Private Key

Stored securely on sender's mail server.

Used to:

```text
Sign Email
```

---

## Public Key

Stored in DNS.

Used to:

```text
Verify Signature
```

---

# DKIM Record Example

```text
v=DKIM1; k=rsa; p=<public_key>
```

---

# DKIM Record Components

## v=DKIM1

```text
DKIM Version
```

---

## k=rsa

```text
Cryptographic Algorithm
```

---

## p=

```text
Public Verification Key
```

---

# Why DKIM Survives Forwarding

SPF validates:

```text
Sending Server
```

DKIM validates:

```text
Email Content
```

Therefore:

```text
Forwarding Does Not Break DKIM
```

if content remains unchanged.

---

# DKIM Verification Results

## Pass

```text
Message Verified
```

---

## Fail

```text
Signature Invalid
```

---

## PermError

```text
Permanent Verification Failure
```

Common causes:

```text
Missing Public Key

Broken Signature

DNS Misconfiguration
```

---

# SOC Perspective

DKIM failures may indicate:

```text
Spoofing

Header Manipulation

Infrastructure Issues
```

---

# DKIM Analysis Tools

## Dmarcian DKIM Checker

Used for:

```text
DNS Validation

Key Verification
```

---

## Email Header Analyzers

Used to inspect:

```text
DKIM Pass

DKIM Fail

DKIM PermError
```

---

# DMARC

## Domain-Based Message Authentication, Reporting & Conformance

Purpose:

```text
Enforce Email Authentication Policies
```

---

# DMARC Question

DMARC answers:

```text
Can This Domain Be Trusted?
```

---

# Why DMARC Exists

SPF and DKIM individually:

```text
Authenticate Email
```

DMARC:

```text
Enforces Policy
```

---

# DMARC Workflow

```text
Check SPF
      ↓
Check DKIM
      ↓
Verify Alignment
      ↓
Apply Policy
```

---

# Domain Alignment

DMARC requires:

```text
From Domain
=
Authenticated Domain
```

---

# SPF Alignment

Checks:

```text
Authorized Server

Matching Domain
```

---

# DKIM Alignment

Checks:

```text
Signature Domain

From Domain
```

---

# DMARC Success

Requires:

```text
SPF Pass + Alignment

OR

DKIM Pass + Alignment
```

---

# DMARC Record Example

```text
v=DMARC1; p=quarantine; rua=mailto:postmaster@example.com
```

---

# DMARC Components

## v=DMARC1

```text
DMARC Version
```

---

## p=

Defines policy.

---

## rua=

Aggregate report destination.

---

# DMARC Policies

## p=none

```text
Monitor Only
```

---

## p=quarantine

```text
Move To Spam
```

---

## p=reject

```text
Reject Email Completely
```

Strongest protection.

---

# DMARC Maturity Model

```text
none
  ↓
quarantine
  ↓
reject
```

Organizations usually progress through these stages.

---

# Why DMARC Matters

Provides:

```text
Spoofing Protection

Visibility

Policy Enforcement

Brand Protection
```

---

# SPF, DKIM & DMARC Relationship

```text
SPF
=
Where Mail Came From

DKIM
=
What Was Sent

DMARC
=
What To Do If Checks Fail
```

---

# S/MIME

## Secure Multipurpose Internet Mail Extensions

Purpose:

```text
Protect Email Content
```

Unlike SPF, DKIM, and DMARC:

```text
Protects Individual Users
```

not domains.

---

# Security Goals

## Authentication

Verify sender identity.

---

## Confidentiality

Protect message contents.

---

## Integrity

Detect modification.

---

## Non-Repudiation

Prevent sender denial.

---

# S/MIME Components

## Digital Signatures

Provides:

```text
Authentication

Integrity

Non-Repudiation
```

---

## Encryption

Provides:

```text
Confidentiality

Integrity
```

---

# S/MIME Workflow

```text
User Obtains Certificate
          ↓
Signs Email
          ↓
Recipient Verifies Signature
          ↓
Encrypted Messages Decrypted
Using Private Key
```

---

# Certificates

Issued by:

```text
Certificate Authorities (CAs)
```

Contain:

```text
Public Key

Identity Information
```

---

# Why S/MIME Matters

Used heavily in:

```text
Government

Legal Communications

Enterprise Security
```

---

# S/MIME vs SPF/DKIM/DMARC

| Technology | Protects        |
| ---------- | --------------- |
| SPF        | Domain          |
| DKIM       | Domain          |
| DMARC      | Domain          |
| S/MIME     | Individual User |

---

# SMTP Analysis

## SMTP

### Simple Mail Transfer Protocol

Responsible for:

```text
Sending Email
```

---

# Why SOC Analysts Analyze SMTP

To investigate:

```text
Delivery Failures

Spam Activity

Mail Flow

Phishing Campaigns
```

---

# SMTP Response Codes

SMTP servers return status codes.

Similar to:

```text
HTTP Status Codes
```

---

# Common SMTP Response Codes

## 220

```text
Service Ready
```

Mail server available.

---

## 250

```text
Request Successful
```

---

## 354

```text
Start Mail Input
```

---

## 421

```text
Service Not Available
```

---

## 550

```text
Mailbox Unavailable
```

---

## 552

```text
Security Or Storage Issue
```

Often used for suspicious content.

---

## 553

```text
Mailbox Name Not Allowed
```

May indicate anti-spam blocking.

---

# SMTP Analysis Using Wireshark

Useful display filter:

```text
smtp.response.code
```

---

# Example Filter

```text
smtp.response.code eq 220
```

Shows:

```text
Service Ready Responses
```

---

# SMTP Investigation Workflow

```text
Capture Traffic
      ↓
Filter SMTP
      ↓
Review Responses
      ↓
Identify Errors
      ↓
Investigate Cause
```

---

# IMF

## Internet Message Format

Defines email structure.

Contains:

```text
From

To

Date

Subject

Content-Type

Attachments
```

---

# Attachment Investigation

Important fields:

## Filename

Example:

```text
document.zip
```

---

## Content-Type

Example:

```text
application/zip
```

---

## Content-Transfer-Encoding

Example:

```text
base64
```

---

# Base64 Encoding

Common method for transporting attachments.

Example:

```text
Encoded Data
       ↓
Decode
       ↓
Original File
```

---

# Phishing Prevention Technologies

Authentication alone is insufficient.

Organizations deploy additional controls.

---

# Email Filtering

Blocks:

```text
Known Spam

Known Phishing

Malicious Domains
```

---

# Secure Email Gateways (SEGs)

Detect:

```text
Spoofing

Impersonation

Advanced Phishing
```

---

# Link Rewriting

Transforms:

```text
Original URL
      ↓
Protected Redirect
```

Allows inspection at click time.

---

# Sandboxing

Safely executes:

```text
Attachments

URLs

Documents
```

inside isolated environments.

---

# Why Sandboxing Works

Allows defenders to observe:

```text
Processes

Network Traffic

Persistence

File Creation
```

without risking production systems.

---

# User-Focused Security Controls

Technology alone is insufficient.

Users remain a major target.

---

# Warning Banners

Examples:

```text
External Sender

Suspicious Message

Unverified Sender
```

---

# Phishing Reporting

Allows users to:

```text
Report Suspicious Emails
```

directly to security teams.

---

# Security Awareness Training

Teaches users:

```text
Phishing Indicators

Safe Behavior

Reporting Procedures
```

---

# Phishing Simulations

Organizations run controlled phishing campaigns to:

```text
Measure Awareness

Improve Detection

Reinforce Training
```

---

# SOC Investigation Workflow

```text
Email Alert
      ↓
SPF Analysis
      ↓
DKIM Analysis
      ↓
DMARC Verification
      ↓
SMTP Review
      ↓
Attachment Analysis
      ↓
IOC Collection
      ↓
Detection Rule Creation
```

---

# Quick Revision

## SPF

```text
Verifies Sending Server
```

---

## DKIM

```text
Verifies Message Integrity
```

---

## DMARC

```text
Enforces Authentication Policy
```

---

## S/MIME

```text
Protects Message Content
```

---

## SMTP

```text
Transfers Email
```

---

## IMF

```text
Defines Email Structure
```

---

## Sandboxing

```text
Safely Executes Suspicious Files
```

---

# Final Takeaway

```text
SPF
      +
DKIM
      +
DMARC
      +
S/MIME
      +
Email Filtering
      +
Sandboxing
      +
User Awareness

=
Modern Email Security
```
