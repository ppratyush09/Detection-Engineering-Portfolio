# 🏗️ Phase 01: Lab Foundation

> “Before the alerts can sing, the lab must stop falling off the table.” 🧪🛠️

This phase documents the foundation of my home detection engineering lab.

Phase 00 was about building the GitHub structure.
Phase 01 is about documenting the actual lab environment where logs will be generated, detections will be tested, and suspicious behavior will be safely poked with a very professional stick. 🪄

The goal of this phase is to build a stable lab base for:

* Detection Engineering
* Threat Hunting
* Incident Response practice
* Malware Analysis preparation
* Digital Forensics practice
* Network Detection
* Future Detection-as-Code workflows

This is the “build the kingdom before hunting dragons” phase. 🏰🐉

---

## 🎯 Phase Objective

The objective of Phase 01 is to document and stabilize the lab foundation.

This includes:

* VM inventory
* Network design
* Firewall setup
* Active Directory setup
* Windows client setup
* Admin workstation setup
* Linux utility server setup
* Malware analysis VM placement
* Forensics VM placement
* Snapshot strategy
* Basic connectivity checks
* Troubleshooting notes
* Safety boundaries

The phase is complete when the lab has a clear structure, stable networking, working core systems, and documented rollback points.

In simple words:

> Build it.
> Connect it.
> Snapshot it.
> Document it.
> Try not to anger the DHCP spirits. 👻

---

## 🧭 Phase Scope

This phase focuses on the **lab foundation**, not advanced detection yet.

Included in this phase:

* Network layout
* VM roles
* IP planning
* Domain foundation
* Firewall routing
* Basic connectivity tests
* VM snapshots
* Lab safety rules
* Documentation of current state

Not included yet:

* Full detection rule validation
* Sysmon tuning
* SIEM deployment
* GitHub Actions
* Malware execution
* Advanced attack simulation
* Automated CI/CD pipelines

Those come later.

This phase is the floor.
Future phases are the furniture, sensors, traps, owl alarms, and suspiciously glowing dashboards. 🦉📊

---

## 🏰 Current Lab Kingdom

The lab is designed as a controlled internal environment protected by OPNsense.

```text
Internet / Host Network
        |
        v
OPNsense Firewall
        |
        v
Internal Lab Network
        |
        +-- Windows Server / Domain Controller
        +-- Windows Client
        +-- Admin Workstation
        +-- Ubuntu Server
        +-- FLARE VM
        +-- REMnux VM
        +-- Parrot VM
        +-- SIFT VM
```

The firewall acts as the gatekeeper.

The domain controller acts as the identity kingdom.

The Windows machines generate endpoint telemetry.

The Linux and analysis VMs support malware analysis, forensics, network testing, and future tooling.

Every VM has a job.

No random digital furniture allowed. 🪑

---

## 🧱 Lab Components

| Component              | Role                | Current Purpose                                                        |
| ---------------------- | ------------------- | ---------------------------------------------------------------------- |
| 🔥 OPNsense            | Firewall and router | Controls lab traffic, segmentation, routing, and future firewall logs  |
| 🪟 Windows Server / DC | Domain Controller   | Active Directory, DNS, authentication, and domain telemetry            |
| 💻 Windows Client      | Endpoint            | User activity, process logs, attack simulation, detection testing      |
| 🧙 Admin Workstation   | Admin system        | PowerShell, admin behavior, remote management, and validation activity |
| 🐧 Ubuntu Server       | Utility server      | Future logging, scripting, services, and SIEM/tooling support          |
| 🔥 FLARE VM            | Malware analysis    | Windows-based static analysis, suspicious file triage, YARA ideas      |
| 🧊 REMnux VM           | Malware analysis    | Linux-based IOC extraction, decoding, network artifact analysis        |
| 🦜 Parrot VM           | Security testing    | Controlled testing, recon simulation, threat hunting support           |
| 🔎 SIFT VM             | Digital forensics   | Timeline analysis, artifact review, incident reconstruction            |

---

## 🧠 Why This Lab Matters

This lab exists to answer practical security questions.

Examples:

* What does suspicious PowerShell look like in logs?
* How does domain discovery appear from a Windows endpoint?
* What events are created when a new local admin is added?
* What does lateral movement look like from source and target machines?
* How can malware-like behavior be safely analyzed?
* What network evidence appears during suspicious outbound activity?
* How can forensic artifacts support detection logic?
* How can lab behavior become Sigma, KQL, YARA, and Suricata rules?

The goal is to move from:

```text
I read about the technique.
```

to:

```text
I generated the behavior, collected the logs, wrote the detection, and documented the result.
```

That is the good stuff. The crunchy detection center. 🥨

---

## 🗺️ Planned Phase 01 Files

This folder will contain the main notes for lab setup and stabilization.

```text
phase-01-lab-foundation/
├── README.md
├── vm-inventory.md
├── network-setup.md
├── snapshot-notes.md
├── connectivity-checks.md
├── troubleshooting.md
└── phase-01-completion-summary.md
```

| File                             | Purpose                                                 |
| -------------------------------- | ------------------------------------------------------- |
| `README.md`                      | Overview of Phase 01                                    |
| `vm-inventory.md`                | List of all lab VMs, roles, OS, resources, and notes    |
| `network-setup.md`               | Network design, IP ranges, firewall notes, DNS, DHCP    |
| `snapshot-notes.md`              | Snapshot names, timing, purpose, rollback notes         |
| `connectivity-checks.md`         | Ping, DNS, domain join, internet access, routing checks |
| `troubleshooting.md`             | Issues faced and how they were fixed                    |
| `phase-01-completion-summary.md` | Final summary before moving to Phase 02                 |

---

## 🖥️ VM Inventory Plan

Each VM should be documented using this format:

```markdown
## VM Name: <Name>

| Item | Details |
|---|---|
| Role | <Purpose of VM> |
| OS | <Operating System> |
| Network | <Lab LAN / NAT / Isolated> |
| IP Address | <Static or DHCP> |
| DNS | <DNS server used> |
| RAM | <Memory assigned> |
| CPU | <vCPU count> |
| Snapshot Status | <Snapshot name and date> |
| Current State | <Ready / In progress / Needs fixing> |

### Notes

- What this VM is used for
- What has been configured
- What still needs to be done
```

This prevents the classic lab problem:

> “Which VM was this again, and why is it judging me from the sidebar?” 👀

---

## 🌐 Network Setup Goals

The network should support:

* Internal lab communication
* Domain services
* Controlled internet access
* Firewall visibility
* Future logging
* Future SIEM integration
* Safe testing boundaries

Basic network goals:

| Goal                               | Status               |
| ---------------------------------- | -------------------- |
| OPNsense firewall configured       | ✅ In progress / Done |
| Lab LAN created                    | ✅ In progress / Done |
| Domain controller reachable        | ✅ In progress / Done |
| Windows client joined to domain    | ✅ In progress / Done |
| Admin workstation joined to domain | ✅ In progress / Done |
| DNS resolution working             | ✅ In progress / Done |
| Internet access controlled         | ✅ In progress / Done |
| Snapshots taken after stable setup | ✅ In progress / Done |

Update statuses as the lab evolves.

---

## 🔥 OPNsense Role

OPNsense is the lab firewall.

Its job is to:

* Route traffic
* Segment the lab
* Control internet access
* Provide visibility into traffic
* Act as the boundary between the lab and outside world

OPNsense is basically the packet bouncer.

It does not care about excuses.

It checks the list. 🔥

Documentation to capture:

* WAN configuration
* LAN configuration
* DHCP settings
* DNS settings
* Firewall rules
* Gateway settings
* Snapshot name
* Known working state

---

## 🪟 Domain Controller Role

The Windows Server / DC provides the Active Directory foundation.

Its job is to:

* Manage domain users
* Provide authentication
* Handle DNS for the lab
* Support domain-joined systems
* Generate identity-related logs
* Support detection testing later

Detection value:

* Logon activity
* Account creation
* Group changes
* Domain discovery
* Authentication behavior
* Privileged user activity

The DC is where identity logs begin their tiny paperwork career. 📄

---

