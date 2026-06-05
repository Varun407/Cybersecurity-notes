# SIEM (Security Information and Event Management)

## What is SIEM?

SIEM is a centralized security solution that:

* Collects logs from multiple sources
* Normalizes log formats
* Correlates events
* Detects suspicious activity
* Generates alerts
* Provides dashboards and reporting

---

# Why SIEM Exists

Modern networks contain many devices:

* Windows endpoints
* Linux endpoints
* Servers
* Firewalls
* Routers
* IDS/IPS
* Web servers

All of these continuously generate logs.

Without SIEM:

```text id="l5n2f7"
Many Devices
      ↓
Many Logs
      ↓
Scattered Data
      ↓
Difficult Investigation
```

---

# Log Sources

A log source is any device or application that generates logs.

Two major categories:

```text id="r7w9a1"
Host-Centric
Network-Centric
```

---

# Host-Centric Log Sources

## Definition

Logs generated within a host or operating system.

---

## Examples

### Authentication

* Login attempts
* Failed logins

### File Activity

* File access
* File modification

### Process Activity

* Process creation
* Process termination

### Registry Activity

* Registry modifications
* Registry deletion

### PowerShell Activity

* Script execution
* Command execution

---

## Common Devices

* Windows systems
* Linux systems
* Servers
* Workstations

---

# Network-Centric Log Sources

## Definition

Logs generated when systems communicate over a network.

---

## Examples

### Remote Access

* SSH sessions
* VPN connections

### File Transfer

* FTP activity
* SMB file sharing

### Web Activity

* HTTP requests
* HTTPS requests

### Network Traffic

* Internal communications
* Internet access

---

## Common Devices

* Firewalls
* Routers
* IDS
* IPS
* VPN Gateways

---

# Problems Without SIEM

## Numerous Log Sources

Organizations generate thousands or millions of logs daily.

Manual review becomes impossible.

---

## No Centralization

Analysts may need to access:

* RDP
* SSH
* Web interfaces

on multiple devices.

Very inefficient during incidents.

---

## Limited Context

A single event rarely tells the complete story.

Example:

```text id="n6v5z3"
VPN Login
      +
File Access
      +
PowerShell Execution
      +
Outbound Connection
```

Individually:

```text id="y1x8m4"
Looks Normal
```

Together:

```text id="u9k2q6"
Potential Data Exfiltration
```

---

## Limited Analysis

Humans cannot manually analyze millions of events.

Important indicators may be missed.

---

## Different Log Formats

Examples:

* Windows Event Logs
* Linux Logs
* Firewall Logs
* Web Server Logs

Every source uses different formats.

---

# Core SIEM Features

## Centralized Log Collection

Collects logs from:

* Endpoints
* Servers
* Firewalls
* Applications
* Network Devices

Stores everything in one location.

---

## Parsing

### Definition

Breaking raw logs into individual fields.

Example:

```text id="g4p9e8"
Timestamp
Username
Source IP
Destination IP
Event ID
```

---

## Normalization

### Definition

Converting logs from different sources into a consistent format.

---

### Goal

```text id="f7m3x2"
Different Logs
      ↓
Common Structure
```

Allows easier searching and analysis.

---

## Correlation

### Definition

Connecting related events from multiple log sources.

---

### Example

```text id="j5w8n1"
VPN Login
      ↓
Shared Drive Access
      ↓
PowerShell Execution
      ↓
External Connection
```

Correlation reveals attack patterns that individual logs cannot.

---

## Real-Time Alerting

SIEM uses detection rules.

When rule conditions match:

```text id="d3k6v9"
Rule Triggered
      ↓
Alert Generated
      ↓
Analyst Notified
```

---

## Dashboards

Provide summarized visibility into security events.

Common dashboard data:

* Alert counts
* Triggered rules
* Failed logins
* System health
* Event volume
* Top visited domains

---

# Common Log Sources

## Windows Logs

Stored and viewed through:

```text id="s8r4t1"
Event Viewer
```

Windows uses Event IDs to identify activities.

Examples:

* Logon events
* Process creation
* Account changes

---

## Linux Logs

Common locations:

### Authentication Logs

