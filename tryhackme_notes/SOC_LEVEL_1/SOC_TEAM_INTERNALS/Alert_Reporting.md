# SOC L1 Alert Reporting & Escalation

## After Alert Triage

After investigating an alert, an L1 analyst may:

* Close it as a False Positive
* Resolve it on the L1 level
* Escalate it to L2 for further investigation
* Request assistance from senior analysts

---

# Key Terms

## Alert Reporting

Formal documentation of investigation findings, evidence, and verdict.

Purpose:

* Provide context for L2 analysts
* Preserve investigation details
* Improve investigation quality
* Create long-term records

---

## Alert Escalation

Process of passing an alert to a higher-level analyst (usually L2) for further investigation or remediation.

Typical flow:

```text
L1 Analyst
    ↓
Investigate Alert
    ↓
Write Report
    ↓
Escalate to L2
```

---

## Communication

Interaction with other teams or users during an investigation.

Examples:

* IT Team
* HR Team
* System Owners
* Management
* Security Team

---

# Why Alert Reports Matter

## Provide Context

A good report helps L2 analysts understand:

* What happened
* What was investigated
* Why the verdict was chosen

Without repeating the entire investigation.

---

## Preserve Evidence

Raw logs may only be retained for a limited time.

Reports preserve:

* Key findings
* Indicators
* Investigation results
* Analyst reasoning

---

## Improve Investigation Skills

A useful principle:

> If you can't explain it clearly, you probably don't understand it completely.

Writing reports forces analysts to organize their thoughts and justify conclusions.

---

# Five Ws Reporting Method

A simple structure for alert reports.

## Who

Who performed the activity?

Examples:

* Username
* Email Address
* Service Account

---

## What

What happened?

Examples:

* Phishing email received
* Suspicious login
* Malware execution
* Data download

---

## When

When did the activity occur?

Include:

* Start time
* End time
* Relevant timestamps

---

## Where

Where did the activity occur?

Examples:

* Hostname
* IP Address
* Website
* Cloud Resource

---

## Why

Most important section.

Explain:

* Why activity is suspicious
* Why alert is benign
* Why TP or FP verdict was chosen

---

# Escalation Criteria

Escalate when:

## Major Security Incident

Examples:

* Active compromise
* Data breach
* Malware outbreak

---

## Remediation Required

Examples:

* Password reset
* Host isolation
* Malware removal
* Account disablement

---

## External Communication Required

Examples:

* Customers
* Partners
* Management
* Legal teams
* Law enforcement

---

## Lack of Understanding

Escalate if:

* Investigation is unclear
* Evidence is insufficient
* Additional expertise is needed

Better to escalate than incorrectly close an alert.

---

# Escalation Workflow

```text
Receive Alert
      ↓
Investigate
      ↓
Write Report
      ↓
Determine Verdict
      ↓
Assign to L2
      ↓
L2 Continues Investigation
```

L2 analysts use the report as their starting point.

---

# Requesting L2 Support

Common situations:

* Unclear alert behaviour
* Missing logs
* Unknown technology
* Uncertain verdict

Recommended approach:

```text
Ask Questions
    >
Assume Nothing
    >
Learn From Feedback
```

---

# Communication Scenarios

## Critical Alert but L2 Not Responding

Recommended escalation path:

```text
L2
 ↓
L3
 ↓
Manager
```

Do not immediately jump to management.

---

## Compromised Communication Platform

Example:

* Teams account compromised
* Slack account compromised

Do NOT communicate through the suspected compromised platform.

Use:

* Phone call
* Alternative messaging platform
* Email (if trusted)

---

## Alert Flood

If many alerts appear simultaneously:

* Prioritize normally
* Inform L2 immediately
* Continue processing critical alerts first

---

## Misclassified Alert

If you later believe an alert was wrongly closed:

* Notify L2 immediately
* Explain concerns
* Reopen investigation if necessary

Attackers may remain undetected for days or weeks.

---

## Logging or SIEM Issues

If logs are missing or not searchable:

* Investigate with available evidence
* Do not ignore the alert
* Inform L2 or SOC Engineer

---

# Good Reporting Checklist

Before closing or escalating an alert:

* Who is involved?
* What happened?
* When did it occur?
* Where did it happen?
* Why was the verdict chosen?
* Is escalation required?
* Are notes clear enough for another analyst?

---

# Quick Revision

### Reporting

```text
Document Findings
```

### Escalation

```text
Pass Alert To L2
```

### Communication

```text
Coordinate With Other Teams
```

### Five Ws

```text
Who
What
When
Where
Why
```

### Escalate If

```text
Major Incident
Remediation Needed
External Communication Needed
Need Help
```

### Critical Situation

```text
L2 → L3 → Manager
```

### Important Rule

```text
When unsure, escalate.
When you make a mistake, report it immediately.
```
