# SOAR (Security Orchestration, Automation and Response)

## What is SOAR?

SOAR stands for:

```text
Security
Orchestration
Automation
Response
```

SOAR is a platform that integrates multiple security tools and automates security workflows to improve incident response efficiency.

It acts as a central platform connecting:

* SIEM
* EDR
* Firewalls
* IAM Solutions
* Threat Intelligence Platforms
* Ticketing Systems

---

# Traditional SOC

## What is a SOC?

A Security Operations Center (SOC) is a centralized team responsible for:

* Monitoring security events
* Detecting threats
* Investigating incidents
* Responding to attacks
* Protecting organizational assets

A SOC relies on three key elements:

```text
People
Processes
Technology
```

---

# Core SOC Capabilities

## Monitoring & Detection

Continuous monitoring of systems and networks to identify suspicious activity.

Examples:

* Failed logins
* Brute force attacks
* Unusual access patterns
* Malware detections

Common Tools:

* SIEM
* EDR
* IDS/IPS

---

## Recovery & Remediation

Taking actions to contain and eliminate threats.

Examples:

* Isolating endpoints
* Blocking malicious IPs
* Disabling user accounts
* Removing malware

Common Tools:

* EDR
* Firewall
* IAM

---

## Threat Intelligence

Using external intelligence feeds to identify known threats.

Examples:

* Malicious IP addresses
* Malicious domains
* Malware hashes
* Threat actor indicators

---

## Communication

SOC analysts coordinate with:

* IT Teams
* System Administrators
* Management
* Incident Response Teams

Activities include:

* Ticket creation
* Escalations
* Incident reporting
* Status updates

---

# Challenges of Traditional SOCs

## Alert Fatigue

### Definition

A condition where analysts are overwhelmed by excessive security alerts.

---

### Causes

* High alert volume
* False positives
* Duplicate alerts
* Poor detection tuning

---

### Impact

* Missed threats
* Slower investigations
* Analyst burnout
* Reduced efficiency

---

## Disconnected Tools

Many security tools operate independently.

Example:

```text
Firewall Logs
      ↓
      X
Endpoint Logs
```

No integration means analysts must manually gather information.

---

### Problems

* Context switching
* Slower investigations
* Inconsistent workflows

---

## Manual Processes

Many organizations rely on undocumented analyst knowledge.

Example:

```text
Alert
 ↓
Manual Checks
 ↓
Manual Investigation
 ↓
Manual Escalation
```

---

### Problems

* Slow response times
* Human error
* Inconsistent investigations

---

## Talent Shortage

Security professionals are in high demand.

Combined with alert fatigue, this creates:

* Burnout
* Longer response times
* Investigation backlogs

---

# How SOAR Solves These Problems

SOAR centralizes tools and automates repetitive processes.

```text
SIEM
EDR
Firewall
Threat Intel
IAM
Ticketing
      ↓
     SOAR
```

---

# Core SOAR Capabilities

## 1. Orchestration

### Definition

Connecting and integrating multiple security tools into a unified workflow.

---

### Purpose

Allow tools to work together automatically.

---

### Example

VPN Brute Force Alert:

```text
Alert Received
      ↓
Query SIEM Logs
      ↓
Check Threat Intel
      ↓
Review Login Activity
      ↓
Escalate if Suspicious
```

Instead of analysts performing every step manually, SOAR coordinates the process.

---

# 2. Automation

### Definition

Automatically executing predefined tasks without analyst interaction.

---

### Example

```text
Alert Received
      ↓
Check IP Reputation
      ↓
Query SIEM
      ↓
Disable User
      ↓
Create Ticket
```

---

### Benefits

* Faster response
* Reduced workload
* Consistent investigations
* Reduced alert fatigue

---

# 3. Response

### Definition

Executing security actions directly through integrated tools.

---

### Example Actions

* Block IP address
* Disable user account
* Quarantine endpoint
* Create ticket
* Notify stakeholders

---

# Benefits of SOAR

## Reduced Alert Fatigue

Automates repetitive investigation tasks.

---

## Improved Integration

Connects previously disconnected tools.

---

## Faster Investigations

Reduces manual effort.

---

## Consistent Processes

Uses predefined workflows instead of undocumented procedures.

---

## Better Incident Response

Allows quicker containment and remediation.

---

# Do SOAR Platforms Replace Analysts?

## No

SOAR improves efficiency but does not replace human analysts.

---

## Why Analysts Are Still Needed

### Human Judgment

Not every alert can be handled automatically.

---

### Context Awareness

Analysts understand:

* Business operations
* Risk levels
* Threat impact

---

### Playbook Development

