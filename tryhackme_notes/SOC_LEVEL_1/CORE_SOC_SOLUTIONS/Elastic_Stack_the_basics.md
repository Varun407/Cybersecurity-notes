# ELK Stack (Elastic Stack)

## What is ELK?

The Elastic Stack (ELK) is a collection of tools used to:

* Collect logs
* Process data
* Search data
* Analyze events
* Create visualizations
* Build dashboards

Although ELK is not a traditional SIEM, many SOC teams use it as one because of its powerful searching and visualization capabilities.

---

# ELK Components

The Elastic Stack consists of four major components:

```text
Beats
   ↓
Logstash
   ↓
Elasticsearch
   ↓
Kibana
```

---

# Elasticsearch

## Definition

Elasticsearch is the core search and analytics engine of ELK.

---

## Responsibilities

* Store logs and events
* Search large amounts of data quickly
* Correlate information
* Perform analytics

---

## Characteristics

* Stores JSON documents
* Uses REST APIs
* Supports fast full-text searching
* Highly scalable

---

## Think of Elasticsearch as

```text
Database + Search Engine
```

for security logs.

---

# Logstash

## Definition

Logstash is a data processing pipeline.

---

## Responsibilities

* Receive data
* Transform data
* Normalize data
* Forward data

---

## Logstash Workflow

```text
Input
   ↓
Filter
   ↓
Output
```

---

### Input

Defines where data comes from.

Examples:

* Syslog
* Beats
* Files
* Databases

---

### Filter

Processes and normalizes data.

Examples:

* Parsing
* Field extraction
* Data enrichment

---

### Output

Defines where data is sent.

Examples:

* Elasticsearch
* Files
* Other systems

---

# Beats

## Definition

Lightweight agents that collect data from endpoints.

---

## Purpose

Send logs from systems to Logstash or Elasticsearch.

---

## Common Beats

### Winlogbeat

Collects Windows Event Logs.

---

### Filebeat

Collects log files.

---

### Packetbeat

Collects network traffic.

---

### Metricbeat

Collects system metrics.

---

### Auditbeat

Collects Linux audit events.

---

# Kibana

## Definition

Web-based interface used to search, investigate, visualize, and analyze data stored in Elasticsearch.

---

## Responsibilities

* Search logs
* Investigate incidents
* Build dashboards
* Create visualizations

---

## Think of Kibana as

```text
SOC Analyst Workspace
```

---

# ELK Data Flow

```text
Endpoints
     ↓
   Beats
     ↓
 Logstash
     ↓
Elasticsearch
     ↓
  Kibana
```

---

# Discover Tab

The Discover tab is where SOC analysts spend most of their investigation time.

---

## Purpose

* Search logs
* Filter events
* Investigate incidents
* Analyze raw data

---

# Main Components of Discover

## Logs View

Each row represents a single event.

Expanding an event shows:

* Fields
* Values
* Metadata

---

## Fields Panel

Displays all available fields.

Examples:

* Source_IP
* UserName
* Country
* Action

---

### Quick Filtering

```text
+  Include Value
-  Exclude Value
```

Useful for narrowing investigations quickly.

---

## Index Pattern

Defines which logs are being searched.

Examples:

```text
vpn_connections
windows_logs
firewall_logs
```

---

## Search Bar

Used to create queries.

Supports:

* Keywords
* Filters
* KQL

---

## Time Filter

Limits events by time.

Examples:

* Last 15 minutes
* Last 24 hours
* Custom dates

---

## Timeline Chart

Displays event counts over time.

Useful for:

* Detecting spikes
* Finding anomalies
* Identifying unusual activity

---

## Add Filter

Creates structured filters without writing queries manually.

---

## Table View

Allows displaying only important fields.

Example:

```text
IP
Username
Country
Action
```

Reduces noise during investigations.

---

# KQL (Kibana Query Language)

## Definition

KQL is the query language used in Kibana for searching and filtering logs.

---

# Free Text Search

Searches all fields.

Example:

```kql
security
```

Returns documents containing:

```text
security
```

---

# Wildcards

Used for partial matching.

Example:

```kql
United*
```

Matches:

```text
United States
United Kingdom
```

---

# Logical Operators

## OR

```kql
"United States" OR "England"
```

---

## AND

```kql
"United States" AND "Virginia"
```

