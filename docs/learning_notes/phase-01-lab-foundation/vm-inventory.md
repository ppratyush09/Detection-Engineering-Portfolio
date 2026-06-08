# 🖥️ Phase 01: VM Inventory

> “Every VM in the lab should have a job. Otherwise, it is just digital furniture with RAM.” 🪑⚡

This file documents all virtual machines used in my detection engineering lab.

The goal is to keep a clean inventory of:

* VM names
* Roles
* Operating systems
* Network placement
* IP assignment
* Resource allocation
* Snapshot status
* Detection engineering purpose
* Current setup status
* Notes for future troubleshooting

A good lab inventory prevents the classic question:

> “Wait, which Windows box was supposed to be the victim, and why is the Linux VM judging me?” 👀

---

## 🎯 Purpose

This VM inventory helps me track the systems used for:

* Detection Engineering
* Threat Hunting
* Incident Response practice
* Malware Analysis
* Digital Forensics
* Network Detection
* Python automation
* Detection-as-Code preparation
* Lab troubleshooting

Each VM should have a clear reason to exist.

No mystery machines.

No “I installed this once and forgot why” energy. 🧃

---

## 🧠 Inventory Philosophy

This lab is designed like a small enterprise-style environment with extra analysis machines.

The core idea:

```text
Windows systems generate telemetry.
Linux systems provide tooling.
Analysis VMs support malware and forensics.
OPNsense controls the roads.
GitHub remembers the journey.
```

Every VM should answer at least one question:

* What does this machine help me learn?
* What logs can it generate?
* What detections can it support?
* What role does it play in the lab?
* What snapshot should protect it?
* What phase does it belong to?

If a VM cannot answer these questions, it may be a storage goblin. 🧌

---

## 🏰 High-Level VM Map

```text
Detection Engineering Lab
|
+-- OPNsense Firewall
|   +-- Gateway, routing, segmentation, firewall logs
|
+-- Windows Server / Domain Controller
|   +-- Active Directory, DNS, authentication telemetry
|
+-- Windows Client
|   +-- Endpoint testing, user behavior, process logs
|
+-- Admin Workstation
|   +-- Admin activity, PowerShell testing, false-positive practice
|
+-- Ubuntu Server
|   +-- Utility server, scripts, future logging/SIEM support
|
+-- FLARE VM
|   +-- Windows malware analysis and suspicious file triage
|
+-- REMnux VM
|   +-- Linux malware toolkit, decoding, IOC extraction
|
+-- Parrot VM
|   +-- Security testing, lab-only scanning, hunting support
|
+-- SIFT VM
    +-- Digital forensics, timeline analysis, artifact review
```

---

## 📋 Current VM Inventory Summary

Update this table as the lab changes.

| VM Name     | Role              | OS / Platform      | Network            | IP Assignment | Current Status        | Snapshot |
| ----------- | ----------------- | ------------------ | ------------------ | ------------- | --------------------- | -------- |
| OPNsense    | Firewall / Router | OPNsense           | WAN + LAB LAN      | Static LAN IP | ✅ In progress / Ready | ⏳ Update |
| DC01        | Domain Controller | Windows Server     | LAB LAN            | Static        | ✅ In progress / Ready | ⏳ Update |
| WINCLIENT01 | Windows Endpoint  | Windows 10/11      | LAB LAN            | DHCP / Static | ⏳ Update              | ⏳ Update |
| ADMIN01     | Admin Workstation | Windows 10/11      | LAB LAN            | DHCP / Static | ⏳ Update              | ⏳ Update |
| UBUNTU01    | Utility Server    | Ubuntu Server      | LAB LAN            | DHCP / Static | ⏳ Update              | ⏳ Update |
| FLARE01     | Malware Analysis  | Windows + FLARE VM | Isolated / LAB LAN | Controlled    | ⏳ Update              | ⏳ Update |
| REMNUX01    | Malware Analysis  | REMnux             | Isolated / LAB LAN | Controlled    | ⏳ Update              | ⏳ Update |
| PARROT01    | Security Testing  | Parrot OS          | LAB LAN            | DHCP / Static | ⏳ Update              | ⏳ Update |
| SIFT01      | Forensics         | SIFT Workstation   | LAB LAN / Isolated | DHCP / Static | ⏳ Update              | ⏳ Update |