## 💻 Windows Client Role

The Windows client acts as a normal endpoint.

Its job is to:

* Generate endpoint telemetry
* Simulate user behavior
* Run controlled test commands
* Support Sigma and KQL validation later
* Provide process creation and PowerShell activity

Detection value:

* Process execution
* PowerShell behavior
* Discovery commands
* File activity
* Logon events
* Suspicious parent-child processes

This VM is the endpoint laboratory mouse, but treated respectfully. 🐭

---

## 🧙 Admin Workstation Role

The admin workstation is used to simulate administrative activity.

Its job is to:

* Run admin commands
* Test PowerShell behavior
* Simulate remote management
* Help distinguish normal admin activity from suspicious behavior
* Generate realistic false positive examples

Detection value:

* Admin tool usage
* PowerShell remoting
* Remote access patterns
* Privileged activity
* Domain management behavior

Important question this VM helps answer:

> Is this bad, or is this just admin work wearing a serious hat? 🎩

---

## 🐧 Ubuntu Server Role

The Ubuntu server is the utility machine.

Possible future roles:

* Log collector
* Script runner
* SIEM support system
* Web server for safe test traffic
* File server for lab experiments
* Python automation host
* Syslog destination

Detection value:

* Linux logs
* SSH activity
* Web traffic
* File transfer behavior
* Future log pipeline testing

Current personality:

> Quiet. Useful. Probably knows more than it says. 🐧

---

## 🔥 FLARE VM Role

FLARE VM is used for Windows malware analysis and suspicious file triage.

Its job is to support:

* Static malware analysis
* Windows executable inspection
* Suspicious script review
* Strings analysis
* YARA rule development
* IOC extraction
* Safe malware-analysis learning

GitHub safety rule:

> FLARE findings can become notes, YARA rules, and sanitized reports.
> Malware samples must not be uploaded.

FLARE is the file detective with sharp glasses. 🔍

---

## 🧊 REMnux Role

REMnux is used for Linux-based malware analysis and network artifact work.

Its job is to support:

* IOC extraction
* Decoding
* Unpacking practice
* Suspicious script review
* Network artifact analysis
* Malware analysis workflows
* YARA support

REMnux is the calm terminal monk of the lab. 🧊

---

## 🦜 Parrot Role

Parrot is used for controlled security testing and threat hunting support.

Its job is to support:

* Lab-only reconnaissance
* Controlled scanning
* Network testing
* Threat hunting utilities
* Safe attack simulation
* Suricata validation later

Safety note:

> Parrot only pokes the lab.
> The outside internet is not a punching bag. 🦜

---

## 🔎 SIFT Role

SIFT is used for digital forensics and incident reconstruction.

Its job is to support:

* Timeline analysis
* Artifact review
* Disk and file-system investigation
* Evidence-based thinking
* Incident reconstruction
* Detection improvement from forensic findings

SIFT helps answer:

> What happened, when did it happen, and what artifacts prove it?

This is where the lab puts on reading glasses and starts building timelines. 📚

---

## 📸 Snapshot Strategy

Snapshots are mandatory after stable milestones.

Snapshot rules:

* Snapshot before risky changes
* Snapshot after stable configuration
* Use clear names
* Document why the snapshot was taken
* Avoid snapshot chaos
* Keep rollback points clean

Suggested snapshot names:

```text
opnsense-working-network-baseline
dc01-domain-baseline
winclient-domain-joined
admin01-domain-joined
ubuntu-clean-baseline
flare-clean-analysis-baseline
remnux-clean-toolkit-baseline
parrot-clean-testing-baseline
sift-clean-forensics-baseline
```

Tiny law:

> Snapshot before chaos.
> Restore after chaos.
> Document during chaos. 📸

---

## ✅ Connectivity Checks

Basic checks to document:

| Check                            | Expected Result                  |
| -------------------------------- | -------------------------------- |
| Windows client can reach DC      | Ping or DNS resolution works     |
| Admin workstation can reach DC   | Ping or DNS resolution works     |
| Domain join works                | Client appears in AD             |
| DNS resolution works             | Domain names resolve correctly   |
| Internet access works if allowed | Updates/downloads work           |
| Lab machines can reach gateway   | OPNsense reachable               |
| OPNsense DHCP leases visible     | Clients receive proper IPs       |
| Static IPs documented            | Critical systems are predictable |