---

## NOT

```kql
"United States" AND NOT "Florida"
```

---

# Field-Based Searches

Syntax:

```kql
Field : Value
```

Example:

```kql
Source_ip : 238.163.231.224
```

---

# Multiple Conditions

Example:

```kql
Source_Country : "United States"
AND
UserName : James
```

---

# OR Conditions

Example:

```kql
UserName : James
OR
UserName : Albert
```

---

# Combined Queries

Example:

```kql
Source_Country : "United States"
AND
(UserName : James OR UserName : Albert)
```

---

# Time-Based Searches

Search activity after a specific date:

```kql
UserName : "Johny Brown"
AND
@timestamp > "2022-01-01T00:00:00.000Z"
```

Useful for:

* Insider threat investigations
* Employee termination monitoring
* Incident timelines

---

# Investigation Workflow in Kibana

```text
Select Index
      ↓
Set Time Range
      ↓
Review Timeline
      ↓
Identify Spike
      ↓
Filter Logs
      ↓
Analyze Fields
      ↓
Determine Cause
```

---

# Common Investigation Fields

## Source_IP

Identifies where activity originated.

---

## UserName

Identifies who performed activity.

---

## Source_Country

Geographic origin of activity.

---

## Source_State

More detailed location information.

---

## Action

Indicates activity performed.

Examples:

```text
Success
Failed
Login
Disconnect
```

---

## Timestamp

Shows when activity occurred.

---

# Visualizations

## Purpose

Convert raw logs into meaningful charts and graphs.

---

## Common Visualizations

### Pie Charts

Show distribution.

Example:

```text
Top Countries
```

---

### Bar Charts

Compare values.

Example:

```text
Failed Logins Per User
```

---

### Tables

Display structured information.

Example:

```text
IP Address
Country
Number of Events
```

---

# Correlation Analysis

Visualizations can correlate multiple fields.

Example:

```text
Source Country
        vs
Source IP
```

Useful for:

* Threat hunting
* Pattern recognition
* Identifying anomalies

---

# Dashboards

## Definition

A collection of visualizations displayed together.

---

## Purpose

Provide a single pane of glass for monitoring.

---

## Dashboard Workflow

```text
Logs
   ↓
Visualizations
   ↓
Dashboard
   ↓
Monitoring
```

---

# SOC Use Cases for ELK

## VPN Monitoring

* Failed logins
* Suspicious countries
* Unusual access times

---

## Threat Hunting

Search for:

* Suspicious IPs
* Malicious domains
* Lateral movement

---

## Incident Investigation

Correlate:

* User activity
* Source IPs
* Geographic locations
* Time ranges

---

## Security Monitoring

Track:

* Authentication events
* Network traffic
* Endpoint activity

---

# ELK vs Splunk

| Feature         | ELK                | Splunk     |
| --------------- | ------------------ | ---------- |
| Cost            | Mostly Open Source | Commercial |
| Search Engine   | Elasticsearch      | SPL        |
| Visualization   | Kibana             | Dashboards |
| Data Collection | Beats              | Forwarder  |
| Processing      | Logstash           | Indexer    |

---

# Key Terms

## Elasticsearch

Stores and searches logs.

---

## Logstash

Processes and normalizes logs.

---

## Beats

Collects and ships logs.

---

## Kibana

Searches and visualizes data.

---

## KQL

Query language used in Kibana.

---

## Index Pattern

Defines which logs are searched.

---

## Visualization

Graphical representation of data.

---

## Dashboard

Collection of visualizations.

---

# Quick Revision

### ELK Components

```text
Beats
   ↓
Logstash
   ↓
Elasticsearch
   ↓
Kibana
```

---

### Logstash Pipeline

```text
Input
 ↓
Filter
 ↓
Output
```

---

### Kibana Discover

```text
Search
Filter
Investigate
Analyze
```

---

### KQL Operators

```text
AND
OR
NOT
```

---

### Most Important Fields

```text
Source_IP
UserName
Country
Action
Timestamp
```

---

### Analyst Workflow

```text
Logs
 ↓
Discover
 ↓
KQL Search
 ↓
Visualization
 ↓
Dashboard
 ↓
Investigation
```

---

### Remember

```text
Beats Collect
Logstash Processes
Elasticsearch Stores
Kibana Visualizes
```
