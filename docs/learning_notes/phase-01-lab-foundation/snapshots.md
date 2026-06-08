# 📸 Phase 01: Snapshot Notes

> “A VM snapshot is a save point before touching the suspicious glowing button.” 🎮🧪

This file documents the snapshot strategy for my detection engineering lab.

Snapshots are important because the lab will eventually include:

* Domain configuration
* Windows telemetry changes
* Sysmon installation
* Detection testing
* Attack simulation
* Malware analysis practice
* Forensics experiments
* Network detection testing
* Tool installation
* Configuration changes that may go sideways and start wearing a villain cape

The purpose of snapshots is simple:

> Break safely.
> Restore quickly.
> Learn confidently.
> Avoid rebuilding the entire kingdom because one setting sneezed. 🏰

---

## 🎯 Objective

The objective of this file is to track:

* Which VMs have snapshots
* When snapshots were taken
* Why snapshots were taken
* Which snapshot is safe to return to
* Which snapshots are temporary
* Which snapshots should be deleted later
* Which snapshots are important lab milestones

A snapshot is not just a backup button.

It is a lab checkpoint.

It says:

> “This machine was stable here. Future chaos may begin after this point.” 📍

---

## 🧠 Why Snapshots Matter

In a detection engineering lab, things will break.

That is not a bug. That is the curriculum.

Snapshots help recover from:

* Broken network settings
* Failed domain joins
* Bad DNS configuration
* Tool installation issues
* Logging misconfiguration
* Registry changes
* Malware-analysis experiments
* Detection testing mess
* Firewall rule mistakes
* “I clicked something and now the lab speaks ancient error language” situations

Without snapshots, troubleshooting can become archaeological excavation.

With snapshots, mistakes become safe experiments.

Tiny wisdom:

> Snapshots turn panic into a reversible learning event. 🔁

---

## 🧪 Snapshot Philosophy

My snapshot strategy follows this rule:

```text
Before major change: snapshot.
After stable success: snapshot.
Before risky testing: snapshot.
After messy testing: restore.
```

This keeps the lab clean and repeatable.

The goal is not to create hundreds of snapshots.

The goal is to create useful checkpoints.

Snapshot hoarding is real.

One day the disk will look at me and whisper:

> “Why are there 47 versions of Windows Client before lunch?” 🍽️

---

## 🗺️ Snapshot Naming Convention

Snapshot names should be clear, boring enough to be useful, and descriptive enough to avoid future confusion.

Recommended format:

```text
<vm-name>-<state>-<short-purpose>
```

Examples:

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

Avoid names like:

```text
snapshot1
final
working
test
new
before change
please work
very final
actual final
final-final-real
```

Those names are emotional poetry, not documentation. 😅

---

## 🧱 Snapshot Inventory

Use this table to track snapshot status.

| VM                  | Snapshot Name                       | Date       | Purpose                                    | Status   | Notes                                 |
| ------------------- | ----------------------------------- | ---------- | ------------------------------------------ | -------- | ------------------------------------- |
| OPNsense            | `opnsense-working-network-baseline` | YYYY-MM-DD | Stable firewall, WAN/LAN, routing baseline | ⏳ Update | Use before firewall rule experiments  |
| Windows Server / DC | `dc01-domain-baseline`              | YYYY-MM-DD | Stable AD DS, DNS, domain baseline         | ⏳ Update | Critical rollback point               |
| Windows Client      | `winclient-domain-joined`           | YYYY-MM-DD | Domain-joined endpoint baseline            | ⏳ Update | Use before endpoint telemetry changes |
| Admin Workstation   | `admin01-domain-joined`             | YYYY-MM-DD | Domain-joined admin machine baseline       | ⏳ Update | Use before admin simulation tests     |
| Ubuntu Server       | `ubuntu-clean-baseline`             | YYYY-MM-DD | Clean utility server baseline              | ⏳ Update | Use before installing log tools       |
| FLARE VM            | `flare-clean-analysis-baseline`     | YYYY-MM-DD | Clean malware-analysis baseline            | ⏳ Update | Use before suspicious file analysis   |
| REMnux VM           | `remnux-clean-toolkit-baseline`     | YYYY-MM-DD | Clean REMnux toolkit baseline              | ⏳ Update | Use before analysis experiments       |
| Parrot VM           | `parrot-clean-testing-baseline`     | YYYY-MM-DD | Clean testing baseline                     | ⏳ Update | Use before controlled scans/tests     |
| SIFT VM             | `sift-clean-forensics-baseline`     | YYYY-MM-DD | Clean forensic workstation baseline        | ⏳ Update | Use before forensic case practice     |

