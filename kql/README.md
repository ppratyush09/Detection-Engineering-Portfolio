# 🔍 KQL Hunting Queries: Asking Logs Suspiciously Good Questions

> “Logs know things. KQL makes them confess.” 🕵️‍♂️📜

This folder contains my **KQL hunting queries** for detection engineering, threat hunting, and investigation workflows.

KQL, or **Kusto Query Language**, is used in Microsoft security platforms such as Microsoft Sentinel and Microsoft Defender to search, filter, summarize, and investigate large volumes of telemetry.

In simple words:

> Sigma says what suspicious behavior looks like.
> KQL goes into the log jungle and asks, “Alright, who did it?” 🌴🔦

---

## 🎯 Purpose of This Folder

This folder is used to store KQL queries created for:

* Threat hunting
* Detection validation
* Incident investigation
* Suspicious process analysis
* PowerShell behavior review
* Windows discovery activity
* Lateral movement investigation
* Pre-ransomware behavior hunting
* Account and privilege abuse checks
* Mapping detection ideas to Microsoft security telemetry

The goal is not just to write queries that “run.”

The goal is to write queries that are:

* Clear
* Explainable
* Useful
* Tunable
* Mapped to behavior
* Ready for investigation
* Easy for another analyst to understand

Because a query without context is just a digital noodle. 🍜

---

## 📁 Folder Structure

Current structure:

```text
kql/
├── README.md
└── windows/
    └── suspicious_powershell_encoded_command.kql
```

Planned structure:

```text
kql/
├── README.md
├── windows/
│   ├── process_creation/
│   ├── powershell/
│   ├── discovery/
│   ├── account_activity/
│   ├── lateral_movement/
│   └── ransomware_precursors/
│
├── defender/
│   ├── device_process_events/
│   ├── device_network_events/
│   ├── device_file_events/
│   └── device_logon_events/
│
└── sentinel/
    ├── security_event/
    ├── sysmon/
    └── hunting_queries/
```

Folder idea:

| Folder                   | Purpose                                          |
| ------------------------ | ------------------------------------------------ |
| `windows/`               | General Windows-focused hunting queries          |
| `defender/`              | Queries for Microsoft Defender tables            |
| `sentinel/`              | Queries for Microsoft Sentinel logs              |
| `process_creation/`      | Process execution behavior                       |
| `powershell/`            | PowerShell abuse and suspicious scripting        |
| `discovery/`             | Reconnaissance and enumeration activity          |
| `account_activity/`      | User creation, group changes, privilege activity |
| `lateral_movement/`      | Remote access, remote execution, admin shares    |
| `ransomware_precursors/` | Early behaviors before encryption                |

---

## 🧠 What KQL Helps Me Practice

KQL helps me learn how to think like a hunter.

Instead of only asking:

> “Did an alert fire?”

KQL helps ask better questions:

* Which process started this?
* Which parent process launched it?
* Which user ran it?
* Which machine did it happen on?
* Was this behavior rare?
* Did it happen across multiple hosts?
* Did it happen after a suspicious logon?
* Did discovery happen before lateral movement?
* Is this one command suspicious, or is the sequence suspicious?

This is where logs become storyboards. 🎬

---

## 🧪 Query Writing Style

Each KQL file should start with a comment block.

Example:

```kql
// Title: Suspicious PowerShell Encoded Command
// Author: PP
// Status: Experimental
// Purpose: Detect PowerShell execution using encoded command parameters.
// MITRE ATT&CK: T1059.001 - PowerShell
// Data Source: DeviceProcessEvents
// Related Sigma Rule: sigma/windows/process_creation/suspicious_powershell_encoded_command.yml
// Notes: Validate in lab before using in production-like environments.
```

A good KQL query should include:

| Section          | Why It Matters                              |
| ---------------- | ------------------------------------------- |
| Title            | Helps identify the purpose quickly          |
| Author           | Shows ownership                             |
| Status           | Experimental, test, stable, retired         |
| Purpose          | Explains what the query hunts               |
| Data Source      | Shows required telemetry                    |
| MITRE Mapping    | Connects behavior to ATT&CK                 |
| Query Logic      | The actual hunt                             |
| Projected Fields | Makes output useful                         |
| Comments         | Helps future me not become an archaeologist |

---

## 🧩 Query Naming Convention