Status values:

```text
✅ Ready
🟡 In progress
⏳ Planned
⚠️ Needs fixing
🔁 Rebuild needed
🧹 Retired / cleanup later
```

---

## 🧾 Standard VM Documentation Template

Use this template for each VM.

```markdown
## VM: <VM Name>

| Item | Details |
|---|---|
| Role | <Purpose of VM> |
| OS / Platform | <Operating system> |
| Phase | <Phase where this VM is used> |
| Network | <LAB LAN / Isolated / NAT / Bridged> |
| IP Address | <Static / DHCP / Reserved> |
| DNS Server | <DNS server used> |
| Gateway | <Gateway used> |
| RAM | <Memory assigned> |
| CPU | <vCPU count> |
| Disk | <Disk size> |
| Snapshot Name | `<snapshot-name>` |
| Current Status | <Ready / In progress / Needs fixing> |

### Purpose

Why this VM exists.

### Detection Engineering Value

What logs, telemetry, rules, or learning this VM supports.

### Current Configuration

What has already been configured.

### Pending Work

What still needs to be done.

### Notes

Anything important for future troubleshooting.
```

---

# 🔥 VM: OPNsense

| Item           | Details                                          |
| -------------- | ------------------------------------------------ |
| Role           | Firewall, router, lab gateway                    |
| OS / Platform  | OPNsense                                         |
| Phase          | Phase 01: Lab Foundation                         |
| Network        | WAN + LAB LAN                                    |
| IP Address     | LAB LAN gateway, update actual value             |
| DNS Server     | OPNsense / DC / forwarding, update as configured |
| Gateway        | WAN gateway from host/home network               |
| RAM            | Update                                           |
| CPU            | Update                                           |
| Disk           | Update                                           |
| Snapshot Name  | `opnsense-working-network-baseline`              |
| Current Status | ⏳ Update                                         |

## Purpose

OPNsense is the central firewall and router for the lab.

It controls how traffic moves between the internal lab network and the outside network.

It is responsible for:

* Gateway services
* Routing
* Firewall rules
* DHCP if configured
* DNS forwarding if configured
* Traffic visibility
* Network segmentation
* Future firewall log review

OPNsense is the lab’s packet bouncer.

No packet enters the party without being judged. 🔥

## Detection Engineering Value

OPNsense supports future detection work by providing:

* Firewall logs
* Blocked connection visibility
* Allowed traffic visibility
* Network troubleshooting evidence
* Controlled access to internet resources
* Future Suricata or network detection support

## Current Configuration

Update this section:

* [ ] WAN interface configured
* [ ] LAN interface configured
* [ ] LAB LAN subnet configured
* [ ] DHCP configured if used
* [ ] DNS settings configured
* [ ] Firewall rules reviewed
* [ ] Gateway reachable from lab machines
* [ ] Snapshot taken

## Pending Work

* Document exact LAN IP
* Document DHCP scope
* Document DNS plan
* Document firewall rules
* Confirm logging settings
* Confirm baseline snapshot

## Notes

If OPNsense is down or misconfigured, the lab network may stop working.

Troubleshooting should start here when multiple VMs lose connectivity.

---

# 🪟 VM: DC01

| Item           | Details                                               |
| -------------- | ----------------------------------------------------- |
| Role           | Windows Server / Domain Controller                    |
| OS / Platform  | Windows Server                                        |
| Phase          | Phase 01: Lab Foundation, Phase 02: Windows Telemetry |
| Network        | LAB LAN                                               |
| IP Address     | Static, update actual value                           |
| DNS Server     | Usually itself                                        |
| Gateway        | OPNsense LAN IP                                       |
| RAM            | Update                                                |
| CPU            | Update                                                |
| Disk           | Update                                                |
| Snapshot Name  | `dc01-domain-baseline`                                |
| Current Status | ⏳ Update                                              |

