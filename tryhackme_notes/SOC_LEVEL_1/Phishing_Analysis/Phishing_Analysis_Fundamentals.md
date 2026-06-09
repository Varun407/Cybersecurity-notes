# Phishing Analysis Fundamentals

## Why Phishing Analysis Matters

Email is one of the most common attack vectors used by adversaries.

Attackers use emails to:

```text
Steal Credentials

Deliver Malware

Gain Initial Access

Conduct Fraud

Deploy Ransomware
```

A single successful phishing email can result in:

```text
Data Breach

Account Compromise

Malware Infection

Financial Loss
```

---

# Email Fundamentals

## What is Email?

Email (Electronic Mail) is a system for sending and receiving digital messages across networks.

An email consists of:

```text
Email Address
       ↓
Email Headers
       ↓
Email Body
       ↓
Attachments
```

---

# Anatomy of an Email Address

Example:

```text
david@tryhackme.com
```

---

## Username

```text
david
```

Identifies the recipient's mailbox.

---

## @ Symbol

Separates:

```text
Username
      from
Domain
```

---

## Domain

```text
tryhackme.com
```

Specifies the mail server responsible for handling messages.

---

# Real-World Analogy

Think of an email address as a postal address:

```text
Domain
=
Street / Apartment Building

Username
=
Specific Mailbox
```

---

# Email Delivery Process

Several protocols work together to deliver emails.

---

# SMTP

## Simple Mail Transfer Protocol

Purpose:

```text
Send Emails
```

SMTP is responsible for:

```text
Client → Mail Server

Mail Server → Mail Server
```

communication.

---

# POP3

## Post Office Protocol Version 3

Purpose:

```text
Download Emails
```

---

# Characteristics

```text
Single Device Access

Downloads Messages

Often Deletes Server Copies

Local Storage
```

---

# IMAP

## Internet Message Access Protocol

Purpose:

```text
Synchronize Emails
```

---

# Characteristics

```text
Multiple Devices

Server Storage

Synchronization

Centralized Mailbox
```

---

# POP3 vs IMAP

| Feature              | POP3          | IMAP        |
| -------------------- | ------------- | ----------- |
| Storage              | Local Device  | Mail Server |
| Multi-Device Support | No            | Yes         |
| Sync                 | No            | Yes         |
| Server Copies        | Often Removed | Kept        |

---

# Email Delivery Workflow

```text
User Sends Email
        ↓
SMTP Server
        ↓
DNS Lookup
        ↓
Recipient Mail Server
        ↓
POP3 / IMAP
        ↓
Recipient Inbox
```

---

# DNS in Email Delivery

Before delivery:

```text
Sender Mail Server
        ↓
Queries DNS
        ↓
Finds Recipient Mail Server
        ↓
Delivers Message
```

DNS tells the sending server where to send the email.

---

# Email Structure

Every email contains:

```text
Headers
+
Body
```

---

# Email Headers

Headers contain metadata.

Think of headers as:

```text
Envelope Information
```

---

# Common Email Header Fields

## From

Sender address.

Example:

```text
sender@example.com
```

---

## To

Recipient address.

Example:

```text
user@example.com
```

---

## Reply-To

Address where replies will be sent.

May differ from:

```text
From Address
```

and is frequently abused by attackers.

---

## Subject

Email topic.

Example:

```text
Invoice Attached
```

---

## Date

Time email was sent.

---

# Why Headers Matter

Headers reveal:

```text
Real Sender

Mail Servers

IP Addresses

Routing Information

Spoofing Attempts
```

---

# Message Source

Most email clients allow viewing:

```text
Raw Email Source
```

---

# Benefits

Provides:

```text
Complete Headers

Originating IP

MIME Information

Body Content

Attachments
```

---

# SOC Investigation Workflow

When analyzing a suspicious email:

```text
Inspect Headers
        ↓
Inspect Sender
        ↓
Inspect Links
        ↓
Inspect Attachments
        ↓
Determine Intent
```

---

# Important Header Analysis Targets

## From Address

Check for:

```text
Misspelled Domains

Look-Alike Domains

Unexpected Senders
```

Example:

```text
microsoft.com
```

vs

```text
microsof.com
```

---

## Reply-To Address

Common phishing tactic:

```text
From:
support@company.com

Reply-To:
attacker@gmail.com
```

---

## Originating IP Address

Can reveal:

```text
Actual Source

Hosting Provider

Country

Threat Infrastructure
```

---

# Email Body

The body contains:

```text
Message Content
```

---

# Two Types

## Plain Text

Only text.

Example:

```text
Hello User,
Please review attached file.
```

---

## HTML Email

Supports:

```text
Images

Colors

Links

Buttons

Formatting
```

Most phishing emails use HTML.

---

# Why HTML Emails Matter

HTML can hide malicious content.

Example:

```html
<a href="http://evil.com">
Microsoft Login
</a>
```

Visible text:

```text
Microsoft Login
```

Actual destination:

```text
evil.com
```

---

# Viewing Email Source

Viewing source reveals:

```text
Raw HTML

Embedded URLs

Tracking Pixels

Hidden Content
```

---

# Common HTML Indicators

