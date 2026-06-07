# 🛡️ Sigma Rules: Writing Alerts Before the Fire Alarm Starts Screaming

> “Suspicious behavior enters. Detection logic judges. Analysts investigate.” 🕵️‍♂️🚨

This folder contains my **Sigma detection rules** for Windows, endpoint behavior, discovery activity, suspicious process execution, pre-ransomware behavior, and other detection engineering use cases.

Sigma is a generic detection rule format. It helps describe suspicious behavior in a structured way so that the same logic can later be converted into platform-specific queries such as Splunk SPL, Microsoft Sentinel KQL, Elastic queries, and other SIEM formats.

In simple words:

> Sigma is the recipe.
> SIEM queries are the cooked dish.
> False positives are the unexpected raisins. 🍪

---

## 🎯 Purpose of This Folder

This folder is used to store Sigma rules created for:

* Windows behavior detection
* Process creation monitoring
* PowerShell abuse detection
* Suspicious command-line activity
* Discovery and enumeration behavior
* Account creation and privilege changes
* Lateral movement clues
* Pre-ransomware activity
* Malware-related behavior patterns
* Lab-based validation and documentation

The goal is not only to write rules that look fancy.

The goal is to write rules that are:

* Clear
* Testable
* Explainable
* Mapped to telemetry
* Mapped to MITRE ATT&CK where possible
* Honest about false positives
* Useful for investigation
* Easy to convert into SIEM logic later

Because a detection rule without context is just YAML wearing sunglasses. 😎

---

## 📁 Folder Structure

Current structure:

```text
sigma/
├── README.md
└── windows/
    └── process_creation/
        └── suspicious_powershell_encoded_command.yml
```

Planned structure:

```text
sigma/
├── README.md
└── windows/
    ├── process_creation/
    │   ├── suspicious_powershell_encoded_command.yml
    │   ├── suspicious_windows_discovery_commands.yml
    │   ├── suspicious_archive_creation.yml
    │   └── shadow_copy_deletion_attempt.yml
    │
    ├── powershell/
    │   ├── powershell_download_cradle.yml
    │   ├── powershell_obfuscation_keywords.yml
    │   └── powershell_suspicious_parent.yml
    │
    ├── account_activity/
    │   ├── new_local_user_created.yml
    │   ├── local_admin_group_modified.yml
    │   └── disabled_account_enabled.yml
    │
    ├── lateral_movement/
    │   ├── remote_service_creation.yml
    │   ├── suspicious_rdp_logon.yml
    │   └── admin_share_access.yml
    │
    └── ransomware_precursors/
        ├── vssadmin_shadowcopy_deletion.yml
        ├── backup_discovery_commands.yml
        └── mass_archive_staging.yml
```

Folder purpose:

| Folder                           | Purpose                                                       |
| -------------------------------- | ------------------------------------------------------------- |
| `windows/process_creation/`      | Rules based on process execution and command-line behavior    |
| `windows/powershell/`            | PowerShell abuse, obfuscation, and suspicious script activity |
| `windows/account_activity/`      | User creation, group changes, privilege modifications         |
| `windows/lateral_movement/`      | Remote execution, remote logons, admin shares, movement clues |
| `windows/ransomware_precursors/` | Early warning behaviors before encryption                     |

---

## 🧠 Why Sigma Matters

Sigma helps me practice the core skill of detection engineering:

> Turning suspicious behavior into structured detection logic.

A good Sigma rule is more than a file.

It should explain:

* What behavior is suspicious
* Which logs are needed
* Which fields matter
* Which conditions trigger the detection
* What false positives may happen
* How severe the behavior is
* Which MITRE ATT&CK technique it maps to
* How an analyst can investigate the result

Sigma is where detection thinking gets organized.

No chaos soup.

No “query1-final-v3-please-work.yml.”

Just clean logic, clear metadata, and a tiny alert owl waiting to scream at the correct moment. 🦉

---

## 🧩 Basic Sigma Rule Anatomy

A Sigma rule usually has these important sections:

| Section          | Purpose                                                         |
| ---------------- | --------------------------------------------------------------- |
| `title`          | Human-readable rule name                                        |
| `id`             | Unique rule identifier, usually a UUID                          |
| `status`         | Rule maturity such as experimental, test, stable, or deprecated |
| `description`    | What the rule detects                                           |
| `author`         | Rule creator                                                    |
| `date`           | Creation date                                                   |
| `modified`       | Last update date, when applicable                               |
| `references`     | Links to research, ATT&CK, reports, or documentation            |
| `tags`           | ATT&CK mappings or category labels                              |
| `logsource`      | Required log source, product, category, or service              |
| `detection`      | The actual matching logic                                       |
| `fields`         | Useful fields to show in results                                |
| `falsepositives` | Expected legitimate activity that may trigger the rule          |
| `level`          | Severity such as low, medium, high, or critical                 |