```text id="w7c1m5"
/var/log/auth.log
/var/log/secure
```

---

### Cron Logs

```text id="p2n8k4"
/var/log/cron
```

---

### Kernel Logs

```text id="r5j9x7"
/var/log/kern
```

---

### HTTP Logs

```text id="b3f6q1"
/var/log/httpd
```

---

## Web Server Logs

Contain:

* Requests
* Responses
* Errors
* User agents
* Source IPs

Useful for detecting:

* Web attacks
* Reconnaissance
* Exploitation attempts

---

# Log Ingestion Methods

## Agent / Forwarder

Installed on endpoints.

Responsible for:

```text id="t4v7n3"
Collect Logs
      ↓
Send To SIEM
```

Example:

```text id="m8w2r5"
Splunk Forwarder
```

---

## Syslog

Standard protocol for log forwarding.

Commonly used by:

* Linux
* Firewalls
* Network Devices

---

## Manual Upload

Used for:

* Offline analysis
* Incident investigations
* Historical log review

---

## Port Forwarding

Devices send logs directly to a listening SIEM port.

---

# Detection Rules

## Definition

Logical conditions used to identify suspicious activity.

---

# Example Rules

## Multiple Failed Logins

```text id="q9x4c8"
5 Failed Logins
Within 10 Seconds
      ↓
Generate Alert
```

---

## Successful Login After Failures

```text id="e7n5m2"
Multiple Failures
      ↓
Successful Login
      ↓
Generate Alert
```

---

## USB Detection

```text id="z2j6p4"
USB Inserted
      ↓
Generate Alert
```

---

## Data Exfiltration

```text id="h5w1k8"
Outbound Traffic > 25MB
      ↓
Generate Alert
```

---

# Windows Detection Examples

## Event Log Cleared

### Event ID

```text id="x4m9r7"
104
```

---

### Detection Logic

```text id="v8q3k5"
Log Source = WinEventLog
AND
EventID = 104
      ↓
Alert
```

---

## WHOAMI Execution Detection

### Event ID

```text id="c1n6w9"
4688
```

(Process Creation)

---

### Detection Logic

```text id="u3p8m2"
Log Source = WinEventLog
AND
EventID = 4688
AND
NewProcessName contains whoami
      ↓
Alert
```

---

# Alert Investigation Workflow

```text id="k6r2v4"
Alert Triggered
      ↓
Review Events
      ↓
Review Detection Rule
      ↓
Analyze Context
      ↓
Determine Verdict
```

---

# Possible Outcomes

## False Positive

Activity is legitimate.

Actions:

* Close alert
* Tune detection rule

---

## True Positive

Malicious activity confirmed.

Actions:

* Continue investigation
* Escalate if needed
* Contact asset owner
* Isolate affected host
* Block malicious IP

---

# Important Terms

## Parsing

```text id="j7n4c1"
Break logs into fields
```

---

## Normalization

```text id="p5x8w6"
Convert logs into common format
```

---

## Correlation

```text id="m2q7r9"
Connect related events
```

---

## Detection Rule

```text id="s1v5k8"
Logic that generates alerts
```

---

## Alert

```text id="f9t3m4"
Notification of suspicious activity
```

---

# Quick Revision

### Host-Centric

```text id="b8n1w7"
Activity inside a system
```

Examples:

* Registry
* PowerShell
* Logins
* File Access

---

### Network-Centric

```text id="r4m6p2"
Activity across a network
```

Examples:

* VPN
* SSH
* FTP
* Web Traffic

---

### SIEM Functions

```text id="t9w3k6"
Collect
Normalize
Correlate
Detect
Alert
Report
```

---

### Linux HTTP Logs

```text id="y6n2q4"
/var/log/httpd
```

---

### Event Log Cleared

```text id="h8c5m1"
Event ID 104
```

---

### Process Creation

```text id="u1r7v3"
Event ID 4688
```

---

### Rule Tuning Needed For

```text id="q3m9w8"
False Positives
```

---

### SIEM Formula

```text id="z7k2n5"
Logs
  ↓
Parsing
  ↓
Normalization
  ↓
Correlation
  ↓
Detection Rules
  ↓
Alerts
  ↓
Investigation
```