Analysts design and improve playbooks.

---

### Advanced Investigations

Complex incidents still require human expertise.

---

# SOAR Playbooks

## What is a Playbook?

A playbook is a predefined workflow that describes how an alert or incident should be handled.

---

## Purpose

* Standardize investigations
* Reduce manual work
* Automate repetitive actions

---

# Phishing Playbook

## Problem

Phishing investigations consume significant analyst time.

---

## Workflow

```text
Suspicious Email Alert
           ↓
      Create Ticket
           ↓
Contains URL?
      ↓        ↓
    Yes        No
     ↓          ↓
Check URL    Notify User
Reputation
     ↓
Malicious?
  ↓      ↓
Yes      No
 ↓        ↓
Block    Close
```

---

## Attachment Investigation

```text
Attachment Found
        ↓
 Sandbox Analysis
        ↓
 AV Scan
        ↓
Malicious?
    ↓      ↓
  Yes      No
   ↓        ↓
Block     Close
```

---

## Remediation Actions

* Quarantine email
* Block sender
* Notify users
* Update ticket

---

# CVE Patching Playbook

## Problem

New vulnerabilities are discovered continuously.

Organizations must quickly identify affected assets and deploy patches.

---

## Workflow

```text
New CVE Released
        ↓
Ingest CVE Details
        ↓
Assess Risk
        ↓
Search Asset Inventory
        ↓
Vulnerable Assets?
     ↓         ↓
   Yes         No
    ↓           ↓
Create Ticket  Close
    ↓
Test Patch
    ↓
Deploy Patch
    ↓
Validate Fix
```

---

# CVE Information Sources

Common sources include:

* Vendor advisories
* Security advisories
* Vulnerability databases
* Threat intelligence feeds

---

# If Patch Fails

If systems remain vulnerable:

```text
Patch Deployed
      ↓
Still Vulnerable?
      ↓
     Yes
      ↓
Develop Mitigation Plan
```

---

## Mitigation Examples

* Temporary firewall rules
* Service restrictions
* Application isolation
* Additional monitoring

---

# Threat Intelligence Workflow

Threat Intelligence workflows automate indicator analysis and response.

---

# Typical Workflow

```text
Indicator Received
        ↓
Create Case
        ↓
Extract Data
        ↓
Threat Intelligence Lookup
        ↓
Reputation Check
        ↓
Determine Action
        ↓
Update Case
```

---

# Automated Activities

## Case Management

* Create ticket
* Assign ticket
* Update ticket
* Notify teams

---

## Threat Intelligence

* Fetch threat feeds
* Update indicators
* Perform lookups

---

## Data Extraction

Automatically extract:

* Domains
* URLs
* IP addresses
* Hashes

---

## Reputation Checks

Automatically query:

* Threat Intelligence Platforms
* Malware Databases
* Reputation Services

---

## Response Actions

Automatically:

* Block IPs
* Block domains
* Block URLs
* Update tickets

---

# Activities That Usually Need Human Approval

Examples:

* Validating results
* Confirming investigations
* Approving containment actions
* Approving business-impacting changes

---

# SOC + SOAR Workflow

```text
Alert Generated
       ↓
      SOAR
       ↓
Run Playbook
       ↓
Gather Evidence
       ↓
Threat Intel Checks
       ↓
Automated Actions
       ↓
Analyst Review
       ↓
Containment / Escalation
```

---

# Key Terms

## SOAR

Security Orchestration, Automation and Response.

---

## Orchestration

Connecting multiple security tools into a unified workflow.

---

## Automation

Performing predefined actions automatically.

---

## Response

Executing remediation actions against threats.

---

## Playbook

A predefined workflow for handling security incidents.

---

## Alert Fatigue

Analyst overload caused by excessive alerts.

---

## Threat Intelligence

Information about known threats and malicious indicators.

---

## Mitigation Plan

Alternative security controls used when a vulnerability cannot be fully remediated.

---

# Quick Revision

## Traditional SOC Challenges

```text
Alert Fatigue
Disconnected Tools
Manual Processes
Talent Shortage
```

---

## SOAR Capabilities

```text
Orchestration
Automation
Response
```

---

## SOAR Benefits

```text
Reduced Manual Work
Faster Investigations
Integrated Tools
Consistent Response
Lower Alert Fatigue
```

---

## Playbook Purpose

```text
Standardize
Automate
Accelerate
```

---

## Remember

```text
SOAR Handles Repetition
Analysts Handle Decisions
```

---

## Complete SOAR Flow

```text
Alert
 ↓
SOAR
 ↓
Playbook
 ↓
Automation
 ↓
Analyst Review
 ↓
Response
```
