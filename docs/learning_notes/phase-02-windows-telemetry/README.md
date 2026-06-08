# 📜 Phase 02: Windows Telemetry

> “Before writing detections, first teach Windows to stop whispering and start leaving receipts.” 🧾🪟

This phase focuses on understanding and configuring **Windows telemetry** for detection engineering.

Phase 01 built the lab foundation.
Phase 02 makes the Windows systems speak in useful logs.

The goal is to learn what Windows records, where it records it, which logs matter for detection engineering, and how to turn raw event data into Sigma rules, KQL queries, and investigation notes.

In simple words:

> No logs, no detections.
> No telemetry, no hunting.
> No visibility, just vibes in a trench coat. 🕵️‍♂️

---

## 🎯 Phase Objective

The objective of Phase 02 is to build strong Windows telemetry understanding.

This includes:

* Windows Event Logs
* Security logs
* System logs
* PowerShell logs
* Sysmon logs
* Process creation visibility
* Authentication events
* Account management events
* Group membership changes
* Service creation events
* Scheduled task events
* Registry visibility
* File activity visibility
* Telemetry-to-detection mapping

Phase 02 is considered successful when I can answer:

> What happened?
> Where is it logged?
> Which event ID records it?
> Which fields matter?
> How can I detect it?
> How can I investigate it?

That is the telemetry treasure map. 🗺️

---

## 🧭 Phase Scope

This phase focuses on **visibility**, not full attack simulation.

Included in this phase:

* Understanding Windows log channels
* Identifying important Event IDs
* Enabling useful logging
* Understanding Sysmon
* Learning PowerShell logging
* Testing basic log generation
* Mapping events to detection ideas
* Preparing for Sigma and KQL validation

Not included yet:

* Full ransomware simulation
* Real malware execution
* Advanced detection pipelines
* GitHub Actions validation
* Full SIEM deployment
* Large-scale log forwarding

Those come later.

This phase is about learning the language of Windows logs.

And Windows speaks in Event IDs, field names, and occasional cryptic grunts. 🪵

---

## 🧱 Why Windows Telemetry Matters

Detection engineering depends on visibility.

If an attacker runs a command but the system does not log the right fields, detection becomes guesswork.

Windows telemetry helps detect:

* Process execution
* Suspicious command lines
* PowerShell abuse
* User logons
* Failed authentication
* Account creation
* Group membership changes
* Service creation
* Scheduled tasks
* Registry changes
* File creation
* Network connections
* Persistence attempts
* Defense evasion activity

Telemetry is the raw material.

Detection logic is the crafted tool.

Without telemetry, detection engineering becomes a flashlight with no batteries. 🔦

---

## 🏰 Lab Systems Involved

| System      | Telemetry Role                                                                 |
| ----------- | ------------------------------------------------------------------------------ |
| DC01        | Domain authentication, account changes, group changes, AD-related events       |
| WINCLIENT01 | Endpoint behavior, process execution, PowerShell, user activity                |
| ADMIN01     | Admin behavior, PowerShell activity, remote management, false-positive testing |
| UBUNTU01    | Future log collection or SIEM support                                          |
| OPNsense    | Firewall and network logs                                                      |
| FLARE01     | Malware-analysis telemetry later                                               |
| REMNUX01    | Analysis support and IOC extraction                                            |
| PARROT01    | Controlled traffic generation later                                            |
| SIFT01      | Forensic artifact review and timeline analysis                                 |

Phase 02 focuses mainly on:

```text
DC01
WINCLIENT01
ADMIN01
```

These systems will generate the Windows logs needed for early Sigma and KQL work.

---

## 📁 Planned Phase 02 Files

This folder will contain notes for Windows telemetry learning.

```text
phase-02-windows-telemetry/
├── README.md
├── windows-event-logs.md
├── useful-event-ids.md
├── process-creation-logging.md
├── powershell-logging.md
├── sysmon-notes.md
├── authentication-events.md
├── account-management-events.md
├── telemetry-to-detection-map.md
└── phase-02-completion-summary.md
```

| File                             | Purpose                                               |
| -------------------------------- | ----------------------------------------------------- |
| `README.md`                      | Overview of Phase 02                                  |
| `windows-event-logs.md`          | Notes on Windows log channels and Event Viewer        |
| `useful-event-ids.md`            | Important Event IDs for detection engineering         |
| `process-creation-logging.md`    | Process execution visibility and command-line logging |
| `powershell-logging.md`          | PowerShell logging setup and useful events            |
| `sysmon-notes.md`                | Sysmon installation, config, and event types          |
| `authentication-events.md`       | Logon, failed logon, and authentication tracking      |
| `account-management-events.md`   | User creation, group changes, privilege changes       |
| `telemetry-to-detection-map.md`  | Mapping logs to Sigma and KQL detections              |
| `phase-02-completion-summary.md` | Summary before moving to Sigma/KQL phase              |

