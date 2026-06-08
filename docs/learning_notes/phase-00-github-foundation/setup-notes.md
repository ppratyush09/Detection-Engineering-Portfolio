# 🛠️ Phase 00: GitHub Foundation Setup Notes

> “The first commit is not just a commit. It is the moment the repo stops being an empty cave and becomes a workshop.” 🔨📚

This file documents the setup process for my Detection Engineering Portfolio repository.

Phase 00 is focused on learning GitHub basics, creating a clean repository structure, writing useful README files, documenting mistakes, and preparing the repo for future detection engineering work.

This phase is not about perfect detections yet.

This phase is about building the table where the detections will eventually sit like tiny alert sandwiches. 🥪🚨

---

## 🎯 Phase Objective

The objective of this phase is to create a clean GitHub foundation for:

* Detection engineering rules
* Sigma rules
* KQL hunting queries
* YARA rules
* Suricata rules
* Python helper scripts
* Malware analysis notes
* Lab architecture documentation
* Phase-wise learning notes
* Detection validation reports
* Future GitHub Actions and detection-as-code practice

The repository should show:

> I can organize security work clearly, document my process, and build a public portfolio safely.

---

## 🧭 Starting Point

At the beginning of this phase, I had very little practical GitHub experience.

Main questions:

* What should I put in a GitHub repository?
* How should folders be structured?
* What should go in README files?
* How do I create folders in GitHub?
* Should I include Sigma, KQL, YARA, Suricata, and Python?
* How do I document my lab setup?
* What should be kept out of a public repository?
* How do I make this useful for Detection Engineering and Threat Research roles?

This phase answers those questions step by step.

---

## 🏗️ Repository Created

Repository name:

```text
Detection-Engineering-Portfolio
```

Repository purpose:

```text
A hands-on Detection Engineering portfolio containing lab notes, Sigma rules, KQL queries, YARA rules, Suricata rules, Python scripts, malware analysis notes, and phase-wise learning documentation.
```

Repository visibility:

```text
Public
```

Reason for public visibility:

* Build a professional portfolio
* Show structured learning
* Demonstrate practical detection engineering work
* Make rules and notes reviewable by others
* Create proof of hands-on effort

Important safety decision:

> Public does not mean careless. Public means sanitized, structured, and safe. 🔐

---

## 🧾 Repository Description

The repository description was written to quickly explain the purpose of the project.

Suggested description:

```text
Hands-on detection engineering portfolio with Sigma, KQL, YARA, Suricata rules, lab notes, validation writeups, and detection-as-code practice.
```

Why this description works:

* Short
* Professional
* Clear
* Role-aligned
* Mentions important detection engineering skills
* Immediately tells visitors what the repository contains

---

## 📘 Root README Setup

The root `README.md` was created first.

Purpose of root README:

* Introduce the repository
* Explain focus areas
* Explain folder structure
* Mention safety rules
* Show current learning direction
* Make the repo look intentional from the first page

Key sections added:

* Project title
* Focus areas
* Repository structure
* Current lab goal
* Safety notice
* Current status
* Author

Why this matters:

> The root README is the front gate of the repository.
> If it is empty, visitors walk into the repo wearing confusion goggles. 🥽

---

## 📁 Folder Creation Method

Important GitHub lesson:

> GitHub does not show empty folders by default.

To create a folder, I created a file inside a folder path.

Example:

```text
docs/lab-architecture.md
```

This created:

```text
docs/
└── lab-architecture.md
```

This method was used for all major folders.

Steps followed:

1. Clicked **Add file**
2. Selected **Create new file**
3. Typed folder path and filename
4. Added Markdown content
5. Committed the file

Example path:

```text
learning-notes/phase-00-github-foundation/setup-notes.md
```

Tiny GitHub rule:

> No file, no folder. GitHub wants proof of life. 📜

---

## 🧱 Core Repository Structure

The repository was organized into major sections.

