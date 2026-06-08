# 🛡️ Phase 03: Sigma and KQL

> “Phase 02 taught Windows to speak. Phase 03 teaches me to turn that chatter into detections.” 🪟📜➡️🚨

This phase focuses on writing **Sigma rules** and matching **KQL hunting queries** using telemetry learned in Phase 02.

Phase 01 built the lab.
Phase 02 focused on Windows telemetry.
Phase 03 turns that telemetry into structured detection logic.

The goal is simple:

> Understand behavior.
> Find the right telemetry.
> Write Sigma.
> Write KQL.
> Validate in the lab.
> Document the result.
> Reduce noise before the alert owl gets dramatic. 🦉

---

## 🎯 Phase Objective

The objective of Phase 03 is to practice writing detection logic using:

* Sigma rules
* KQL hunting queries
* Windows process creation telemetry
* PowerShell logs
* Authentication events
* Account management events
* Sysmon events
* Lab-generated behavior
* False-positive notes
* Detection writeups

This phase is considered successful when I can take one suspicious behavior and produce:

| Output              | Purpose                                                        |
| ------------------- | -------------------------------------------------------------- |
| Sigma rule          | Platform-agnostic detection logic                              |
| KQL query           | Microsoft-focused hunting or detection query                   |
| Validation note     | Proof that the logic was tested or clearly marked experimental |
| False-positive note | Expected legitimate activity                                   |
| Detection writeup   | Clear explanation of what, why, how, and next steps            |

Tiny detection law:

> A rule without validation is a hopeful spell.
> A rule with testing becomes engineering. 🧪

---

## 🧭 Phase Scope

This phase focuses on **beginner to intermediate detection writing**.

Included in this phase:

* Sigma rule structure
* KQL query structure
* Logsource selection
* Data source mapping
* Process creation detections
* PowerShell detections
* Windows discovery detections
* Account activity detections
* Basic lateral movement clues
* Pre-ransomware behavior ideas
* False-positive documentation
* MITRE ATT&CK mapping
* Lab validation notes

Not included yet:

* Full CI/CD rule validation
* Advanced Sigma pipelines
* Large-scale SIEM deployment
* Production tuning
* Complex correlation rules
* Real incident data
* Company detections
* Proprietary logic

Those come later.

This phase is about learning the craft.

Not pretending every rule is production-grade thunder magic. ⚡

---

## 🧠 Why Sigma and KQL Matter

Sigma and KQL are two important parts of detection engineering.

### Sigma

Sigma helps describe suspicious behavior in a generic rule format.

It answers:

> What behavior should be detected?

Example:

```text
PowerShell launched with encoded command parameters.
```

### KQL

KQL helps search Microsoft telemetry and hunt for that behavior.

It answers:

> Where did this behavior happen in the logs?

Example:

```text
Search DeviceProcessEvents for powershell.exe with -EncodedCommand.
```

Together:

```text
Sigma = Detection idea in reusable format
KQL = Query that hunts through Microsoft telemetry
```

Sigma is the blueprint.
KQL is the flashlight. 🔦

---

## 🏗️ Planned Phase 03 Files

This phase will contain notes and practical detection work.

```text
phase-03-sigma-and-kql/
├── README.md
├── sigma-basics.md
├── kql-basics.md
├── logsource-selection.md
├── detection-rule-template.md
├── query-template.md
├── rule-validation-notes.md
├── false-positive-notes.md
├── behavior-to-detection-map.md
└── phase-03-completion-summary.md
```

| File                             | Purpose                                             |
| -------------------------------- | --------------------------------------------------- |
| `README.md`                      | Overview of Phase 03                                |
| `sigma-basics.md`                | Notes on Sigma structure and components             |
| `kql-basics.md`                  | Notes on KQL query structure and operators          |
| `logsource-selection.md`         | How to choose correct Sigma logsource and telemetry |
| `detection-rule-template.md`     | Standard Sigma rule template                        |
| `query-template.md`              | Standard KQL query template                         |
| `rule-validation-notes.md`       | How rules were tested in the lab                    |
| `false-positive-notes.md`        | Expected legitimate triggers and tuning ideas       |
| `behavior-to-detection-map.md`   | Mapping suspicious behavior to Sigma and KQL        |
| `phase-03-completion-summary.md` | Summary before moving to YARA and Malware Analysis  |

---

## 📁 Related Repository Folders

Phase 03 connects strongly with these main repository folders:

| Folder                                       | Purpose                                      |
| -------------------------------------------- | -------------------------------------------- |
| `sigma/`                                     | Final Sigma rules                            |
| `kql/`                                       | Final KQL queries                            |
| `reports/`                                   | Detection writeups                           |
| `tests/`                                     | Safe validation notes and sample event notes |
| `docs/`                                      | Lab and telemetry documentation              |
| `learning-notes/phase-02-windows-telemetry/` | Telemetry knowledge used for rules           |