Status values:

```text
✅ Created
⏳ Planned
🔁 Updated
🧹 Delete later
⚠️ Needs review
```

---

## 🔥 OPNsense Snapshot Plan

OPNsense is the firewall and gateway for the lab.

Important snapshot points:

| Snapshot Point               | When to Take                                | Why                                  |
| ---------------------------- | ------------------------------------------- | ------------------------------------ |
| Fresh install                | After basic installation                    | Clean firewall rollback              |
| Interface assignment working | After WAN/LAN are configured                | Prevent adapter confusion later      |
| DHCP working                 | After lab clients receive leases            | Stable network checkpoint            |
| DNS/routing working          | After clients reach DC/internet as expected | Useful troubleshooting baseline      |
| Firewall baseline            | After rules are stable                      | Before detection/network experiments |

Recommended snapshot name:

```text
opnsense-working-network-baseline
```

Why this matters:

> If OPNsense breaks, the whole lab starts wandering around without roads. 🚦

---

## 🪟 Windows Server / Domain Controller Snapshot Plan

The Domain Controller is one of the most important systems in the lab.

Important snapshot points:

| Snapshot Point           | When to Take                         | Why                         |
| ------------------------ | ------------------------------------ | --------------------------- |
| Fresh Windows Server     | Before AD DS installation            | Clean OS rollback           |
| Static IP configured     | After IP/DNS settings are correct    | Network baseline            |
| AD DS installed          | After domain is created              | Domain baseline             |
| DNS working              | After domain resolution works        | Prevent domain chaos        |
| DHCP configured, if used | After DHCP scope works               | Enterprise-style checkpoint |
| Users/groups baseline    | After basic users/groups are created | Identity baseline           |

Recommended snapshot name:

```text
dc01-domain-baseline
```

Why this matters:

> The DC is the kingdom’s identity brain. If it gets confused, everyone forgets who they are. 👑

---

## 💻 Windows Client Snapshot Plan

The Windows Client is used for endpoint behavior and telemetry testing.

Important snapshot points:

| Snapshot Point    | When to Take                                        | Why                              |
| ----------------- | --------------------------------------------------- | -------------------------------- |
| Fresh install     | After OS installation                               | Clean rollback                   |
| Network working   | After client receives correct IP/DNS                | Stable connectivity baseline     |
| Domain joined     | After successful domain join                        | Important endpoint checkpoint    |
| Logging enabled   | After Windows logging configuration                 | Before Sysmon or detection tests |
| Pre-test baseline | Before running attack simulation or telemetry tests | Reset point                      |

Recommended snapshot name:

```text
winclient-domain-joined
```

Why this matters:

> This VM will generate many future logs. It deserves a clean reset point before the log confetti begins. 🎊

---

## 🧙 Admin Workstation Snapshot Plan

The Admin Workstation is used to simulate admin behavior.

Important snapshot points:

| Snapshot Point        | When to Take                        | Why                   |
| --------------------- | ----------------------------------- | --------------------- |
| Fresh install         | After OS installation               | Clean rollback        |
| Network working       | After gateway and DNS work          | Connectivity baseline |
| Domain joined         | After domain join                   | Admin baseline        |
| Admin tools installed | After useful tools are installed    | Tooling checkpoint    |
| Pre-admin-test        | Before PowerShell/admin simulations | Reset point           |

Recommended snapshot name:

```text
admin01-domain-joined
```

Why this matters:

> Admin activity can look suspicious. This machine helps me learn the difference between evil and Tuesday IT work. 📋

---

## 🐧 Ubuntu Server Snapshot Plan

Ubuntu may support future logging, scripting, and tooling.

Important snapshot points:

| Snapshot Point            | When to Take                                        | Why                       |
| ------------------------- | --------------------------------------------------- | ------------------------- |
| Fresh install             | After OS installation                               | Clean baseline            |
| Network working           | After gateway/DNS checks                            | Stable connectivity       |
| Basic updates done        | After system updates                                | Tool-ready baseline       |
| Before SIEM/log tooling   | Before installing ELK, Wazuh, Splunk, Graylog, etc. | Safe rollback             |
| Before scripting projects | Before major Python/tool changes                    | Clean automation baseline |

Recommended snapshot name:

```text
ubuntu-clean-baseline
```

Why this matters:

> Ubuntu is the utility drawer. If the drawer explodes, all the tools scatter. 🧰

---

## 🔥 FLARE VM Snapshot Plan

FLARE VM is used for Windows malware analysis and suspicious file review.

Important snapshot points:

| Snapshot Point                  | When to Take                         | Why                       |
| ------------------------------- | ------------------------------------ | ------------------------- |
| Clean FLARE install             | After FLARE is fully installed       | Main analysis baseline    |
| Tool updates complete           | After important tools are updated    | Stable toolkit checkpoint |
| Before suspicious file analysis | Before analyzing any suspicious file | Safety checkpoint         |
| After test analysis             | Restore, do not keep messy state     | Clean lab hygiene         |

Recommended snapshot name:

```text
flare-clean-analysis-baseline
```

Safety notes:

* Do not upload malware samples to GitHub.
* Do not analyze real malware with unrestricted internet.
* Disable shared folders during risky work if needed.
* Restore snapshot after suspicious analysis.
* Keep analysis notes sanitized.

FLARE rule:

> If the file is suspicious, snapshot first. Curiosity is good. Regret is not. 🔥

---

## 🧊 REMnux Snapshot Plan

REMnux supports Linux-based malware analysis, IOC extraction, decoding, and network artifact work.

Important snapshot points:

| Snapshot Point            | When to Take                         | Why                         |
| ------------------------- | ------------------------------------ | --------------------------- |
| Clean REMnux baseline     | After installation/import            | Clean toolkit rollback      |
| Tool updates complete     | After updates                        | Stable analysis environment |
| Before analysis workflow  | Before suspicious artifact work      | Reset point                 |
| Before network simulation | Before fake services or traffic labs | Clean rollback              |

Recommended snapshot name:

```text
remnux-clean-toolkit-baseline
```

Why this matters:

> REMnux is calm, but I should still give it a time machine. 🧊

---

## 🦜 Parrot Snapshot Plan

Parrot is used for controlled security testing, lab-only recon, and future Suricata validation.

Important snapshot points:

| Snapshot Point          | When to Take                     | Why                   |
| ----------------------- | -------------------------------- | --------------------- |
| Clean Parrot baseline   | After install/import             | Clean rollback        |
| Network verified        | After lab-only network checks    | Safe testing baseline |
| Before scanning tests   | Before controlled lab scans      | Reset point           |
| Before tool experiments | Before installing/changing tools | Avoid tool chaos      |

Recommended snapshot name:

```text
parrot-clean-testing-baseline
```

Safety note:

> Parrot only tests the lab. The internet is not a punching bag. 🦜

---

## 🔎 SIFT Snapshot Plan

SIFT is used for digital forensics, timeline analysis, artifact review, and incident reconstruction.

Important snapshot points:

| Snapshot Point               | When to Take                   | Why                        |
| ---------------------------- | ------------------------------ | -------------------------- |
| Clean SIFT baseline          | After install/import           | Clean forensic workstation |
| Tool updates complete        | After updates                  | Stable analysis toolkit    |
| Before forensic case         | Before working on lab evidence | Reset point                |
| Before large evidence import | Before adding big files/images | Avoid storage chaos        |

Recommended snapshot name:

```text
sift-clean-forensics-baseline
```

Why this matters:

> SIFT handles evidence. Evidence likes clean tables. 🔎

---

## 🧪 Snapshot Decision Matrix

Use this to decide when a snapshot is needed.

| Situation                        | Snapshot Needed? | Reason                               |
| -------------------------------- | ---------------- | ------------------------------------ |
| Installing a major tool          | ✅ Yes            | Tool installs can break dependencies |
| Changing network settings        | ✅ Yes            | Network breakage is common           |
| Joining domain                   | ✅ Yes            | Important lab milestone              |
| Enabling logging/Sysmon          | ✅ Yes            | Telemetry changes can be noisy       |
| Running attack simulation        | ✅ Yes            | Easy rollback after tests            |
| Running suspicious file analysis | ✅ Yes            | Safety and cleanup                   |
| Editing a README                 | ❌ No             | Git handles versioning               |
| Adding a Markdown note           | ❌ No             | No VM state change                   |
| Installing normal updates        | ⚠️ Maybe         | Snapshot if VM is critical           |
| Testing firewall rules           | ✅ Yes            | OPNsense changes can isolate systems |

Simple rule:

> If the VM state can become messy, snapshot first. 🧹

---

## 🔁 Restore Strategy

Snapshots should be restored when:

* A test leaves the VM messy
* A tool breaks the system
* Malware-analysis state should be cleaned
* Network settings become confusing
* Logs need to be reset for a clean test
* A detection test needs to be repeated from baseline

Before restoring:

* Save any useful notes
* Export safe logs if needed
* Do not save sensitive data into GitHub
* Record what was learned
* Confirm which snapshot is being restored

