# 📚 Phase-wise Learning Notes: Building the Detection Lab One Goblin at a Time

> “First I broke the lab. Then I fixed the lab. Then I documented the lab. That is basically engineering.” 🛠️📜

This folder contains my phase-by-phase learning notes for detection engineering, threat hunting, malware analysis, digital forensics, Python automation, and lab setup.

The purpose of this folder is to document not only the final working setup, but also the learning journey behind it.

Because the real skill is not just knowing what works.

The real skill is knowing:

* What I tried
* What broke
* Why it broke
* How I fixed it
* What I learned
* How it helps detection engineering

Future me deserves clean notes, not ancient cyber riddles written in panic. 🧠

---

## 🎯 Purpose

This section is used to track my learning in phases.

Each phase contains:

* Setup notes
* Tool notes
* Configuration steps
* Mistakes and fixes
* Screenshots or diagrams when safe
* Detection ideas
* Validation notes
* Lessons learned

The goal is to build a practical, hands-on portfolio that shows structured progress toward becoming stronger in:

* Detection Engineering
* Threat Hunting
* Incident Response
* Malware Analysis
* Threat Research
* Digital Forensics
* Detection-as-Code

---

## 🧭 Phase Map

| Phase    | Focus                            | Goal                                                                            |
| -------- | -------------------------------- | ------------------------------------------------------------------------------- |
| Phase 00 | GitHub Foundation                | Learn repository structure, Markdown, commits, and documentation                |
| Phase 01 | Lab Foundation                   | Build the core home lab with firewall, domain, clients, and analysis VMs        |
| Phase 02 | Windows Telemetry                | Understand event logs, Sysmon, PowerShell logs, and useful Windows data sources |
| Phase 03 | Sigma and KQL                    | Write behavior-based detections and hunting queries                             |
| Phase 04 | YARA and Malware Analysis        | Learn safe malware triage, file indicators, and YARA rule development           |
| Phase 05 | Suricata and Network Detection   | Write network detection rules and analyze suspicious traffic                    |
| Phase 06 | Python for Detection Engineering | Build helper scripts for IOC extraction, parsing, and automation                |
| Phase 07 | Detection-as-Code                | Learn GitHub Actions and automated rule validation                              |
| Phase 08 | Threat Research Projects         | Convert public threat behavior into detections and writeups                     |

---

## 🏗️ Folder Structure

```text
learning-notes/
├── phase-00-github-foundation/
├── phase-01-lab-foundation/
├── phase-02-windows-telemetry/
├── phase-03-sigma-and-kql/
├── phase-04-yara-and-malware-analysis/
├── phase-05-suricata-and-network-detection/
├── phase-06-python-for-detection-engineering/
├── phase-07-detection-as-code/
└── phase-08-threat-research-projects/
```

Each phase will include notes, checklists, mistakes, fixes, and practical outcomes.

---

## 🧪 How I Will Use These Notes

For every phase, I will try to document:

| Section            | What It Captures                                 |
| ------------------ | ------------------------------------------------ |
| Objective          | What I am trying to learn                        |
| Setup              | What I configured or installed                   |
| Tools Used         | VMs, software, scripts, or platforms used        |
| What Worked        | Successful steps                                 |
| What Broke         | Errors, confusion, failed attempts               |
| Fixes              | How I solved issues                              |
| Security Relevance | Why this matters for detection engineering       |
| Detection Ideas    | Rules or queries that can come from the activity |
| Lessons Learned    | Important takeaways                              |

---

## 🧰 Lab Machines Covered

This learning folder may include notes for:

| Machine             | Purpose                                                             |
| ------------------- | ------------------------------------------------------------------- |
| OPNsense            | Firewall, routing, segmentation, and network visibility             |
| Windows Server / DC | Active Directory, authentication, and domain telemetry              |
| Windows Client      | Endpoint testing and log generation                                 |
| Admin Workstation   | Admin behavior simulation and PowerShell testing                    |
| Ubuntu Server       | Utility server, logging, scripting, or future SIEM experiments      |
| FLARE VM            | Windows malware analysis and reverse engineering toolkit            |
| REMnux              | Linux malware analysis, decoding, and IOC extraction                |
| Parrot              | Security testing, threat hunting, and controlled traffic generation |
| SIFT                | Digital forensics, timeline analysis, and artifact review           |

---

## 🧠 Note-taking Rules

1. **Document the why**

   * Not just what I clicked, but why I clicked it.

2. **Record mistakes**

   * Mistakes are part of the lab. They are just lessons wearing fake mustaches. 🥸

3. **Keep sensitive data out**

   * No company data, no client logs, no credentials, no private screenshots.

4. **Use screenshots carefully**

   * Blur or avoid hostnames, usernames, tokens, and anything sensitive.

5. **Connect setup to detection**

   * Every lab setup should eventually help answer: “What can I detect from this?”

6. **Keep notes readable**

   * Future me should not need a decoder ring.

---

## 🔐 Safety Rules

This folder must not contain:

* Company data
* Client data
* Credentials
* API keys
* Production logs
* Private investigation details
* Real malware samples
* Sensitive screenshots
* Proprietary detections

Allowed content:

* Personal lab notes
* Safe screenshots
* Sanitized examples
* Public-learning references
* Lab-generated observations
* Personal troubleshooting notes
* Detection ideas written from my own practice

Golden rule:

> Show the learning. Do not leak the kingdom. 🔐

---

## 🏁 Final Note

This folder is my learning trail.

Every note is a breadcrumb.

Every fix is a checkpoint.

Every phase is one step closer to becoming better at turning suspicious behavior into clear, tested, explainable detections.

The lab may break.

The logs may mumble.

The YAML may betray me.

But the notes will survive. 📚🔥