Expected workflow:

```text
learning-notes/phase-03-sigma-and-kql/
        ↓
sigma/
        ↓
kql/
        ↓
reports/
        ↓
tests/
```

Learning notes explain the journey.
Rule folders contain the artifacts.
Reports explain the investigation value.

That is the tidy detection sandwich. 🥪

---

## 🧾 Sigma Rule Basics

A Sigma rule usually includes:

| Section          | Purpose                            |
| ---------------- | ---------------------------------- |
| `title`          | Clear rule name                    |
| `id`             | Unique rule ID                     |
| `status`         | Rule maturity                      |
| `description`    | What the rule detects              |
| `author`         | Rule creator                       |
| `date`           | Creation date                      |
| `references`     | Public research or technique links |
| `tags`           | ATT&CK mapping or classification   |
| `logsource`      | Required telemetry source          |
| `detection`      | Matching logic                     |
| `fields`         | Useful fields for investigation    |
| `falsepositives` | Expected legitimate triggers       |
| `level`          | Severity                           |

Basic Sigma thinking:

```text
Behavior
   ↓
Log source
   ↓
Fields
   ↓
Selections
   ↓
Condition
   ↓
False positives
   ↓
Severity
```

Sigma is not just YAML.

It is detection thinking written in YAML clothing. 👔

---

## 🛡️ Standard Sigma Template

```yaml
title: <Clear Detection Title>
id: <UUID>
status: experimental
description: <What suspicious behavior this rule detects.>
author: PP
date: YYYY-MM-DD
references:
  - <Public reference or MITRE ATT&CK link>
tags:
  - attack.<tactic>
  - attack.<technique_id>
logsource:
  product: windows
  category: process_creation
detection:
  selection:
    CommandLine|contains:
      - '<suspicious value>'
  condition: selection
fields:
  - Image
  - CommandLine
  - ParentImage
  - User
  - ComputerName
falsepositives:
  - <Expected legitimate activity>
level: medium
```

Default status for new rules:

```yaml
status: experimental
```

Why?

Because honesty is better than pretending a new rule has been blessed by seven SIEM wizards. 🧙

---

## 🔍 KQL Query Basics

KQL is used to hunt through Microsoft security telemetry.

Important KQL skills:

* `where`
* `project`
* `extend`
* `summarize`
* `order by`
* `join`
* `has`
* `contains`
* `in`
* `ago()`
* `bin()`
* `count()`

A basic KQL query should answer:

* What table am I searching?
* What time range am I using?
* What condition am I looking for?
* Which fields do I want to show?
* How should results be sorted?
* What is the investigation purpose?

KQL is where logs get questioned under a desk lamp. 💡

---

## 🔦 Standard KQL Template

```kql
// Title: <Query Title>
// Author: PP
// Date: YYYY-MM-DD
// Status: Experimental
// Purpose: <What behavior this query hunts for>
// MITRE ATT&CK: <Technique ID and Name>
// Data Source: <Table Name>
// Related Sigma Rule: <Path if applicable>
// Notes: <Validation and false-positive notes>

<TableName>
| where Timestamp > ago(7d)
| where <condition>
| project Timestamp, DeviceName, AccountName, FileName, ProcessCommandLine
| order by Timestamp desc
```

Example table names may include:

```text
DeviceProcessEvents
DeviceNetworkEvents
DeviceFileEvents
DeviceLogonEvents
SecurityEvent
Sysmon
```

Actual table availability depends on the platform and log source.

No table, no query feast. 🍽️

---

## 🎯 Initial Detection Use Cases

Phase 03 should start with practical Windows detections.

### 1. Suspicious PowerShell Encoded Command ⚡

Behavior:

```text
PowerShell launched with encoded command parameters.
```

Detection value:

* Common suspicious pattern
* Good beginner process creation detection
* Easy to map to Sigma and KQL
* Useful for understanding command-line fields

Possible indicators:

```text
-enc
-EncodedCommand
/enc
```

Expected artifacts:

```text
sigma/windows/process_creation/suspicious_powershell_encoded_command.yml
kql/windows/suspicious_powershell_encoded_command.kql
reports/suspicious_powershell_encoded_command.md
```

---

### 2. Windows Discovery Commands 🕵️

Behavior:

```text
A user or process runs multiple discovery commands.
```

Commands to watch:

```text
whoami
hostname
ipconfig
systeminfo
net user
net group
net localgroup
net view
nltest
tasklist
quser
```

Detection idea:

> One command may be normal.
> A burst of discovery commands may be the endpoint equivalent of someone measuring the windows. 🪟

Expected artifacts:

```text
sigma/windows/process_creation/suspicious_windows_discovery_commands.yml
kql/windows/discovery/windows_discovery_commands.kql
reports/windows_discovery_commands.md
```