## Purpose

DC01 provides the Active Directory foundation for the lab.

It is responsible for:

* Domain services
* DNS
* Authentication
* Domain users
* Domain groups
* Group Policy
* Identity-related telemetry
* Domain-joined machine management

DC01 is the identity brain of the lab.

If it sneezes, the domain catches a cold. 🤧

## Detection Engineering Value

DC01 helps generate and analyze:

* Authentication events
* Logon activity
* Account creation
* Group membership changes
* Domain discovery
* Kerberos and NTLM activity
* Privileged account activity

Future detections may focus on:

* Suspicious account creation
* Domain admin group modification
* Failed logon bursts
* Domain discovery commands
* Unusual authentication patterns

## Current Configuration

Update this section:

* [ ] Static IP configured
* [ ] DNS role configured
* [ ] AD DS installed
* [ ] Domain created
* [ ] Domain name documented safely
* [ ] Windows Client joined to domain
* [ ] Admin Workstation joined to domain
* [ ] Snapshot taken

## Pending Work

* Document domain name safely
* Document important services
* Document baseline users/groups
* Enable useful Windows logging later
* Prepare for Phase 02 telemetry notes

## Notes

Domain-joined clients should use DC01 as DNS.

If domain join fails, DNS should be checked first.

Then DNS again.

Then maybe something else. 🧭

---

# 💻 VM: WINCLIENT01

| Item           | Details                                                                        |
| -------------- | ------------------------------------------------------------------------------ |
| Role           | Windows endpoint / test client                                                 |
| OS / Platform  | Windows 10/11                                                                  |
| Phase          | Phase 01: Lab Foundation, Phase 02: Windows Telemetry, Phase 03: Sigma and KQL |
| Network        | LAB LAN                                                                        |
| IP Address     | DHCP / Static, update actual value                                             |
| DNS Server     | DC01 IP                                                                        |
| Gateway        | OPNsense LAN IP                                                                |
| RAM            | Update                                                                         |
| CPU            | Update                                                                         |
| Disk           | Update                                                                         |
| Snapshot Name  | `winclient-domain-joined`                                                      |
| Current Status | ⏳ Update                                                                       |

## Purpose

WINCLIENT01 acts as a normal endpoint system in the lab.

It is used to generate realistic Windows activity and validate detections.

It supports:

* Endpoint telemetry
* User activity simulation
* Process creation logging
* PowerShell testing
* Discovery behavior testing
* Sigma and KQL validation
* Future Sysmon testing

This VM is where suspicious behavior will politely knock on the logs. 🚪

## Detection Engineering Value

WINCLIENT01 is useful for testing detections related to:

* PowerShell execution
* Encoded commands
* Discovery commands
* Suspicious parent-child process relationships
* File creation
* User activity
* Local account changes
* Pre-ransomware behavior

Future detections:

* Suspicious PowerShell encoded command
* Windows discovery command burst
* New local user created
* Suspicious archive creation
* Shadow copy deletion attempt
* Unusual process execution path

## Current Configuration

Update this section:

* [ ] Network configured
* [ ] Correct DNS configured
* [ ] Domain joined
* [ ] Local admin access verified
* [ ] Snapshot taken
* [ ] Windows updates completed if needed
* [ ] Basic telemetry confirmed

## Pending Work

* Enable PowerShell logging
* Install Sysmon later
* Generate safe test activity
* Export sample event logs
* Validate first Sigma/KQL detections

## Notes

This VM should have a clean rollback point before running detection tests.

The endpoint will eventually become noisy.

That is fine.

Noisy with purpose is telemetry. Noisy without purpose is a toddler with cymbals. 🥁

---

# 🧙 VM: ADMIN01