Use lowercase filenames with underscores.

Recommended format:

```text
behavior_or_detection_name.kql
```

Examples:

```text
suspicious_powershell_encoded_command.kql
windows_discovery_commands.kql
new_local_admin_created.kql
suspicious_archive_creation.kql
possible_lateral_movement_logon.kql
shadow_copy_deletion_attempt.kql
```

Bad names:

```text
query1.kql
test-final-final-v2.kql
newquery.kql
powershellthing.kql
pleasework.kql
```

The last one is emotionally honest, but not portfolio-friendly. 😅

---

## 🔥 Current KQL Focus Areas

### 1. Suspicious PowerShell Activity ⚡

Goal:

Detect suspicious PowerShell behavior that may indicate script abuse, obfuscation, or execution of encoded commands.

Focus patterns:

* `-enc`
* `-EncodedCommand`
* `IEX`
* `Invoke-Expression`
* `DownloadString`
* `FromBase64String`
* PowerShell launched by Office apps
* PowerShell launched from unusual parent processes

Example investigation questions:

* Who ran PowerShell?
* What command line was used?
* What parent process launched it?
* Was it interactive or automated?
* Did it connect to the network?
* Did it write files?

---

### 2. Windows Discovery Behavior 🕵️

Goal:

Detect suspicious enumeration commands commonly used during reconnaissance.

Focus commands:

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
quser
tasklist
```

Detection thinking:

> One command may be normal.
> Many discovery commands in a short time may be the log equivalent of someone measuring the windows before a robbery. 🪟

---

### 3. Suspicious Account Activity 👤

Goal:

Hunt for account creation, privilege changes, and suspicious administrative modifications.

Focus areas:

* New local user creation
* Local administrators group modification
* Domain group changes
* Privileged user activity
* Account enabled after being disabled
* Unusual admin behavior

Investigation questions:

* Who created the account?
* Was the account added to a privileged group?
* Which machine did it happen on?
* Was there remote access afterward?
* Is the account expected?

---

### 4. Lateral Movement Clues 🚪

Goal:

Identify signs that activity moved from one system to another.

Focus areas:

* Remote logons
* Admin share usage
* Remote service creation
* Suspicious source-host to target-host patterns
* Unusual administrative tools
* RDP activity
* SMB activity

Investigation questions:

* Where did the connection originate?
* Which account was used?
* Was the source machine expected?
* Did process execution follow the logon?
* Was the target a critical server?

---

### 5. Pre-Ransomware Behavior 🧨

Goal:

Hunt for early-stage behavior that may happen before encryption.

Focus areas:

* Backup discovery
* Shadow copy deletion
* Mass file access
* Archive creation
* Suspicious compression tools
* Security tool tampering
* Remote access tool usage
* Discovery bursts

Detection idea:

> Catch the smoke before the toaster becomes a volcano. 🌋

---

## 🧾 Standard KQL Template

Use this format for new queries:

```kql
// Title: <Query Name>
// Author: PP
// Date: YYYY-MM-DD
// Status: Experimental
// Purpose: <What behavior this query hunts for>
// MITRE ATT&CK: <Technique ID and Name>
// Data Source: <Table Name>
// Related Rule: <Sigma/YARA/Suricata reference if applicable>
// Notes: <Validation or false-positive notes>

<TableName>
| where Timestamp > ago(7d)
| where <condition>
| project Timestamp, DeviceName, AccountName, FileName, ProcessCommandLine
| order by Timestamp desc
```

---

## 🧪 Example Query: Suspicious PowerShell Encoded Command

```kql
// Title: Suspicious PowerShell Encoded Command
// Author: PP
// Date: 2026-06-07
// Status: Experimental
// Purpose: Detect PowerShell execution using encoded command parameters.
// MITRE ATT&CK: T1059.001 - PowerShell
// Data Source: DeviceProcessEvents
// Related Sigma Rule: sigma/windows/process_creation/suspicious_powershell_encoded_command.yml
// Notes: Validate in lab and tune for administrative scripts.

DeviceProcessEvents
| where Timestamp > ago(7d)
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where ProcessCommandLine has_any ("-enc", "-EncodedCommand", "/enc")
| project
    Timestamp,
    DeviceName,
    AccountName,
    InitiatingProcessFileName,
    FileName,
    ProcessCommandLine,
    ReportId