Restore reminder:

> Restoring without notes means the lesson vanishes into the fog. 🌫️

---

## 🧹 Snapshot Cleanup Rules

Too many snapshots can waste storage and create confusion.

Keep:

* Clean baseline snapshots
* Major milestone snapshots
* Pre-risky-test snapshots only while needed
* Stable tool installation snapshots

Delete later:

* Temporary test snapshots
* Confusing duplicate snapshots
* Failed configuration snapshots
* Snapshots with unclear names
* Old snapshots replaced by better baselines

Cleanup checklist:

* [ ] Is this snapshot still useful?
* [ ] Does it have a clear name?
* [ ] Is there a newer stable baseline?
* [ ] Is it taking too much storage?
* [ ] Would I know why this exists one month later?

If the answer is “no idea,” the snapshot may be a storage goblin. 🧌

---

## 🧾 Snapshot Log Template

Use this template whenever a new snapshot is taken.

```markdown
## Snapshot: <snapshot-name>

| Item | Details |
|---|---|
| VM | <VM name> |
| Date | YYYY-MM-DD |
| Snapshot Name | `<snapshot-name>` |
| Reason | <Why this snapshot was taken> |
| System State | <What was working at this point> |
| Before / After | Before change / After stable setup |
| Keep or Temporary | Keep / Temporary |
| Notes | <Anything important> |

### Validation Before Snapshot

- [ ] VM boots successfully
- [ ] Network works
- [ ] DNS works if needed
- [ ] Domain connectivity works if applicable
- [ ] Tools open correctly if applicable
- [ ] No sensitive files stored unexpectedly
```

---

## 📋 Current Snapshot Log

Add real entries below as snapshots are taken.

---

## Snapshot: opnsense-working-network-baseline

| Item              | Details                                      |
| ----------------- | -------------------------------------------- |
| VM                | OPNsense                                     |
| Date              | YYYY-MM-DD                                   |
| Snapshot Name     | `opnsense-working-network-baseline`          |
| Reason            | Stable firewall and network baseline         |
| System State      | WAN/LAN working, lab clients can communicate |
| Before / After    | After stable setup                           |
| Keep or Temporary | Keep                                         |
| Notes             | Update after confirming current setup        |

### Validation Before Snapshot

* [ ] OPNsense boots successfully
* [ ] WAN interface works
* [ ] LAN interface works
* [ ] Lab machines can reach gateway
* [ ] DHCP/DNS behavior confirmed if used

---

## Snapshot: dc01-domain-baseline

| Item              | Details                                       |
| ----------------- | --------------------------------------------- |
| VM                | Windows Server / Domain Controller            |
| Date              | YYYY-MM-DD                                    |
| Snapshot Name     | `dc01-domain-baseline`                        |
| Reason            | Stable Active Directory and DNS baseline      |
| System State      | Domain created, DNS working, clients can join |
| Before / After    | After stable setup                            |
| Keep or Temporary | Keep                                          |
| Notes             | Critical rollback point                       |

### Validation Before Snapshot

* [ ] DC boots successfully
* [ ] Static IP configured
* [ ] DNS working
* [ ] AD DS working
* [ ] Domain reachable from client
* [ ] No configuration errors visible

---

## Snapshot: winclient-domain-joined

| Item              | Details                                  |
| ----------------- | ---------------------------------------- |
| VM                | Windows Client                           |
| Date              | YYYY-MM-DD                               |
| Snapshot Name     | `winclient-domain-joined`                |
| Reason            | Stable domain-joined endpoint baseline   |
| System State      | Client joined to domain, DNS working     |
| Before / After    | After domain join                        |
| Keep or Temporary | Keep                                     |
| Notes             | Use before telemetry and detection tests |

### Validation Before Snapshot

* [ ] Client boots successfully
* [ ] Correct IP/DNS assigned
* [ ] Domain login works
* [ ] DC reachable
* [ ] Internet access works if allowed

---

## Snapshot: admin01-domain-joined

| Item              | Details                              |
| ----------------- | ------------------------------------ |
| VM                | Admin Workstation                    |
| Date              | YYYY-MM-DD                           |
| Snapshot Name     | `admin01-domain-joined`              |
| Reason            | Stable admin workstation baseline    |
| System State      | Joined to domain, network working    |
| Before / After    | After domain join                    |
| Keep or Temporary | Keep                                 |
| Notes             | Use before admin behavior simulation |

### Validation Before Snapshot

* [ ] Admin workstation boots successfully
* [ ] Correct IP/DNS assigned
* [ ] Domain login works
* [ ] DC reachable
* [ ] Admin tools ready if installed