```text
Detection-Engineering-Portfolio/
├── README.md
├── docs/
├── kql/
├── sigma/
├── yara/
├── suricata/
├── python/
├── reports/
├── tests/
└── learning-notes/
```

Each folder has a specific purpose.

| Folder            | Purpose                                                   |
| ----------------- | --------------------------------------------------------- |
| `docs/`           | Lab architecture, learning log, and general documentation |
| `kql/`            | KQL hunting queries                                       |
| `sigma/`          | Sigma detection rules                                     |
| `yara/`           | YARA rules for file-pattern detection                     |
| `suricata/`       | Suricata network detection rules                          |
| `python/`         | Python automation and helper scripts                      |
| `reports/`        | Detection writeups and analysis reports                   |
| `tests/`          | Safe test notes and validation data                       |
| `learning-notes/` | Phase-wise learning and lab setup notes                   |

---

## 📚 Documentation Files Created

The first documentation files were created to explain the repository and lab.

| File                                               | Purpose                                          |
| -------------------------------------------------- | ------------------------------------------------ |
| `docs/lab-architecture.md`                         | Documents the home lab architecture and VM roles |
| `docs/learning-log.md`                             | Tracks learning progress and skill development   |
| `kql/README.md`                                    | Explains KQL folder usage and query standards    |
| `sigma/README.md`                                  | Explains Sigma rule writing approach             |
| `yara/README.md`                                   | Explains YARA rule development and safety        |
| `suricata/README.md`                               | Explains Suricata network detection rules        |
| `python/README.md`                                 | Explains Python’s role in detection engineering  |
| `learning-notes/README.md`                         | Explains phase-wise learning documentation       |
| `phase-00-github-foundation/README.md`             | Explains Phase 00                                |
| `phase-00-github-foundation/checklist.md`          | Tracks Phase 00 tasks                            |
| `phase-00-github-foundation/mistakes-and-fixes.md` | Documents issues and lessons                     |
| `phase-00-github-foundation/setup-notes.md`        | Documents the setup process                      |

---

## 🧪 Lab Architecture Documentation

The lab architecture file was created to document the home lab design.

Included systems:

| System              | Purpose                                     |
| ------------------- | ------------------------------------------- |
| OPNsense            | Firewall, routing, segmentation             |
| Windows Server / DC | Active Directory and domain telemetry       |
| Windows Client      | Endpoint testing and log generation         |
| Admin Workstation   | Admin activity and PowerShell testing       |
| Ubuntu Server       | Future logging, scripts, and tools          |
| FLARE VM            | Windows malware analysis                    |
| REMnux              | Linux malware analysis and IOC extraction   |
| Parrot              | Security testing and threat hunting support |
| SIFT                | Digital forensics and timeline analysis     |

Why this matters:

> A lab should not be a random zoo of VMs.
> Each system should have a purpose, a role, and a reason to exist. 🧪

---

## 🧠 Learning Log Setup

The learning log was created to track progress.

Purpose:

* Record what I learned
* Track tools and skills
* Capture mistakes
* Track planned work
* Document skill growth
* Keep future learning structured

Main areas tracked:

* GitHub basics
* Lab setup
* Sigma
* KQL
* YARA
* Suricata
* Python
* Malware analysis
* Digital forensics
* Detection-as-code

Why this matters:

> Learning without notes becomes fog.
> Learning with notes becomes a trail. 🐾

---

## 🛡️ Sigma Section Setup

Created:

```text
sigma/README.md
```

Purpose:

* Explain Sigma rule writing
* Document rule structure
* Define folder organization
* Add quality checklist
* Define naming standards
* Explain false positive thinking
* Connect Sigma with KQL and reports

Planned Sigma areas:

```text
sigma/windows/process_creation/
sigma/windows/powershell/
sigma/windows/account_activity/
sigma/windows/lateral_movement/
sigma/windows/ransomware_precursors/
```

Sigma learning goal:

> Turn suspicious behavior into structured detection logic. 🛡️

---

## 🔍 KQL Section Setup

Created:

```text
kql/README.md
```

Purpose:

* Explain KQL hunting queries
* Define query style
* Document metadata comments
* List investigation fields
* Connect KQL with Sigma
* Plan query categories

Planned KQL areas:

```text
kql/windows/
kql/defender/
kql/sentinel/
```

KQL learning goal:

> Ask logs better questions and turn telemetry into investigation answers. 🔦

---

## 🧬 YARA Section Setup

Created:

```text
yara/README.md
```

Purpose:

* Explain YARA rule development
* Document YARA structure
* Define safe testing approach
* Add rule quality checklist
* Explain false positives
* Connect YARA to malware analysis

Planned YARA areas:

```text
yara/windows/
yara/documents/
yara/malware_patterns/
yara/lab_testing/
```

YARA learning goal:

> Detect suspicious file patterns safely and clearly. 🧬

---

## 🌐 Suricata Section Setup

Created:

```text
suricata/README.md
```

Purpose:

* Explain Suricata rules
* Document rule anatomy
* Define custom SID ranges
* Add network detection goals
* Connect network alerts with endpoint telemetry
* Plan suspicious outbound, DNS, HTTP, and scanning detections

Planned Suricata areas:

```text
suricata/suspicious_outbound/
suricata/dns/
suricata/http/
suricata/scanning/
suricata/lab_testing/
```

Suricata learning goal:

> Detect suspicious network behavior and turn packet trails into investigation clues. 🦈

---

## 🐍 Python Section Setup

Created:

```text
python/README.md
```

Purpose:

* Explain Python’s role in detection engineering
* Plan automation scripts
* Define scripting standards
* Add safety rules
* Connect Python with rule validation and IOC extraction

Planned scripts:

```text
ioc_extractor.py
log_field_profiler.py
sigma_metadata_checker.py
yara_rule_runner.py
suspicious_command_parser.py
```

Python learning goal:

> Automate repetitive detection engineering tasks so the human brain can focus on the spicy thinking. 🧠🌶️

---

## 📚 Phase-wise Learning Notes Setup

Created:

```text
learning-notes/
```

Purpose:

* Track learning in phases
* Document setup work
* Record mistakes and fixes
* Keep lab setup notes organized
* Show progression over time

Initial phase created:

```text
learning-notes/phase-00-github-foundation/
```

Files inside Phase 00:

```text
README.md
checklist.md
mistakes-and-fixes.md
setup-notes.md
```

Planned future phases:

```text
phase-01-lab-foundation/
phase-02-windows-telemetry/
phase-03-sigma-and-kql/
phase-04-yara-and-malware-analysis/
phase-05-suricata-and-network-detection/
phase-06-python-for-detection-engineering/
phase-07-detection-as-code/
phase-08-threat-research-projects/
```

Why this matters:

> A phase-wise structure shows growth, not just output.
> It tells the story of how the skills were built. 📈

---

## ⚙️ GitHub Actions Lesson

A workflow file was created early:

```text
.github/workflows/validate.yml
```

A failure notification appeared.

Lesson learned:

> GitHub Actions is useful, but it should be added after the repository has stable content and clear validation goals.

Decision:

```text
Delay GitHub Actions until the Detection-as-Code phase.
```

Why:

* Avoid noisy failures
* Learn GitHub basics first
* Add CI/CD when rules and validation requirements are clearer
* Prevent automation from becoming a confusion cannon

Tiny DevOps wisdom:

> Do not automate confusion. It just runs faster. ⚙️💥

---

## 🔐 Public Repository Safety Rules

Since this is a public repository, strict safety rules were defined.

Do not upload:

* Company data
* Client logs
* Credentials
* API keys
* Tokens
* Real malware samples
* Password-protected malware ZIP files
* Proprietary detections
* Private incident reports
* Sensitive screenshots
* Production hostnames
* Internal work IPs
* Confidential investigation data