A Sigma rule without metadata is like a suspicious suitcase at an airport with no tag.

Technically interesting.

Operationally stressful. 🧳

---

## 🧾 Standard Sigma Template

Use this template for new rules:

```yaml
title: <Clear Rule Title>
id: <UUID>
status: experimental
description: <What suspicious behavior this rule detects.>
author: PP
date: YYYY-MM-DD
modified: YYYY-MM-DD
references:
  - <Public reference or MITRE link>
tags:
  - attack.<tactic>
  - attack.<technique_id>
logsource:
  product: windows
  category: process_creation
detection:
  selection:
    <FieldName>|contains:
      - <value>
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

---

## 🔥 Example Rule: Suspicious PowerShell Encoded Command

```yaml
title: Suspicious PowerShell Encoded Command
id: 11111111-1111-1111-1111-111111111111
status: experimental
description: Detects PowerShell execution using encoded command parameters commonly observed in suspicious or malicious activity.
author: PP
date: 2026-06-07
references:
  - https://attack.mitre.org/techniques/T1059/001/
tags:
  - attack.execution
  - attack.t1059.001
logsource:
  product: windows
  category: process_creation
detection:
  selection_img:
    Image|endswith:
      - '\powershell.exe'
      - '\pwsh.exe'
  selection_cmd:
    CommandLine|contains:
      - '-enc'
      - '-EncodedCommand'
      - '/enc'
  condition: selection_img and selection_cmd
fields:
  - Image
  - CommandLine
  - ParentImage
  - User
  - ComputerName
falsepositives:
  - Administrative scripts
  - Software deployment tools
  - Security automation
level: medium
```

---

## 🛰️ Logsource Notes

The `logsource` section tells Sigma what kind of telemetry the rule needs.

Common examples:

### Windows Process Creation

```yaml
logsource:
  product: windows
  category: process_creation
```

Useful for detecting:

* PowerShell execution
* LOLBins
* Discovery commands
* Suspicious command lines
* Parent-child process relationships

This is one of the most useful starting points for detection engineering. Process logs are little behavior cameras. 📸

---

### Windows PowerShell

```yaml
logsource:
  product: windows
  category: ps_script
```

Useful for detecting:

* Suspicious script blocks
* Encoded commands
* Obfuscation
* Download cradles
* In-memory execution patterns

PowerShell logs can be noisy, but they are also full of useful crumbs. Suspicious crumbs. Cyber breadcrumbs. 🍞

---

### Windows Security Events

```yaml
logsource:
  product: windows
  service: security
```

Useful for detecting:

* Logons
* Account creation
* Group membership changes
* Privilege usage
* Authentication events

Identity telemetry is where many investigations start whispering, “Something is off.” 👤

---

### Sysmon

```yaml
logsource:
  product: windows
  category: process_creation
```

or sometimes:

```yaml
logsource:
  product: windows
  service: sysmon
```

Useful for:

* Process creation
* Network connections
* Registry changes
* File creation
* Image loads
* More detailed endpoint visibility

Sysmon is like Windows Event Logs after drinking an espresso. ☕

---

## 🔎 Detection Logic Style

Sigma detection logic usually has:

* One or more selections
* Optional filters
* A condition

Example:

```yaml
detection:
  selection:
    CommandLine|contains:
      - 'vssadmin delete shadows'
      - 'wmic shadowcopy delete'
  condition: selection
```

A more mature rule may include filters:

```yaml
detection:
  selection:
    CommandLine|contains:
      - 'vssadmin delete shadows'
  filter_admin_script:
    ParentImage|endswith:
      - '\trusted_admin_tool.exe'
  condition: selection and not filter_admin_script