| Item           | Details                                                                        |
| -------------- | ------------------------------------------------------------------------------ |
| Role           | Admin Workstation                                                              |
| OS / Platform  | Windows 10/11                                                                  |
| Phase          | Phase 01: Lab Foundation, Phase 02: Windows Telemetry, Phase 03: Sigma and KQL |
| Network        | LAB LAN                                                                        |
| IP Address     | DHCP / Static, update actual value                                             |
| DNS Server     | DC01 IP                                                                        |
| Gateway        | OPNsense LAN IP                                                                |
| RAM            | Update                                                                         |
| CPU            | Update                                                                         |
| Disk           | Update                                                                         |
| Snapshot Name  | `admin01-domain-joined`                                                        |
| Current Status | ⏳ Update                                                                       |

## Purpose

ADMIN01 simulates administrative activity in the lab.

It is used to understand the difference between legitimate admin behavior and suspicious admin-like behavior.

It supports:

* PowerShell testing
* Remote management testing
* Domain administration activity
* False-positive analysis
* Privileged activity simulation
* Lateral movement detection practice later

ADMIN01 is the clipboard wizard of the domain. 📋

## Detection Engineering Value

ADMIN01 helps with detections involving:

* PowerShell remoting
* Administrative tools
* Remote service management
* Domain user/group activity
* Suspicious use of admin privileges
* Normal admin activity baseline
* False-positive tuning

Important detection lesson:

> Not every admin command is evil.
> But every powerful command deserves context.

## Current Configuration

Update this section:

* [ ] Network configured
* [ ] Correct DNS configured
* [ ] Domain joined
* [ ] Admin tools installed if needed
* [ ] Snapshot taken
* [ ] Can reach DC
* [ ] Can perform intended admin tasks

## Pending Work

* Document installed admin tools
* Create test admin account if needed
* Generate benign admin activity
* Compare admin behavior with suspicious behavior
* Use for future false-positive tuning

## Notes

This VM helps make detections more realistic.

A good detection should not alert on every normal admin action unless the goal is analyst sadness. 😵

---

# 🐧 VM: UBUNTU01

| Item           | Details                                              |
| -------------- | ---------------------------------------------------- |
| Role           | Utility server                                       |
| OS / Platform  | Ubuntu Server                                        |
| Phase          | Phase 01: Lab Foundation, Phase 05/06 future support |
| Network        | LAB LAN                                              |
| IP Address     | DHCP / Static, update actual value                   |
| DNS Server     | DC01 / OPNsense, update based on role                |
| Gateway        | OPNsense LAN IP                                      |
| RAM            | Update                                               |
| CPU            | Update                                               |
| Disk           | Update                                               |
| Snapshot Name  | `ubuntu-clean-baseline`                              |
| Current Status | ⏳ Update                                             |

## Purpose

UBUNTU01 is the utility server for the lab.

Possible future roles:

* Log collector
* Syslog server
* Web server for safe traffic generation
* Python automation host
* File transfer testing system
* Future SIEM support
* Future Wazuh, ELK, Graylog, or Splunk experiment

Ubuntu is the quiet worker in the corner.

Not dramatic.

Very useful. 🐧

## Detection Engineering Value

UBUNTU01 can support:

* Linux logging
* Network traffic generation
* Safe server-side HTTP testing
* Syslog collection
* Python scripts
* Future SIEM integration
* Lab automation

Future use cases:

* Generate safe web traffic
* Host safe test files
* Receive logs
* Run detection helper scripts
* Support Suricata/network testing

## Current Configuration

Update this section:

* [ ] Installed
* [ ] Network configured
* [ ] Gateway reachable
* [ ] DNS configured
* [ ] SSH configured if needed
* [ ] Snapshot taken
* [ ] Updates completed if needed

## Pending Work

* Decide final role
* Configure static IP if needed
* Install tools as required
* Document installed packages
* Prepare for log collection

## Notes

Ubuntu should remain simple until its role is clear.

Do not install half the internet because one future idea winked at you. 🌐

---

# 🔥 VM: FLARE01