---

### 3. New Local User Created 👤

Behavior:

```text
A new local user account is created.
```

Detection value:

* Useful for persistence detection
* Common post-compromise activity
* Good account management use case

Possible Windows event:

```text
4720
```

Detection questions:

* Who created the account?
* On which host?
* Was the account added to administrators?
* Was there remote access afterward?
* Is the account expected?

Expected artifacts:

```text
sigma/windows/account_activity/new_local_user_created.yml
kql/windows/account_activity/new_local_user_created.kql
reports/new_local_user_created.md
```

---

### 4. Local Admin Group Modified 👑

Behavior:

```text
A user is added to the local Administrators group.
```

Detection value:

* Privilege escalation clue
* Persistence clue
* High investigation value

Possible Windows event:

```text
4732
```

Detection questions:

* Which account was added?
* Who added it?
* Was this expected?
* Was it followed by RDP or remote access?
* Did it happen on a critical system?

---

### 5. Shadow Copy Deletion Attempt 🧨

Behavior:

```text
A command attempts to delete shadow copies.
```

Example commands:

```text
vssadmin delete shadows
wmic shadowcopy delete
wbadmin delete catalog
bcdedit /set
```

Detection value:

* Possible ransomware preparation
* High-value pre-encryption clue
* Useful for process command-line detection

Detection thought:

> If shadow copies start disappearing, the incident has already put on tap shoes. Better alert early. 🕺

---

## 🛰️ Logsource Selection Notes

Choosing the correct Sigma logsource is critical.

Common examples:

### Windows Process Creation

```yaml
logsource:
  product: windows
  category: process_creation
```

Useful for:

* PowerShell execution
* Discovery commands
* LOLBins
* Suspicious parent-child processes
* Ransomware precursor commands

### Windows Security

```yaml
logsource:
  product: windows
  service: security
```

Useful for:

* Logons
* Account creation
* Group changes
* Privilege events

### PowerShell

```yaml
logsource:
  product: windows
  category: ps_script
```

Useful for:

* Script block logging
* Suspicious PowerShell content
* Obfuscation
* Download cradles

### Sysmon

```yaml
logsource:
  product: windows
  service: sysmon
```

Useful for:

* Process creation
* Network connections
* Registry events
* File creation
* DNS queries

Rule goblin warning:

> Wrong logsource means the rule may look pretty but hunt in the wrong forest. 🌲

---

## 🧪 Validation Approach

Each detection should be validated when possible.

Validation flow:

```text
Pick suspicious behavior
        ↓
Generate safe lab activity
        ↓
Confirm event/log exists
        ↓
Write Sigma rule
        ↓
Write matching KQL query
        ↓
Check whether logic matches expected telemetry
        ↓
Document false positives
        ↓
Write detection report
```

Validation result labels:

| Status         | Meaning                          |
| -------------- | -------------------------------- |
| Draft          | Written but not tested           |
| Lab Tested     | Tested in home lab               |
| Needs Tuning   | Works but too noisy              |
| Improved       | Updated after review             |
| Stable for Lab | Good enough for repeated lab use |

Important:

> If not tested yet, mark it clearly as experimental.

That is not a weakness.

That is professional honesty with a tiny clipboard. 📋

---

## 🧾 Rule Validation Note Template

```markdown
# Rule Validation: <Detection Name>

## Detection

- Sigma: `<path>`
- KQL: `<path>`

## Behavior Tested

What behavior was generated?

## Lab Systems Used

| System | Role |
|---|---|
| WINCLIENT01 | Endpoint |
| DC01 | Domain Controller |

## Expected Telemetry

Which log source or event ID should capture it?

## Observed Telemetry

What was actually seen?

## Result

- [ ] Matched expected behavior
- [ ] Needs tuning
- [ ] Did not match
- [ ] Not tested yet

## False Positives

What legitimate activity may trigger this?

## Lessons Learned

What did this test teach?
```

---

## 🧯 False Positive Thinking

False positives are not embarrassment.

They are feedback.

Common false-positive sources:

* Admin scripts
* Software deployment tools
* Monitoring tools
* Security tools
* Helpdesk activity
* Developer scripts
* Scheduled tasks
* Backup tools
* IT automation
* Normal PowerShell usage

Good detection questions:

* Is this behavior rare?
* Is the user expected?
* Is the parent process expected?
* Is the host expected?
* Did this happen with other suspicious activity?
* Is this a single event or part of a chain?
* Can a filter reduce noise safely?

Detection goal:

```text
Not zero alerts.
Not maximum alerts.
Useful alerts.
```

Alert quality matters.

Nobody wants a SIEM that screams whenever a spreadsheet breathes. 📣

---

## 📚 MITRE ATT&CK Mapping