```

Detection thinking:

> Selection catches the behavior.
> Filters reduce noise.
> The condition decides who enters the alert party. 🎉

---

## 🧠 Field Selection Tips

Useful fields for Sigma rules:

| Field                 | Why It Helps             |
| --------------------- | ------------------------ |
| `Image`               | Process executable path  |
| `CommandLine`         | Full command details     |
| `ParentImage`         | Parent process           |
| `ParentCommandLine`   | Parent command details   |
| `User`                | Account context          |
| `ComputerName`        | Host involved            |
| `CurrentDirectory`    | Execution location       |
| `Hashes`              | File hash information    |
| `TargetFilename`      | File path involved       |
| `DestinationIp`       | Network destination      |
| `DestinationHostname` | Remote host              |
| `EventID`             | Windows event identifier |

Fields are investigation handles.

Without useful fields, analysts have to wrestle the alert like a slippery fish. 🐟

---

## 🎯 Current Detection Focus Areas

### 1. Suspicious PowerShell Activity ⚡

Focus:

* Encoded commands
* Obfuscation
* Download cradles
* Suspicious parent processes
* PowerShell launched from unusual paths
* PowerShell used by unexpected users

Example suspicious patterns:

```text
-enc
-EncodedCommand
Invoke-Expression
IEX
DownloadString
FromBase64String
```

Expected rule types:

* Sigma
* Matching KQL
* Detection writeup
* Validation note

---

### 2. Windows Discovery Commands 🕵️

Focus:

* User discovery
* Group discovery
* System discovery
* Network discovery
* Domain trust discovery

Example commands:

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

Detection idea:

> One discovery command may be normal.
> Ten discovery commands in two minutes may be a suspicious little parade. 🥁

---

### 3. Suspicious Account Activity 👤

Focus:

* Local user creation
* Local admin group modification
* Domain group modification
* Disabled account re-enabled
* New account followed by remote access

Example behaviors:

```text
net user <name> <password> /add
net localgroup administrators <name> /add
```

Detection idea:

> New accounts are not always bad.
> New accounts appearing during suspicious activity deserve a flashlight and a clipboard. 🔦

---

### 4. Lateral Movement Clues 🚪

Focus:

* Remote service creation
* RDP logons
* Admin share access
* Remote command execution
* Unusual source-to-target authentication
* Tools used from unexpected systems

Detection idea:

> Lateral movement is not just one event.
> It is a trail of tiny footprints across machines. 👣

---

### 5. Pre-Ransomware Behavior 🧨

Focus:

* Shadow copy deletion
* Backup discovery
* Mass archive creation
* Security tool tampering
* Large file access
* Remote access tool usage
* Discovery followed by staging

Detection idea:

> Detect the preparation before the encryption party starts. Nobody invited the ransomware DJ. 🎧

---

### 6. Malware-Related Behavior 🧬

Focus:

* Suspicious script execution
* Dropped files
* Strange command lines
* LOLBin usage
* Persistence attempts
* Network beacon hints

Related VMs:

* FLARE VM
* REMnux VM
* Windows Client
* Admin Workstation

Sigma can detect behavior.
YARA can detect file patterns.
Together, they make a nice little detection sandwich. 🥪

---

## 📌 Rule Status Guidelines

Use honest status labels.

| Status         | Meaning                                |
| -------------- | -------------------------------------- |
| `experimental` | Early rule, needs testing and tuning   |
| `test`         | Used for lab validation                |
| `stable`       | Tested and reasonably reliable         |
| `deprecated`   | Old rule, replaced or no longer useful |

Most rules in this repository should start as:

```yaml
status: experimental
```

That is not weakness.

That is honesty with a YAML hat. 🎩

---

## 🚦 Severity Level Guidelines

| Level      | Meaning                                 |
| ---------- | --------------------------------------- |
| `low`      | Interesting but usually not urgent      |
| `medium`   | Suspicious and worth investigation      |
| `high`     | Strong suspicious signal                |
| `critical` | Very high confidence or severe activity |

Beginner note:

Do not mark everything as `critical`.

If every alert is a dragon, analysts stop bringing swords. 🐉

---

## ✅ Sigma Rule Quality Checklist

Before adding a rule, check:

* [ ] Does the rule have a clear title?
* [ ] Does it have a unique ID?
* [ ] Is the status honest?
* [ ] Is the description useful?
* [ ] Is the logsource correct?
* [ ] Does the detection logic match the behavior?
* [ ] Are important fields included?
* [ ] Are false positives documented?
* [ ] Is the severity reasonable?
* [ ] Is MITRE ATT&CK mapping included if possible?
* [ ] Is the filename clear?
* [ ] Can another analyst understand it without mind reading?
* [ ] Has it been tested or clearly marked as experimental?

Because “it looks suspicious to me” is not a complete detection strategy. 🧃

---

## 🧪 Validation Approach

Each rule should eventually be validated in the lab.

Validation flow:

```text
Pick behavior
    ↓
