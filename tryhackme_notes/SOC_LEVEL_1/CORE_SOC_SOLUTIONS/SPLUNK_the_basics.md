# Splunk: The Basics

## What is Splunk?

Splunk is a SIEM platform used to:

* Collect logs
* Store logs
* Search logs
* Correlate events
* Detect threats
* Investigate incidents
* Create dashboards and reports

---

# Why Splunk is Important

Organizations generate logs from:

* Windows systems
* Linux systems
* Web servers
* Databases
* Firewalls
* VPN devices
* Security tools

Splunk centralizes and analyzes these logs.

```text
Multiple Log Sources
        ↓
     Splunk
        ↓
Search & Analysis
        ↓
Detection & Investigation
```

---

# Splunk Architecture

Splunk consists of three main components:

```text
Forwarder
    ↓
Indexer
    ↓
Search Head
```

---

# Splunk Forwarder

## Definition

A lightweight agent installed on monitored systems.

---

## Purpose

* Collect logs
* Forward logs to Splunk

---

## Characteristics

* Lightweight
* Low resource usage
* Minimal performance impact

---

## Common Data Sources

### Windows

* Event Logs
* PowerShell Logs
* Sysmon Logs

### Linux

* Authentication Logs
* System Logs

### Web Servers

* Apache Logs
* Nginx Logs

### Databases

* Queries
* Connections
* Errors

---

## Workflow

```text
Endpoint
    ↓
Forwarder
    ↓
Indexer
```

---

# Splunk Indexer

## Definition

The core processing engine of Splunk.

---

## Responsibilities

### Parsing

Breaks raw logs into fields.

Example:

```text
Timestamp
Username
IP Address
Event Type
```

---

### Normalization

Converts logs into a searchable format.

---

### Indexing

Stores processed logs as events.

---

## Workflow

```text
Raw Logs
    ↓
Parsing
    ↓
Normalization
    ↓
Indexing
    ↓
Searchable Events
```

---

# Splunk Search Head

## Definition

The interface analysts use to search and investigate data.

---

## Responsibilities

* Run searches
* Investigate alerts
* Create reports
* Build dashboards

---

## Uses

```text
Search
Analyze
Visualize
Report
```

---

# SPL (Search Processing Language)

## Definition

Splunk's query language used to search indexed data.

---

## Purpose

Allows analysts to:

* Filter events
* Search logs
* Investigate incidents
* Generate statistics

---

## Example

```spl
UserName=Maleena
```

Returns all events associated with user Maleena.

---

# Splunk Interface

## Splunk Bar

Top navigation panel.

Contains:

### Messages

System notifications.

### Settings

Configuration options.

### Activity

Search job status.

### Help

Documentation and tutorials.

### Find

Search across Splunk.

---

# Apps Panel

Displays installed applications.

Default application:

```text
Search & Reporting
```

---

# Explore Splunk

Provides shortcuts for:

* Adding data
* Installing apps
* Documentation

---

# Dashboards

## Purpose

Visual representation of security and operational data.

---

## Common Dashboard Information

* Alert counts
* Triggered rules
* Event volume
* Failed logins
* System health
* Top sources
* Top users

---

# Data Ingestion

## Definition

The process of bringing logs into Splunk.

---

## Data Sources

* Event Logs
* VPN Logs
* Firewall Logs
* Web Logs
* System Logs
* Application Logs

---

## Ingestion Workflow

```text
Log Source
      ↓
Forwarder / Upload
      ↓
Indexer
      ↓
Parsing
      ↓
Normalization
      ↓
Index
      ↓
Searchable Events
```

---

# Uploading Data

Typical upload process:

### 1. Select Source

Choose log file.

---

### 2. Select Source Type

Examples:

* JSON
* Syslog
* CSV
* XML

---

### 3. Input Settings

Configure:

* Index
* Hostname

---

### 4. Review

Verify settings.

---

### 5. Done

Data becomes searchable.

---

# Important Splunk Terms

## Source

Original file or location generating logs.

Example:

```text
VPNlogs.json
```

---

## Host

Device generating logs.

Example:

```text
VPN_Connections
```

---

## Sourcetype

Format of ingested data.

Examples:

```text
_json
syslog
csv
```

---

## Index

Logical storage location for events.

Example:

```text
VPN_Logs
```

---

# Basic SPL Searches

## Search All Events

```spl
index=vpn_logs
```

---

## Search Specific User

```spl
UserName=Maleena
```

---

## Search Specific IP

```spl
Source_ip="107.14.182.38"
```

---

## Exclude Values

```spl
Source_Country!=France
```

---

## Combined Search

```spl
index=vpn_logs UserName=Maleena
```

---

# Common Investigation Fields

## UserName

Identifies the user associated with activity.

---

## Source_ip

IP address where activity originated.

---

## Source_Country

Country associated with source IP.

---

## Host

System generating logs.

---

## Sourcetype

Type/format of logs.

---

# Practical Investigation Examples

## Find User Activity

```spl
UserName=Maleena
```

Used to investigate a specific user.

---

## Investigate IP Address

```spl
Source_ip="107.14.182.38"
```

Used to identify:

* User
* Location
* Activity

---

## Exclude a Country

```spl
Source_Country!=France
```

Useful during:

* Threat hunting
* Geographic filtering
* Investigation narrowing

---

# Splunk Investigation Workflow

```text
Logs Ingested
      ↓
Search Events
      ↓
Filter Results
      ↓
Identify Suspicious Activity
      ↓
Investigate Context
      ↓
Determine Verdict
```

---

# Splunk in SOC Operations

SOC Analysts use Splunk for:

### Monitoring

Observe network activity.

### Threat Detection

Identify suspicious behavior.

### Incident Investigation

Analyze alerts and events.

### Threat Hunting

Search for hidden threats.

### Reporting

Generate security reports.

---

# Key Terms

## Forwarder

Collects and sends logs.

---

## Indexer

Processes and stores logs.

---

## Search Head

Provides search and analysis interface.

---

## SPL

Splunk Search Processing Language.

---

## Source

Original log source.

---

## Host

System generating logs.

---

## Sourcetype

Log format identifier.

---

## Index

Storage location for logs.

---

# Quick Revision

### Splunk Components

```text
Forwarder → Collect
Indexer → Process & Store
Search Head → Search & Analyze
```

---

### Indexer Responsibilities

```text
Parsing
Normalization
Indexing
```

---

### SPL Purpose

```text
Search
Filter
Investigate
Analyze
```

---

### Common Fields

```text
UserName
Source_ip
Source_Country
Host
Sourcetype
Index
```

---

### Data Flow

```text
Log Source
     ↓
Forwarder
     ↓
Indexer
     ↓
Search Head
     ↓
Analyst
```

---

### Most Important Concept

```text
Raw Logs
     ↓
Forwarder
     ↓
Indexer
     ↓
Searchable Events
     ↓
SPL Searches
     ↓
Investigation
```