| Item           | Details                              |
| -------------- | ------------------------------------ |
| Role           | Windows malware analysis workstation |
| OS / Platform  | Windows + FLARE VM                   |
| Phase          | Phase 04: YARA and Malware Analysis  |
| Network        | Isolated / controlled LAB LAN        |
| IP Address     | Controlled, update as needed         |
| DNS Server     | Depends on isolation mode            |
| Gateway        | Depends on isolation mode            |
| RAM            | Update                               |
| CPU            | Update                               |
| Disk           | Update                               |
| Snapshot Name  | `flare-clean-analysis-baseline`      |
| Current Status | ⏳ Update                             |

## Purpose

FLARE01 is used for Windows-based malware analysis and suspicious file triage.

It supports:

* Static file analysis
* PE file inspection
* Strings analysis
* Suspicious script review
* YARA rule development
* IOC extraction
* Safe malware-analysis learning

FLARE is the file detective with a magnifying glass and too many tools. 🔍

## Detection Engineering Value

FLARE01 helps convert file analysis into detections:

* Suspicious strings become YARA rules
* Malware-like behavior becomes Sigma/KQL ideas
* Network clues become Suricata ideas
* File indicators become IOC notes
* Analysis findings become reports

Detection chain:

```text
Suspicious file
        ↓
FLARE analysis
        ↓
Strings / imports / behavior clues
        ↓
YARA + Sigma + KQL + Suricata ideas
        ↓
Sanitized report
```

## Current Configuration

Update this section:

* [ ] FLARE installed
* [ ] Tools verified
* [ ] Snapshot taken
* [ ] Network mode documented
* [ ] Shared folders reviewed
* [ ] No suspicious files stored in baseline

## Pending Work

* Create safe analysis methodology
* Add static analysis checklist
* Add dynamic analysis checklist
* Test YARA safely
* Document analysis workflow
* Keep samples out of GitHub

## Notes

Important safety rule:

> Upload rules and notes, not malware samples.

FLARE should be restored to a clean baseline after risky analysis.

Curiosity is useful.

Unsafe curiosity is a paperwork generator. 🧯

---

# 🧊 VM: REMNUX01

| Item           | Details                             |
| -------------- | ----------------------------------- |
| Role           | Linux malware analysis toolkit      |
| OS / Platform  | REMnux                              |
| Phase          | Phase 04: YARA and Malware Analysis |
| Network        | Isolated / controlled LAB LAN       |
| IP Address     | Controlled, update as needed        |
| DNS Server     | Depends on isolation mode           |
| Gateway        | Depends on isolation mode           |
| RAM            | Update                              |
| CPU            | Update                              |
| Disk           | Update                              |
| Snapshot Name  | `remnux-clean-toolkit-baseline`     |
| Current Status | ⏳ Update                            |

## Purpose

REMNUX01 supports malware analysis, IOC extraction, decoding, and network artifact review.

It supports:

* IOC extraction
* Decoding suspicious content
* Script analysis
* Network artifact review
* PCAP review later
* YARA support
* Suspicious file triage

REMnux is the calm terminal wizard.

It does not panic.

It parses. 🧊

## Detection Engineering Value

REMNUX01 helps produce:

* IOC tables
* Decoded strings
* Network indicators
* YARA rule ideas
* Suricata rule ideas
* Malware triage notes
* Sanitized analysis reports

Future use cases:

* Decode suspicious payloads
* Extract URLs/domains
* Review PCAPs
* Analyze script artifacts
* Support fake/sinkhole services later

## Current Configuration

Update this section:

* [ ] REMnux imported/installed
* [ ] Tools verified
* [ ] Network mode documented
* [ ] Snapshot taken
* [ ] Updates completed if needed

## Pending Work

* Document common tools
* Practice IOC extraction
* Add malware triage workflow
* Add safe analysis notes
* Connect findings to YARA and Suricata

## Notes

REMnux is often used alongside FLARE.

Together, they make a good malware-analysis pair:

```text
FLARE = Windows file investigation
REMnux = Linux decoding and artifact analysis
```

Two analysts.

One suspicious file.

Many tiny clues. 🧩

---

# 🦜 VM: PARROT01

| Item           | Details                                  |
| -------------- | ---------------------------------------- |
| Role           | Security testing and threat hunting VM   |
| OS / Platform  | Parrot OS                                |
| Phase          | Phase 05: Suricata and Network Detection |
| Network        | LAB LAN only                             |
| IP Address     | DHCP / Static, update actual value       |
| DNS Server     | DC01 / OPNsense, update based on need    |
| Gateway        | OPNsense LAN IP                          |
| RAM            | Update                                   |
| CPU            | Update                                   |
| Disk           | Update                                   |
| Snapshot Name  | `parrot-clean-testing-baseline`          |
| Current Status | ⏳ Update                                 |

## Purpose

PARROT01 is used for controlled security testing inside the lab.

It supports:

* Lab-only scanning
* Recon behavior simulation
* Safe traffic generation
* Suricata validation
* Threat hunting practice
* Network testing

Parrot is the noisy bird with receipts. 🦜

## Detection Engineering Value

PARROT01 helps generate traffic for:

* Network scan detection
* Suspicious connection attempts
* Reconnaissance behavior
* Suricata rule testing
* Firewall log review
* Endpoint/network correlation

Important safety boundary:

> Parrot only tests the lab.
> The outside world is not a punching bag.

## Current Configuration

Update this section:

* [ ] Installed/imported
* [ ] Network configured
* [ ] Lab-only boundary confirmed
* [ ] Tools verified
* [ ] Snapshot taken
* [ ] Can reach intended lab systems

## Pending Work

* Document allowed lab-only tests
* Prepare network detection scenarios
* Use for Suricata validation
* Record traffic generation notes
* Avoid uncontrolled scanning

## Notes

Parrot should be used carefully and intentionally.

Every test should have a purpose and stay inside the lab.

No random tool fireworks. 🎆

---

# 🔎 VM: SIFT01

| Item           | Details                            |
| -------------- | ---------------------------------- |
| Role           | Digital forensics workstation      |
| OS / Platform  | SIFT Workstation                   |
| Phase          | Phase 04/Forensics Support         |
| Network        | LAB LAN / Isolated                 |
| IP Address     | DHCP / Static, update actual value |
| DNS Server     | Depends on role                    |
| Gateway        | Depends on role                    |
| RAM            | Update                             |
| CPU            | Update                             |
| Disk           | Update                             |
| Snapshot Name  | `sift-clean-forensics-baseline`    |
| Current Status | ⏳ Update                           |

## Purpose

SIFT01 is used for digital forensics and incident reconstruction.

It supports:

* Timeline analysis
* Artifact review
* Disk image review
* File-system investigation
* Evidence handling practice
* Post-incident analysis
* Detection improvement from forensic findings

SIFT is the forensic librarian with a flashlight. 🔦

## Detection Engineering Value

SIFT01 helps connect detections to evidence.

It can support:

* Timeline reconstruction
* Windows artifact review
* Persistence evidence review
* File-system activity analysis
* Incident sequence reconstruction
* Post-detection investigation notes

Detection lesson:

> Better forensic understanding creates better detection logic.

## Current Configuration

Update this section:

* [ ] Installed/imported
* [ ] Network mode documented
* [ ] Tools verified
* [ ] Snapshot taken
* [ ] Storage reviewed
* [ ] Evidence-handling workflow planned

## Pending Work

* Document forensic workflow
* Practice timeline creation
* Analyze safe lab artifacts
* Connect findings to detection reports
* Keep evidence sanitized

## Notes

SIFT should be used with clean evidence handling habits.

Do not mix personal/work data with lab evidence.

Evidence likes clean tables and careful notes. 🧾

---

## 🧮 Resource Planning

Use this section to track host resource usage.

Host system details:

| Item                    | Details            |
| ----------------------- | ------------------ |
| CPU                     | Update             |
| RAM                     | Update             |
| Storage                 | Update             |
| Virtualization Platform | VMware Workstation |
| Notes                   | Update             |

Suggested VM resource planning:

| VM          | Suggested RAM | Suggested vCPU | Notes                        |
| ----------- | ------------: | -------------: | ---------------------------- |
| OPNsense    |          2 GB |         1 to 2 | Lightweight firewall         |
| DC01        |     4 to 6 GB |              2 | AD and DNS                   |
| WINCLIENT01 |     4 to 6 GB |              2 | Endpoint testing             |
| ADMIN01     |     4 to 6 GB |              2 | Admin testing                |
| UBUNTU01    |     2 to 4 GB |         1 to 2 | Utility server               |
| FLARE01     |  8 GB or more |         2 to 4 | Heavy tools                  |
| REMNUX01    |     4 to 8 GB |              2 | Analysis tools               |
| PARROT01    |     4 to 8 GB |              2 | Security tools               |
| SIFT01      |  8 GB or more |         2 to 4 | Forensics tools can be heavy |

Important:

> Do not run every VM at once unless needed.
> The host is powerful, but it is not a magic cloud with RGB. 🌩️

---

## ⚡ Which VMs Should Be Running?

Use this table to avoid unnecessary resource pressure.

| Task                       | VMs Needed                                                            |
| -------------------------- | --------------------------------------------------------------------- |
| Basic domain testing       | OPNsense, DC01, WINCLIENT01                                           |
| Admin behavior testing     | OPNsense, DC01, ADMIN01                                               |
| Sigma/KQL endpoint testing | OPNsense, DC01, WINCLIENT01, ADMIN01 if needed                        |
| Network detection testing  | OPNsense, Parrot, target VM, Suricata/monitoring system if configured |
| Malware static analysis    | FLARE01 or REMNUX01                                                   |
| Malware dynamic analysis   | FLARE01, REMNUX01, isolated network only                              |
| Forensic practice          | SIFT01, evidence source VM or safe image                              |
| Python automation          | UBUNTU01 or host machine                                              |
| Documentation only         | No lab VMs needed                                                     |

Tiny power-saving truth:

> If the VM is not part of the current experiment, let it sleep. Even VMs deserve naps. 😴

---

## 🔐 Safety Notes

This inventory must not include:

* Company hostnames
* Work IP addresses
* Client machine names
* Credentials
* API keys
* Sensitive screenshots
* Real incident system names
* Malware sample names from private cases
* Anything tied to production environments

Allowed:

* Lab VM names
* Lab-only private IPs
* Roles
* Resource allocation
* Snapshot names
* Safe notes
* Public-safe configuration summaries

Golden rule:

> Inventory the lab, not the secrets. 🔐

---

## ✅ VM Inventory Checklist

| Task                       | Status |
| -------------------------- | ------ |
| OPNsense documented        | ⏳      |
| DC01 documented            | ⏳      |
| WINCLIENT01 documented     | ⏳      |
| ADMIN01 documented         | ⏳      |
| UBUNTU01 documented        | ⏳      |
| FLARE01 documented         | ⏳      |
| REMNUX01 documented        | ⏳      |
| PARROT01 documented        | ⏳      |
| SIFT01 documented          | ⏳      |
| Snapshot names added       | ⏳      |
| IP assignments added       | ⏳      |
| DNS/gateway values added   | ⏳      |
| VM resource values added   | ⏳      |
| Current status updated     | ⏳      |
| No sensitive data included | ✅      |

---

## 🏁 Final Note

This VM inventory is the lab’s roll call.

Each machine has a purpose.

Each purpose supports a skill.

Each skill supports the larger goal:

> Become better at detecting, hunting, analyzing, documenting, and explaining suspicious behavior.

The lab is not just VMs.

It is a training ground.

A tiny enterprise.

A safe cyber workshop.

A place where logs are born, packets confess, files get questioned, and alerts learn when to hoot. 🦉🚨