Generate safe lab activity
    ↓
Collect relevant logs
    ↓
Check if Sigma logic matches
    ↓
Convert or compare with KQL if needed
    ↓
Review false positives
    ↓
Document results
```

A rule is stronger when I can say:

> “I tested this behavior in my lab, observed the telemetry, and documented what happened.”

That is detection engineering with receipts. 🧾

---

## 🧯 False Positive Thinking

False positives are not failures.

They are signals that the rule needs context.

Common false positive sources:

* Admin scripts
* Software deployment tools
* Security tools
* Backup software
* IT automation
* Monitoring agents
* Developer activity
* Scheduled tasks
* Helpdesk troubleshooting

The goal is not zero false positives forever.

The goal is:

> Useful signal, manageable noise, clear investigation path.

Or, in tiny alert owl language:

> Hoot only when it matters. 🦉

---

## 🔄 Relationship with Other Folders

Sigma connects to the rest of the repository.

| Folder      | Relationship                                                                    |
| ----------- | ------------------------------------------------------------------------------- |
| `kql/`      | Sigma logic can be translated into KQL queries                                  |
| `reports/`  | Writeups explain the rule, validation, false positives, and investigation steps |
| `tests/`    | Safe validation notes and test data references                                  |
| `python/`   | Scripts can validate metadata or parse logs                                     |
| `yara/`     | File-based detection can support behavior-based Sigma detections                |
| `suricata/` | Network behavior can complement endpoint Sigma rules                            |
| `docs/`     | Lab architecture and learning notes explain the environment                     |

Example workflow:

```text
Research attacker behavior
        ↓
Write Sigma rule
        ↓
Write matching KQL query
        ↓
Generate lab activity
        ↓
Validate telemetry
        ↓
Document in reports/
        ↓
Improve rule
```

---

## 🗺️ Planned Sigma Rules

| Rule                                        | Purpose                                | Status    |
| ------------------------------------------- | -------------------------------------- | --------- |
| `suspicious_powershell_encoded_command.yml` | Detect encoded PowerShell execution    | 🟡 Draft  |
| `suspicious_windows_discovery_commands.yml` | Detect common discovery command bursts | ⚪ Planned |
| `new_local_user_created.yml`                | Detect new local user creation         | ⚪ Planned |
| `local_admin_group_modified.yml`            | Detect local admin group changes       | ⚪ Planned |
| `shadow_copy_deletion_attempt.yml`          | Detect possible ransomware preparation | ⚪ Planned |
| `suspicious_archive_creation.yml`           | Detect possible staging or collection  | ⚪ Planned |
| `remote_service_creation.yml`               | Detect possible remote execution       | ⚪ Planned |
| `powershell_download_cradle.yml`            | Detect PowerShell download behavior    | ⚪ Planned |
| `suspicious_parent_child_process.yml`       | Detect odd process relationships       | ⚪ Planned |
| `backup_discovery_commands.yml`             | Detect backup-related discovery        | ⚪ Planned |

---

## 🔐 Safety and Ethics

This folder must not contain:

* Company-owned rules copied from work
* Client-specific detections
* Proprietary logic
* Private environment details
* Real incident data
* Internal hostnames
* Credentials
* API keys
* Confidential logs
* Sensitive screenshots

Allowed content:

* Lab-created rules
* Public-learning detections
* Personal research
* Safe examples
* Rules written from my own understanding
* Rules mapped to public techniques and lab behavior

Golden rule:

> Show skill, not secrets. 🔐

---

## 🧠 Personal Sigma Notes

Things to remember:

* Start simple.
* Test before trusting.
* Metadata matters.
* Logsource matters a lot.
* False positives are part of the job.
* Good descriptions save time.
* MITRE mapping adds context.
* Matching KQL helps validation.
* Behavior beats random IOC matching.
* Good detection logic should explain itself.
* A clean rule is better than a clever mess.

Also:

> YAML indentation is tiny furniture.
> Move it wrong and the whole room collapses. 🪑

---

## 🏁 Final Note

This Sigma folder is where behavior becomes detection logic.

The mission is not to create a pile of random YAML files.

The mission is to build clear, tested, explainable rules that answer:

* What happened?
* Why is it suspicious?
* What logs are needed?
* What fields matter?
* What false positives may occur?
* How should an analyst investigate?
* How can this be improved?

Every rule should help move from noise to signal.

Every detection should be useful.

Every alert owl should hoot with purpose. 🦉🚨