Look for:

```text
External Images

Obfuscated Links

JavaScript References

Fake Login Buttons
```

---

# Email Attachments

Emails frequently contain:

```text
PDFs

Word Documents

Excel Files

ZIP Archives

Executables
```

---

# MIME Attachments

Attachments are stored using MIME encoding.

Important fields include:

---

## Content-Type

Specifies file type.

Example:

```text
application/pdf
```

---

## Content-Disposition

Specifies:

```text
Attachment

Filename
```

Example:

```text
invoice.pdf
```

---

## Content-Transfer-Encoding

Common value:

```text
base64
```

---

# Base64 Encoding

Attachments are commonly encoded before transmission.

Example:

```text
JVBERi0xLjQK...
```

Can be decoded using:

```text
CyberChef

Base64 Decoders
```

to reconstruct the original file.

---

# Phishing Fundamentals

## What is Phishing?

Phishing is a social engineering attack designed to trick users into:

```text
Revealing Credentials

Installing Malware

Sending Money

Providing Sensitive Data
```

---

# Types of Phishing

## Spam

Unsolicited bulk email.

---

## Malspam

Spam containing:

```text
Malware

Malicious Links

Attachments
```

---

## Phishing

Impersonates trusted organizations.

Goal:

```text
Credential Theft

Malware Delivery
```

---

## Spear Phishing

Targeted phishing attack.

Victim is specifically chosen.

Uses:

```text
Personal Information

Company Information

Role Information
```

---

## Whaling

Targets executives.

Examples:

```text
CEO

CFO

Directors

Senior Managers
```

---

## Smishing

Phishing through:

```text
SMS

Text Messages
```

---

## Vishing

Phishing through:

```text
Phone Calls

VoIP Calls
```

---

# Anatomy of a Phishing Email

Most phishing emails share common characteristics.

---

# Spoofed Sender

Fake sender pretending to be:

```text
Microsoft

Google

Banks

Employers
```

---

# Urgency

Creates panic.

Examples:

```text
Account Locked

Password Expiring

Payment Failed

Security Alert
```

---

# Brand Impersonation

Uses:

```text
Official Logos

Corporate Colors

Professional Layouts
```

to appear legitimate.

---

# Grammar Issues

Common indicators:

```text
Spelling Errors

Strange Wording

Poor Formatting
```

Although AI has made this less reliable.

---

# Generic Greeting

Examples:

```text
Dear Customer

Dear User

Valued Member
```

instead of actual names.

---

# Hidden Links

Visible link:

```text
Microsoft Login
```

Actual destination:

```text
evil-login-site.com
```

---

# URL Shorteners

Examples:

```text
bit.ly

tinyurl

shorturl
```

Used to conceal destinations.

---

# Malicious Attachments

Examples:

```text
invoice.pdf.exe

salary_report.zip

urgent.docm
```

---

# Common Phishing Objectives

## Credential Harvesting

Steal:

```text
Usernames

Passwords

MFA Codes
```

---

## Malware Delivery

Deliver:

```text
Trojans

Ransomware

Remote Access Tools
```

---

## Financial Fraud

Examples:

```text
Wire Transfers

Gift Card Scams

Invoice Fraud
```

---

# Safe Email Analysis

Never directly interact with suspicious content.

---

# Hyperlink Safety

Do NOT click suspicious links.

Instead:

```text
Extract URL

Analyze Safely

Defang URL
```

---

# What is Defanging?

Defanging makes indicators safe to share.

---

# URL Defanging

Original:

```text
http://malicious-site.com
```

Defanged:

```text
hxxp[://]malicious-site[.]com
```

---

# Email Defanging

Original:

```text
attacker@gmail.com
```

Defanged:

```text
attacker[@]gmail[.]com
```

---

# Why Defang?

Prevents:

```text
Accidental Clicks

Automatic Hyperlinking

Accidental Execution
```

---

# SOC Email Investigation Checklist

When analyzing suspicious emails:

## Sender

```text
Who sent it?
```

---

## Domain

```text
Is the domain legitimate?
```

---

## Subject

```text
Does it create urgency?
```

---

## Links

```text
Where do they actually go?
```

---

## Attachments

```text
What file types are included?
```

---

## Headers

```text
What servers handled the email?

What is the originating IP?
```

---

## Intent

```text
Credential Theft?

Malware?

Fraud?

Spam?
```

---

# Quick Revision

## Email Protocols

```text
SMTP
=
Sending

POP3
=
Download

IMAP
=
Synchronization
```

---

## Email Components

```text
Address
Headers
Body
Attachments
```

---

## Header Analysis Focus

```text
From

Reply-To

Subject

Date

Originating IP
```

---

## Common Phishing Indicators

```text
Spoofed Sender

Urgency

Brand Impersonation

Generic Greetings

Hidden Links

Malicious Attachments
```

---

## Phishing Types

```text
Spam

Phishing

Spear Phishing

Whaling

Smishing

Vishing
```

---

# Final Takeaway

```text
SOC Analysts Do Not Trust The Displayed Email

They Verify:

Headers
Links
Attachments
Originating Infrastructure

Before Determining If An Email Is Legitimate
```