Where possible, detections should map to MITRE ATT&CK.

Examples:

| Behavior                     | Technique |
| ---------------------------- | --------- |
| PowerShell execution         | T1059.001 |
| System information discovery | T1082     |
| Account discovery            | T1087     |
| Domain trust discovery       | T1482     |
| Create account               | T1136     |
| Account added to group       | T1098     |
| Service creation             | T1543.003 |
| Shadow copy deletion         | T1490     |

MITRE mapping helps explain:

* Tactic
* Technique
* Attacker objective
* Detection relevance
* Investigation priority

But mapping should be accurate.

Do not throw ATT&CK IDs like glitter at a birthday party. 🎉

---

## 🧠 Behavior-to-Detection Thinking

This is the main mental model of Phase 03.

```text
Suspicious Behavior
        ↓
Required Telemetry
        ↓
Relevant Fields
        ↓
Sigma Rule
        ↓
KQL Query
        ↓
Validation
        ↓
False Positive Notes
        ↓
Report
```

Example:

| Behavior                | Telemetry           | Sigma                          | KQL                             |
| ----------------------- | ------------------- | ------------------------------ | ------------------------------- |
| Encoded PowerShell      | Process creation    | Match Image and CommandLine    | Query DeviceProcessEvents       |
| Discovery command burst | Process creation    | Match known discovery commands | Summarize commands by host/user |
| New user created        | Security Event 4720 | Match account creation event   | Query SecurityEvent             |
| Admin group modified    | Security Event 4732 | Match group membership change  | Query SecurityEvent             |
| Shadow copy deletion    | Process creation    | Match vssadmin/wmic commands   | Query process command line      |

This is where the craft lives.

Not in memorizing syntax.

In understanding the chain from behavior to evidence. 🔗

---

## 🧰 Tools and Systems Used

| Tool / System  | Use in Phase 03                               |
| -------------- | --------------------------------------------- |
| WINCLIENT01    | Generate endpoint behavior                    |
| ADMIN01        | Generate admin behavior and false positives   |
| DC01           | Generate authentication and account telemetry |
| Event Viewer   | Review Windows logs                           |
| Sysmon         | Future richer endpoint visibility             |
| Sigma          | Write detection rules                         |
| KQL            | Write hunting queries                         |
| GitHub         | Store rules and notes                         |
| Reports folder | Document detections                           |

Optional later:

* Microsoft Defender tables
* Microsoft Sentinel
* Sigma conversion tools
* YAML validators
* GitHub Actions

But first:

> Write understandable rules before building robot pipelines. 🤖

---

## 🔐 Safety Rules

This phase must not include:

* Company detections
* Client logs
* Proprietary queries
* Work screenshots
* Private incident data
* Credentials
* API keys
* Real hostnames from work
* Internal IPs from production
* Malware samples

Allowed:

* Lab-generated detections
* Safe test commands
* Public ATT&CK references
* Sanitized notes
* Personal Sigma rules
* Personal KQL queries
* Dummy indicators
* Lab VM names

Golden rule:

> Show detection skill, not sensitive evidence. 🔐

---

## ✅ Phase 03 Checklist

| Task                                         | Status |
| -------------------------------------------- | ------ |
| Sigma basics documented                      | ⏳      |
| KQL basics documented                        | ⏳      |
| Logsource selection notes created            | ⏳      |
| Standard Sigma template created              | ⏳      |
| Standard KQL template created                | ⏳      |
| First Sigma rule drafted                     | ⏳      |
| First KQL query drafted                      | ⏳      |
| PowerShell encoded command detection started | ⏳      |
| Windows discovery detection started          | ⏳      |
| Account activity detection planned           | ⏳      |
| False-positive notes started                 | ⏳      |
| Validation notes started                     | ⏳      |
| Detection writeup created                    | ⏳      |
| No sensitive data included                   | ✅      |

---

## 🚀 Next Phase

After Phase 03, the next phase should be:

```text
Phase 04: YARA and Malware Analysis
```

Phase 04 will focus on:

* Safe malware-analysis methodology
* Static analysis basics
* Dynamic analysis checklist
* FLARE usage
* REMnux usage
* Suspicious strings
* IOC extraction
* YARA rule writing
* Behavior-to-detection mapping

Phase 03 detects behavior from logs.

Phase 04 starts asking files why they look so suspicious. 🧬

---

## 🏁 Final Note

Phase 03 is where detection engineering becomes real.

This phase is not about writing hundreds of rules.

It is about writing a few good ones properly.

A good detection should answer:

* What behavior is suspicious?
* What telemetry is required?
* What fields matter?
* What rule detects it?
* What query hunts it?
* What false positives exist?
* Was it tested?
* How should an analyst investigate?

That is the difference between a random rule and a useful detection.

The YAML may be small.

The thinking should not be. 🧠🛡️