Possible commands:

```powershell
ipconfig /all
ping <domain-controller-ip>
nslookup <domain-name>
whoami /fqdn
nltest /dsgetdc:<domain-name>
```

Use these only in the lab.

No production screenshots.

No sensitive data.

No accidental “look, my real network!” moments. 🧯

---

## 🧯 Troubleshooting Notes to Capture

Common issues to record:

| Issue Type         | Examples                                   |
| ------------------ | ------------------------------------------ |
| Networking         | Wrong adapter, wrong gateway, wrong subnet |
| DNS                | Client using wrong DNS server              |
| DHCP               | Lease not assigned or wrong scope          |
| Domain Join        | Cannot contact domain controller           |
| Firewall           | Traffic blocked unexpectedly               |
| VM Resources       | Not enough RAM or CPU                      |
| Time Sync          | Domain authentication issues               |
| Snapshot Confusion | Wrong rollback point used                  |

Troubleshooting format:

```markdown
## Issue: <Short title>

### Symptom

What did I see?

### Cause

Why did it happen?

### Fix

What solved it?

### Lesson

What should I remember?
```

Every lab error becomes useful if documented.

Otherwise, it becomes folklore with error codes. 🧌

---

## 🔐 Safety Rules for Phase 01

This phase must not include:

* Company data
* Client data
* Credentials
* Real incident screenshots
* Public IPs tied to private work
* Work hostnames
* API keys
* Malware samples
* Sensitive network diagrams

Allowed:

* Lab-only notes
* Sanitized screenshots
* Private IP examples from lab
* VM roles
* Configuration summaries
* Learning notes
* Troubleshooting summaries

Golden rule:

> Build publicly. Leak nothing. 🔐

---

## 🧠 Detection Engineering Relevance

Phase 01 supports detection engineering by creating the environment needed for later telemetry.

This phase prepares for:

* Windows Event Log collection
* Sysmon deployment
* PowerShell logging
* Process creation detection
* Authentication event analysis
* Network traffic detection
* Malware analysis workflows
* Forensic evidence review
* Sigma and KQL validation
* YARA and Suricata testing

Without this phase, future detections would be floating in the air like lonely YAML balloons. 🎈

---

## 🧭 Exit Criteria

Phase 01 is complete when:

* [ ] Lab architecture is documented
* [ ] VM inventory is documented
* [ ] Network setup is documented
* [ ] OPNsense configuration is stable
* [ ] Domain controller is stable
* [ ] Windows client is joined to domain
* [ ] Admin workstation is joined to domain
* [ ] Ubuntu server role is documented
* [ ] FLARE VM role is documented
* [ ] REMnux VM role is documented
* [ ] Parrot VM role is documented
* [ ] SIFT VM role is documented
* [ ] Snapshots are created and named properly
* [ ] Connectivity checks are documented
* [ ] Troubleshooting notes are created
* [ ] No sensitive data is exposed
* [ ] Phase 01 completion summary is written

---

## 🚀 Next Phase

After Phase 01, the next phase should be:

```text
Phase 02: Windows Telemetry
```

Phase 02 will focus on:

* Windows Event Logs
* Important Event IDs
* Sysmon
* PowerShell logging
* Process creation visibility
* Authentication logs
* Log collection strategy
* Telemetry-to-detection mapping

Phase 01 builds the lab.

Phase 02 teaches the lab to speak in logs. 📜

---

## 🏁 Final Note

Phase 01 is the foundation of the detection engineering lab.

The goal is not to rush into alerts.

The goal is to build a stable environment where alerts can be created, tested, broken, fixed, and explained.

A strong lab foundation means:

* Better telemetry
* Better testing
* Better detections
* Better troubleshooting
* Better documentation
* Better confidence

This is the base camp.

The mountain is still ahead.

But at least now the backpack is packed, the map is labeled, and the firewall goblin has been given a job. 🧌🔥