Allowed content:

* Lab-generated notes
* Synthetic examples
* Sanitized screenshots
* Public-learning references
* Personal detection rules
* Safe test files
* Methodology
* Checklists
* Writeups without sensitive data

Golden rule:

> Show skill, not secrets. 🔐

---

## 🏷️ Naming Conventions

Naming rules were created to keep the repository clean.

### README files

Use:

```text
README.md
```

### Markdown notes

Use lowercase with hyphens:

```text
lab-architecture.md
learning-log.md
setup-notes.md
mistakes-and-fixes.md
```

### Rules and scripts

Use lowercase with underscores:

```text
suspicious_powershell_encoded_command.yml
suspicious_script_obfuscation.yar
suspicious_user_agent.rules
ioc_extractor.py
```

Why this matters:

> Clean names reduce future folder archaeology.
> Nobody wants to investigate `final-final-real-one-use-this.md`. 🪦

---

## 🧾 Commit Message Style

Simple commit messages were used.

Examples:

```text
Initial README setup
Add KQL section README
Add Sigma section README
Add YARA section README
Add Suricata section README
Add Python section README
Add phase-wise learning notes README
Add Phase 00 GitHub foundation checklist
Add Phase 00 mistakes and fixes notes
Add Phase 00 setup notes
```

Commit message rule:

> Short, clear, and specific.

Bad commit messages to avoid:

```text
Update
Changes
Stuff
Final
Please work
```

Emotionally valid, professionally weak. 😅

---

## 🧠 Key Things Learned

During this setup, I learned:

* GitHub repositories need structure
* README files are important
* GitHub creates folders through file paths
* Public repositories need strict safety rules
* Detection Engineering portfolios should include notes, rules, and validation
* Python is useful for detection engineering automation
* Malware analysis should be included safely
* GitHub Actions should come later
* Phase-wise learning makes progress visible
* Documentation is a skill, not an afterthought

---

## ✅ Phase 00 Setup Summary

| Area                               | Status |
| ---------------------------------- | ------ |
| Repository created                 | ✅ Done |
| Repository description added       | ✅ Done |
| Root README created                | ✅ Done |
| Core folders created               | ✅ Done |
| Section README files added         | ✅ Done |
| Lab architecture documented        | ✅ Done |
| Learning log created               | ✅ Done |
| Phase-wise learning folder created | ✅ Done |
| Phase 00 checklist created         | ✅ Done |
| Mistakes and fixes documented      | ✅ Done |
| Setup notes created                | ✅ Done |
| GitHub Actions delayed             | ✅ Done |
| Malware analysis planning started  | ✅ Done |
| Public safety rules defined        | ✅ Done |

---

## 🚀 Next Step After Phase 00

After completing Phase 00, the next phase should be:

```text
Phase 01: Lab Foundation
```

Focus of Phase 01:

* Document the actual lab setup
* Record VM details
* Document network layout
* Track snapshots
* Document troubleshooting
* Prepare telemetry sources
* Connect lab activity to detection goals

Suggested next files:

```text
learning-notes/phase-01-lab-foundation/README.md
learning-notes/phase-01-lab-foundation/vm-inventory.md
learning-notes/phase-01-lab-foundation/network-setup.md
learning-notes/phase-01-lab-foundation/snapshot-notes.md
learning-notes/phase-01-lab-foundation/troubleshooting.md
```

---

## 🏁 Final Note

Phase 00 built the foundation.

Not the detections.

Not the pipelines.

Not the malware reports.

The foundation.

The place where everything else can grow without becoming a tangled jungle of files, half-written notes, and mystery YAML.

The repo now has:

* A purpose
* A structure
* A learning path
* Documentation standards
* Safety rules
* Phase-wise notes
* A clear next step

That is a good start.

The workshop is open.

The tools are labeled.

The alert owls are still babies, but they have a home. 🦉🚨