| order by Timestamp desc
```

---

## 🧠 Query Quality Checklist

Before adding a KQL query to this folder, check:

* [ ] Does the query have a clear title?
* [ ] Does it mention the data source?
* [ ] Does it explain the purpose?
* [ ] Does it include useful output fields?
* [ ] Does it avoid unnecessary noise?
* [ ] Does it include MITRE ATT&CK mapping if possible?
* [ ] Does it mention false positives?
* [ ] Was it tested or marked experimental?
* [ ] Is the filename clear?
* [ ] Would another analyst understand it without telepathy?

Because “works on my machine” is not a detection strategy. 🧙‍♂️

---

## 🧯 Safety and Ethics

This folder must not contain:

* Company queries copied from work
* Client names
* Internal hostnames from real environments
* Private IP ranges from production
* Proprietary detection logic
* Sensitive investigation details
* Credentials
* API keys
* Real incident data

Allowed content:

* Lab-created queries
* Public-learning detections
* Personal research notes
* Sanitized examples
* Queries written from my own understanding
* Queries mapped to safe lab behavior

Golden rule:

> The repo should show skill, not spill secrets. 🔐

---

## 🔄 Relationship with Other Folders

KQL does not live alone. It has cousins.

| Folder      | Relationship                                                          |
| ----------- | --------------------------------------------------------------------- |
| `sigma/`    | Sigma rules may be translated into KQL logic                          |
| `reports/`  | Writeups explain the detection, validation, and investigation process |
| `tests/`    | Stores safe test notes and validation results                         |
| `python/`   | Helper scripts can parse logs or generate test data                   |
| `yara/`     | File detection findings can inspire hunting queries                   |
| `suricata/` | Network detections can be investigated further using KQL              |

Example workflow:

```text
Research behavior
        ↓
Write Sigma rule
        ↓
Write matching KQL query
        ↓
Generate safe lab activity
        ↓
Validate logs
        ↓
Document in reports/
```

---

## 🧭 Planned KQL Queries

| Query                                       | Purpose                                 | Status    |
| ------------------------------------------- | --------------------------------------- | --------- |
| `suspicious_powershell_encoded_command.kql` | Detect encoded PowerShell command usage | 🟡 Draft  |
| `windows_discovery_commands.kql`            | Hunt common discovery commands          | ⚪ Planned |
| `new_local_admin_created.kql`               | Detect suspicious local admin creation  | ⚪ Planned |
| `shadow_copy_deletion_attempt.kql`          | Hunt possible ransomware preparation    | ⚪ Planned |
| `suspicious_archive_creation.kql`           | Detect archive staging behavior         | ⚪ Planned |
| `possible_lateral_movement_logon.kql`       | Hunt remote logon patterns              | ⚪ Planned |
| `suspicious_parent_child_process.kql`       | Detect odd process relationships        | ⚪ Planned |
| `powershell_download_cradle.kql`            | Hunt download-and-execute behavior      | ⚪ Planned |

---

## 🧠 Investigation Fields I Care About

Useful fields commonly seen in Microsoft Defender style telemetry:

| Field                          | Why It Helps                   |
| ------------------------------ | ------------------------------ |
| `Timestamp`                    | When it happened               |
| `DeviceName`                   | Where it happened              |
| `AccountName`                  | Who did it                     |
| `FileName`                     | Process or file involved       |
| `FolderPath`                   | File location                  |
| `ProcessCommandLine`           | Command details                |
| `InitiatingProcessFileName`    | Parent process                 |
| `InitiatingProcessCommandLine` | Parent process command         |
| `RemoteUrl`                    | Network destination            |
| `RemoteIP`                     | Remote address                 |
| `ActionType`                   | Event/action category          |
| `ReportId`                     | Event tracking and correlation |

Good fields make investigations easier.
Bad field selection makes analysts squint at the screen like confused owls. 🦉

---

## 🏁 Final Note

This KQL folder is where hunting ideas become searchable logic.

The mission is not to create fancy queries for decoration.

The mission is to ask better questions from telemetry:

> What happened?
> Who did it?
> Where did it happen?
> Is it normal?
> What happened next?
> Can I turn this into a better detection?

Every query here should help move from noise to signal.

And when the logs start mumbling, KQL brings the flashlight. 🔦