---

## 🪟 Key Windows Log Channels

Windows logs are stored in different channels.

Important ones for this lab:

| Log Channel                              | Why It Matters                                                      |
| ---------------------------------------- | ------------------------------------------------------------------- |
| Security                                 | Logons, account changes, privilege use, process creation if enabled |
| System                                   | Services, drivers, system-level changes                             |
| Application                              | Application activity and errors                                     |
| Windows PowerShell                       | PowerShell engine activity                                          |
| Microsoft-Windows-PowerShell/Operational | Script block logging and PowerShell operational events              |
| Microsoft-Windows-Sysmon/Operational     | Sysmon telemetry for process, network, registry, file, and more     |
| TaskScheduler Operational                | Scheduled task activity                                             |
| Windows Defender Operational             | Defender detections, exclusions, and security events                |

Tiny note:

> Event Viewer is where Windows keeps its diary, but the handwriting can be dramatic. 📖

---

## 🔐 Security Log Focus

The Windows Security log is one of the most important telemetry sources.

It can help track:

* Successful logons
* Failed logons
* User creation
* User deletion
* Group membership changes
* Privilege use
* Process creation, if enabled
* Service installation
* Account lockouts
* Audit policy changes

Important Security Event IDs:

| Event ID | Meaning                     | Detection Use                            |
| -------: | --------------------------- | ---------------------------------------- |
|     4624 | Successful logon            | Track user access and lateral movement   |
|     4625 | Failed logon                | Brute force or authentication failures   |
|     4634 | Logoff                      | Session tracking                         |
|     4648 | Explicit credential logon   | RunAs or alternate credentials           |
|     4672 | Special privileges assigned | Privileged logon activity                |
|     4688 | Process creation            | Command execution visibility             |
|     4697 | Service installed           | Possible persistence or remote execution |
|     4720 | User account created        | Suspicious account creation              |
|     4722 | User account enabled        | Re-enabled account detection             |
|     4726 | User account deleted        | Account cleanup or suspicious deletion   |
|     4732 | Member added to local group | Local admin group changes                |
|     4738 | User account changed        | Account modification tracking            |
|     4740 | Account locked out          | Brute-force or password issue signal     |
|     7045 | Service installed           | Service creation, usually in System log  |

Note:

> Event ID 4688 becomes much more useful when command-line logging is enabled.

Without command line, process creation is like seeing footprints but not knowing whether they wore boots, roller skates, or clown shoes. 👞

---

## ⚙️ Process Creation Logging

Process creation logging is one of the most important telemetry sources for detection engineering.

It helps detect:

* PowerShell execution
* Suspicious command lines
* Discovery commands
* LOLBins
* Parent-child process relationships
* Script execution
* Ransomware precursor commands
* Remote execution tools

Important field examples:

| Field                | Why It Matters                         |
| -------------------- | -------------------------------------- |
| New Process Name     | Process that started                   |
| Process Command Line | Full command executed                  |
| Creator Process Name | Parent process                         |
| Subject User Name    | User context                           |
| Computer             | Host where it happened                 |
| Process ID           | Useful for correlation                 |
| Parent Process ID    | Useful for process tree reconstruction |

Detection examples:

| Behavior                   | Detection Idea                  |
| -------------------------- | ------------------------------- |
| `powershell.exe -enc`      | Encoded PowerShell detection    |
| `cmd.exe /c whoami`        | Discovery command detection     |
| `net user /add`            | New local user creation         |
| `vssadmin delete shadows`  | Ransomware preparation          |
| Office spawning PowerShell | Suspicious parent-child process |

Process creation logs are the CCTV footage of command execution.

Tiny, verbose CCTV.

But useful. 📹

---

## ⚡ PowerShell Logging

PowerShell is extremely important for detection engineering because attackers and administrators both use it.

That makes it powerful.

And noisy.

And suspicious.

And useful.

PowerShell telemetry can include:

* Script block logging
* Module logging
* Transcription
* Engine start/stop events
* Suspicious command content
* Encoded commands
* Download cradles
* Obfuscation patterns

Important PowerShell Event IDs:

| Event ID | Log                    | Meaning                   |
| -------: | ---------------------- | ------------------------- |
|      400 | Windows PowerShell     | PowerShell engine started |
|      403 | Windows PowerShell     | PowerShell engine stopped |
|     4103 | PowerShell Operational | Module logging            |
|     4104 | PowerShell Operational | Script block logging      |
|      600 | Windows PowerShell     | Provider lifecycle event  |

High-value detection patterns:

```text
-EncodedCommand
-enc
IEX
Invoke-Expression
DownloadString
FromBase64String
New-Object Net.WebClient
System.Net.WebClient
Invoke-WebRequest
Start-BitsTransfer
```

