# SOC Workbooks & Lookups

## Investigation Context

Alert triage often requires additional context about:

* Users
* Servers
* Workstations
* IP addresses
* Network segments

Without context, it is difficult to determine whether activity is legitimate or malicious.

---

# Identity Inventory

## Definition

A centralized catalogue of users, service accounts, and their attributes.

Contains information such as:

* Role
* Department
* Manager
* Contact details
* Permissions
* Access rights

---

## Purpose

Provides context about user activity.

Helps answer questions like:

* Who performed the action?
* Does the user normally have this access?
* Is the activity expected for their role?

---

## Common Sources

### Directory Services

* Active Directory
* Azure AD

### Identity Providers

* Okta
* Google Workspace

### HR Systems

* BambooHR
* SAP

### Internal Databases

* CSV inventories
* Excel sheets
* Custom portals

---

# Asset Inventory

## Definition

A catalogue of systems and computing assets within the organization.

Examples:

* Servers
* Workstations
* Laptops
* Virtual Machines

---

## Purpose

Provides context about affected systems.

Helps answer:

* What system is involved?
* What is its purpose?
* Is it sensitive or critical?

---

## Example Assets

### Domain Controller

```text id="qlnn25"
HQ-ADDC-01
```

### File Server

```text id="r4bftt"
HQ-FINFS-02
```

Stores:

```text id="lgb8qg"
Financial Records
```

---

## Common Sources

* Active Directory
* SIEM Platforms
* EDR Platforms
* MDM Solutions
* Internal Asset Databases

---

# Identity + Asset Context

A simple investigation formula:

```text id="f0a4su"
Identity Inventory
        +
Asset Inventory
        =
Investigation Context
```

Identity inventory explains:

```text id="v4r8jg"
Who
```

Asset inventory explains:

```text id="04xk0w"
Where
```

Together they help determine whether activity is expected or suspicious.

---

# Network Diagrams

## Definition

Visual representations of:

* Networks
* Subnets
* Servers
* Security devices
* Connections

---

## Purpose

Help analysts understand:

* Asset relationships
* Traffic flows
* Exposed services
* Attack paths

---

# What Network Diagrams Help Identify

## Exposed Services

Examples:

* VPN
* Web Servers
* Remote Access Services

---

## Subnet Functions

Examples:

### VPN Subnet

```text id="vczx8e"
10.10.0.0/16
```

### Database Subnet

```text id="66f0t9"
172.16.15.0/24
```

### Office Subnet

```text id="d9ruxn"
172.16.23.0/24
```

---

## Attack Path Reconstruction

Example:

```text id="9dwlx7"
Internet
    ↓
VPN Access
    ↓
Internal Network
    ↓
Subnet Scanning
    ↓
Lateral Movement
```

Network diagrams make it easier to understand how attackers move through an environment.

---

# Workbook

## Definition

A structured investigation guide that outlines the exact steps analysts should follow.

Also called:

* Playbook
* Runbook
* Workflow

---

## Purpose

* Standardize investigations
* Reduce mistakes
* Improve consistency
* Help junior analysts
* Speed up triage

---

# Who Uses Workbooks Most?

Primarily:

```text id="yg95e6"
SOC L1 Analysts
```

Workbooks reduce reliance on memory and experience.

---

# Workbook Structure

Most workbooks contain three major phases.

## 1. Enrichment

Gather context.

Examples:

* User information
* Asset information
* Threat intelligence
* IP reputation

Purpose:

```text id="z7cx8e"
Understand the alert context
```

---

## 2. Investigation

Analyze available evidence.

Examples:

* SIEM logs
* EDR events
* User behavior
* Authentication logs

Purpose:

```text id="6h0g1t"
Determine if activity is suspicious
```

---

## 3. Escalation

Performed if the alert requires additional investigation.

Examples:

* Create report
* Collect evidence
* Assign to L2

Purpose:

```text id="1ivk7v"
Continue investigation at higher tier
```

---

# Generic Workbook Flow

```text id="n89c2i"
Receive Alert
      ↓
Assign To Yourself
      ↓
Enrichment
      ↓
Investigation
      ↓
Verdict
      ↓
Close OR Escalate
```

---

# Common Investigation Workflow

```text id="xz9u3r"
Assign Alert
      ↓
Collect Context
      ↓
Review Evidence
      ↓
Determine Verdict
      ↓
Document Findings
      ↓
Close / Escalate
```

---

# Workbook Philosophy

A good workbook should:

* Be simple
* Be repeatable
* Minimize analyst mistakes
* Produce consistent results

---

# Key Terms

## Identity Inventory

```text id="pbx5iy"
Who is involved?
```

---

## Asset Inventory

```text id="7g4m40"
What system is involved?
```

---

## Network Diagram

```text id="uvr3y3"
How is the environment connected?
```

---

## Enrichment

```text id="zcjlwm"
Gather context before investigation
```

---

## Investigation

```text id="crstlm"
Analyze evidence and activity
```

---

## Escalation

```text id="lq3a0f"
Pass alert to higher-tier analysts
```

---

# Quick Revision

### Identity Inventory

```text id="br1fqo"
Who?
```

### Asset Inventory

```text id="yyc0xu"
Where?
```

### Network Diagram

```text id="okn8km"
How is it connected?
```

### Workbook Phases

```text id="r9zbmv"
Enrichment
    ↓
Investigation
    ↓
Escalation
```

### Analyst Workflow

```text id="3zivj8"
Assign
 ↓
Enrich
 ↓
Investigate
 ↓
Verdict
 ↓
Close / Escalate
```

### Main Goal

```text id="xg5ffn"
Use context to make better triage decisions.
```