---

## Snapshot: flare-clean-analysis-baseline

| Item              | Details                                |
| ----------------- | -------------------------------------- |
| VM                | FLARE VM                               |
| Date              | YYYY-MM-DD                             |
| Snapshot Name     | `flare-clean-analysis-baseline`        |
| Reason            | Clean malware-analysis baseline        |
| System State      | FLARE installed and ready              |
| Before / After    | After setup                            |
| Keep or Temporary | Keep                                   |
| Notes             | Restore after suspicious file analysis |

### Validation Before Snapshot

* [ ] FLARE boots successfully
* [ ] Tools are available
* [ ] Network mode documented
* [ ] No suspicious files stored
* [ ] Shared folders reviewed

---

## Snapshot: remnux-clean-toolkit-baseline

| Item              | Details                               |
| ----------------- | ------------------------------------- |
| VM                | REMnux                                |
| Date              | YYYY-MM-DD                            |
| Snapshot Name     | `remnux-clean-toolkit-baseline`       |
| Reason            | Clean REMnux toolkit baseline         |
| System State      | REMnux tools available                |
| Before / After    | After setup                           |
| Keep or Temporary | Keep                                  |
| Notes             | Use before malware-analysis workflows |

### Validation Before Snapshot

* [ ] REMnux boots successfully
* [ ] Tools available
* [ ] Network mode documented
* [ ] Updates complete if applicable

---

## Snapshot: parrot-clean-testing-baseline

| Item              | Details                                |
| ----------------- | -------------------------------------- |
| VM                | Parrot                                 |
| Date              | YYYY-MM-DD                             |
| Snapshot Name     | `parrot-clean-testing-baseline`        |
| Reason            | Clean security testing baseline        |
| System State      | Parrot ready for lab-only testing      |
| Before / After    | After setup                            |
| Keep or Temporary | Keep                                   |
| Notes             | Use before scanning or network testing |

### Validation Before Snapshot

* [ ] Parrot boots successfully
* [ ] Network works in lab
* [ ] Lab-only boundary confirmed
* [ ] Tools available

---

## Snapshot: sift-clean-forensics-baseline

| Item              | Details                             |
| ----------------- | ----------------------------------- |
| VM                | SIFT                                |
| Date              | YYYY-MM-DD                          |
| Snapshot Name     | `sift-clean-forensics-baseline`     |
| Reason            | Clean forensic workstation baseline |
| System State      | SIFT ready for forensic practice    |
| Before / After    | After setup                         |
| Keep or Temporary | Keep                                |
| Notes             | Use before forensic case work       |

### Validation Before Snapshot

* [ ] SIFT boots successfully
* [ ] Tools available
* [ ] Network mode documented
* [ ] Storage available for evidence work

---

## 🔐 Safety Notes

Do not store in snapshots if avoidable:

* Company files
* Client data
* Credentials
* API keys
* Real incident artifacts
* Sensitive screenshots
* Real malware samples in shared folders
* Uncontrolled downloaded files

For malware-analysis VMs:

* Use isolated mode when needed
* Disable shared folders during risky work
* Restore clean snapshot after analysis
* Do not sync suspicious files to cloud folders
* Do not upload malware samples to GitHub

Snapshot safety rule:

> A dirty snapshot can preserve a dirty problem. Take clean snapshots deliberately. 🧼

---

## ✅ Snapshot Checklist

| Task                                        | Status |
| ------------------------------------------- | ------ |
| OPNsense baseline snapshot created          | ⏳      |
| DC baseline snapshot created                | ⏳      |
| Windows Client baseline snapshot created    | ⏳      |
| Admin Workstation baseline snapshot created | ⏳      |
| Ubuntu baseline snapshot created            | ⏳      |
| FLARE baseline snapshot created             | ⏳      |
| REMnux baseline snapshot created            | ⏳      |
| Parrot baseline snapshot created            | ⏳      |
| SIFT baseline snapshot created              | ⏳      |
| Snapshot names documented                   | ⏳      |
| Snapshot purpose documented                 | ⏳      |
| Temporary snapshots reviewed                | ⏳      |
| Old/unclear snapshots cleaned               | ⏳      |

---

## 🏁 Final Note

Snapshots are not glamorous.

They do not write detections.

They do not hunt threats.

They do not reverse malware.

But when the lab breaks, snapshots become tiny golden parachutes. 🪂

A good snapshot strategy makes future experiments safer, faster, and more repeatable.

The lab can break.

The VM can sulk.

The network can forget its own address.

But with clean snapshots, the kingdom can rewind. 🔁🏰