PowerShell detection thought:

> PowerShell is not evil.
> PowerShell without context is spicy. 🌶️

---

## 🧰 Sysmon Notes

Sysmon provides richer endpoint telemetry than default Windows logs.

It can help capture:

* Process creation
* Network connections
* File creation
* Registry changes
* Image loads
* Process access
* DNS queries
* Driver loads
* WMI events
* Pipe events

Important Sysmon Event IDs:

| Event ID | Meaning                         | Detection Use                             |
| -------: | ------------------------------- | ----------------------------------------- |
|        1 | Process creation                | Command-line and process lineage          |
|        3 | Network connection              | Outbound/inbound process network activity |
|        7 | Image loaded                    | DLL loading visibility                    |
|       10 | Process access                  | Credential access and injection clues     |
|       11 | File created                    | Dropped files and suspicious paths        |
|       12 | Registry object created/deleted | Registry monitoring                       |
|       13 | Registry value set              | Persistence and config changes            |
|       15 | FileCreateStreamHash            | Alternate data streams                    |
|       22 | DNS query                       | Domain lookup visibility                  |
|       23 | File delete                     | File removal activity                     |

Sysmon is not magic.

Sysmon is visibility with opinions.

The config matters a lot.

Bad config equals noise soup.

Good config equals useful signal stew. 🍲

---

## 👤 Authentication Telemetry

Authentication logs are critical for detecting account misuse and lateral movement.

Important questions:

* Who logged in?
* Where did they log in from?
* What type of logon happened?
* Was the logon expected?
* Was the account privileged?
* Did the logon happen after suspicious activity?
* Did the same account access multiple systems?

Useful logon types:

| Logon Type | Meaning           | Detection Use               |
| ---------: | ----------------- | --------------------------- |
|          2 | Interactive       | Local keyboard login        |
|          3 | Network           | SMB, remote network access  |
|          4 | Batch             | Scheduled task or batch job |
|          5 | Service           | Service account logon       |
|          7 | Unlock            | Workstation unlock          |
|         10 | RemoteInteractive | RDP logon                   |
|         11 | CachedInteractive | Cached domain logon         |

Detection ideas:

* Multiple failed logons followed by success
* Privileged logon from unusual workstation
* RDP logon to server
* Network logon from unexpected host
* Explicit credential use with Event ID 4648

Authentication logs are identity footprints.

Some are normal.

Some walk across the carpet at 3 AM wearing muddy boots. 👣

---

## 👥 Account Management Telemetry

Account and group changes are high-value events.

Important activities:

* User created
* User enabled
* User disabled
* Password reset
* User added to local admins
* Domain group membership changed
* Privileged group modified

Useful Event IDs:

| Event ID | Meaning                         | Detection Use               |
| -------: | ------------------------------- | --------------------------- |
|     4720 | User account created            | New account detection       |
|     4722 | User account enabled            | Disabled account re-enabled |
|     4723 | Password change attempted       | Account activity            |
|     4724 | Password reset attempted        | Admin or suspicious reset   |
|     4725 | User account disabled           | Account lifecycle           |
|     4726 | User account deleted            | Cleanup behavior            |
|     4732 | Member added to local group     | Local admin detection       |
|     4733 | Member removed from local group | Group change tracking       |
|     4756 | Member added to universal group | Domain group monitoring     |

Detection idea:

> New account plus admin group membership plus remote logon equals “please investigate this little chain of chaos.” 🔗

---

## 🧪 Telemetry Test Plan

Phase 02 should include basic tests to confirm logs are being generated.

Example safe tests:

| Test                               | Expected Telemetry                       |
| ---------------------------------- | ---------------------------------------- |
| Run `whoami`                       | Process creation event                   |
| Run `ipconfig /all`                | Process creation event                   |
| Run PowerShell command             | PowerShell and process event             |
| Run encoded PowerShell test safely | Process command line and PowerShell logs |
| Create local test user             | Account creation event                   |
| Add test user to local group       | Group membership event                   |
| Start/stop service                 | System/service event                     |
| Create scheduled task              | Task Scheduler event                     |
| Make DNS lookup                    | DNS/Sysmon event if enabled              |
| Make HTTP request                  | Sysmon network event if enabled          |

Safe rule:

> Generate boring behavior first.
> Understand the logs before adding spice. 🌶️

---

## 🧾 Standard Telemetry Note Template

Use this template when documenting an event.

```markdown
## Event: <Event Name>

| Item | Details |
|---|---|
| Event ID | <ID> |
| Log Source | <Security / Sysmon / PowerShell / System> |
| System | <DC01 / WINCLIENT01 / ADMIN01> |
| Trigger Activity | <What action generated it> |
| Useful Fields | <Fields that matter> |
| Detection Use | <How this helps detection engineering> |
| False Positives | <Legitimate activity that may look similar> |

### Example Activity

What was run or configured?

### Expected Log

Where should the event appear?

### Detection Idea

What Sigma/KQL rule could be written from this?

### Notes

What did I learn?
```

---

## 🔎 Telemetry-to-Detection Mapping

This is the main skill of Phase 02.

Example:

| Observed Telemetry                              | Detection Type         | Rule Idea                                       |
| ----------------------------------------------- | ---------------------- | ----------------------------------------------- |
| Process command line contains `-EncodedCommand` | Sigma + KQL            | Suspicious PowerShell encoded command           |
| Multiple discovery commands in short time       | Sigma + KQL            | Windows discovery command burst                 |
| User account created                            | Sigma + KQL            | New local/domain user account                   |
| User added to administrators group              | Sigma + KQL            | Local admin group modification                  |
| Service installed                               | Sigma + KQL            | Possible persistence or remote service creation |
| DNS query to unusual domain                     | KQL + Suricata         | Suspicious DNS lookup                           |
| Script creates files in AppData                 | Sigma + KQL + YARA     | Suspicious script/dropper behavior              |
| PowerShell downloads content                    | Sigma + KQL + Suricata | Download cradle behavior                        |

The goal is to train this thinking:

```text
Behavior
   ↓
Telemetry
   ↓
Field
   ↓
Detection logic
   ↓
Validation
   ↓
Writeup
```

That is the detection engineering conveyor belt. 🏭

---

## 🧠 What Good Telemetry Notes Should Capture

Good notes should answer:

* What action was performed?
* Which system generated the event?
* Which log channel captured it?
* Which Event ID appeared?
* Which fields were useful?
* Was command line visible?
* Was the user visible?
* Was parent process visible?
* Was the destination visible?
* Could this become a Sigma rule?
* Could this become a KQL query?
* What false positives might exist?

A log without context is just a number wearing a tiny badge. 🎖️

---

## 🛡️ Detection Engineering Relevance

Phase 02 directly supports:

| Future Area       | Why Telemetry Matters                         |
| ----------------- | --------------------------------------------- |
| Sigma rules       | Sigma needs correct logsource and field names |
| KQL queries       | KQL needs correct tables and fields           |
| Threat hunting    | Hunting starts with knowing what data exists  |
| Incident response | IR needs timelines and event evidence         |
| Malware analysis  | Behavior needs telemetry validation           |
| Suricata          | Network alerts need endpoint correlation      |
| Python automation | Scripts can parse exported logs               |
| Reports           | Writeups need evidence and field details      |

Telemetry is the bridge between “I think this is suspicious” and “Here is the evidence.”

---

## 🔐 Safety Rules

This phase must not include:

* Company logs
* Client logs
* Production screenshots
* Real user details from work
* Credentials
* API keys
* Private investigation details
* Malware samples
* Sensitive hostnames
* Work IP ranges

Allowed:

* Lab-generated events
* Sanitized screenshots
* Lab VM names
* Private lab IPs
* Safe test commands
* Documentation of event IDs
* Detection ideas from lab behavior

Golden rule:

> Publish learning, not secrets. 🔐

---

## ✅ Phase 02 Checklist

| Task                                   | Status |
| -------------------------------------- | ------ |
| Windows log channels documented        | ⏳      |
| Useful Event IDs documented            | ⏳      |
| Security log basics documented         | ⏳      |
| Process creation logging documented    | ⏳      |
| PowerShell logging documented          | ⏳      |
| Sysmon notes created                   | ⏳      |
| Authentication event notes created     | ⏳      |
| Account management event notes created | ⏳      |
| Basic telemetry tests planned          | ⏳      |
| Telemetry-to-detection mapping started | ⏳      |
| Safety rules followed                  | ✅      |
| No sensitive logs uploaded             | ✅      |

---

## 🚀 Next Phase

After Phase 02, the next phase should be:

```text
Phase 03: Sigma and KQL
```

Phase 03 will focus on:

* Writing Sigma rules
* Writing matching KQL queries
* Testing simple detections
* Mapping rules to telemetry
* Documenting false positives
* Creating detection writeups

Phase 02 teaches the lab to speak.

Phase 03 teaches me to understand what it says and turn the useful bits into alerts. 🦉

---

## 🏁 Final Note

Windows telemetry is the foundation of endpoint detection engineering.

This phase is not about writing the fanciest rule.

It is about understanding the evidence.

A good detection engineer should know:

* What log source is needed
* What event ID matters
* Which fields are useful
* What normal looks like
* What suspicious looks like
* What false positives may appear
* How to validate the detection

The logs are the breadcrumbs.

The fields are the clues.

The detections are the traps.

And somewhere inside Event Viewer, a tiny Windows owl is preparing to hoot. 🦉🚨

