# 🧯 Phase 00: Mistakes and Fixes

> “Every setup error is just a tiny goblin asking for documentation.” 🧌📚

This file tracks the mistakes, confusing moments, small errors, and useful fixes I encountered while setting up my GitHub repository for Detection Engineering.

The goal is not to pretend everything went perfectly.

The goal is to show that I can:

* Notice issues
* Understand what caused them
* Fix them safely
* Document the lesson
* Avoid repeating the same chaos soup later 🍲

---

## 🎯 Purpose

This file exists because mistakes are part of engineering.

A clean portfolio should not only show final results. It should also show learning discipline.

This document captures:

* What went wrong
* What I saw
* Why it happened
* How I fixed it
* What I learned
* How I will prevent it next time

Tiny philosophy:

> A mistake without documentation becomes folklore.
> A mistake with documentation becomes experience. 🧠

---

## 🧾 Mistake Log

| # | Issue                                           | Status    | Lesson                                                                   |
| - | ----------------------------------------------- | --------- | ------------------------------------------------------------------------ |
| 1 | Unsure what to put in the GitHub repository     | ✅ Fixed   | Start with structure, README files, and safe documentation               |
| 2 | Unsure how to create folders in GitHub          | ✅ Fixed   | GitHub creates folders when a file is created inside a path              |
| 3 | GitHub Actions workflow failed                  | ✅ Learned | Do not add CI/CD before understanding the basics                         |
| 4 | Unsure whether Python belongs in the repo       | ✅ Decided | Python is useful for automation, parsing, IOC extraction, and validation |
| 5 | Needed separate READMEs for each section        | ✅ Fixed   | Every major folder should explain its purpose                            |
| 6 | Needed a phase-wise notes area                  | ✅ Fixed   | Learning should be documented in phases                                  |
| 7 | Needed safe malware-analysis documentation plan | ✅ Learned | Upload methodology, reports, and rules, not malware samples              |

---

# 1. Issue: “What should I even put in this repository?” 🤔

## What Happened

At the start, I had a GitHub repository but was unsure what should go inside it.

The first confusion was:

> Should this repo contain only rules?
> Should it contain notes?
> Should it include Python?
> Should malware analysis be separate?
> Will this look professional or messy?

Classic beginner GitHub fog. Very dramatic. Slightly damp. 🌫️

---

## Why It Happened

GitHub can be used in many ways:

* Code storage
* Documentation
* Portfolio
* Detection rule library
* Lab notes
* Research writeups
* Automation scripts

Because this repository is for Detection Engineering, it needed a structure that supports multiple skill areas instead of becoming a random dumping ground.

---

## Fix Applied

Created a structured repository layout:

```text
docs/
kql/
sigma/
yara/
suricata/
python/
reports/
tests/
learning-notes/
```

Each folder was given a clear purpose.

---

## Lesson Learned

A Detection Engineering portfolio should show both:

* Technical artifacts
* Thinking process

So the repo should include:

* Rules
* Queries
* Scripts
* Writeups
* Lab documentation
* Learning notes
* Safety rules
* Validation notes

A repo without structure is just a digital attic.

And nobody hires an attic. 🏚️

---

# 2. Issue: “How do I create folders in GitHub?” 📁

## What Happened

I wanted to create directories like:

```text
docs/
sigma/
kql/
yara/
suricata/
python/
```

But GitHub’s web interface does not create empty folders in the usual way.

---

## Why It Happened

Git tracks files, not empty folders.

So an empty folder is like a ghost chair.

You believe in it, but GitHub refuses to show it. 👻🪑

---

## Fix Applied

Created a file inside each folder path.

Example:

```text
docs/lab-architecture.md
```

This automatically created:

```text
docs/
└── lab-architecture.md
```

Same method used for:

```text
kql/README.md
sigma/README.md
yara/README.md
suricata/README.md
python/README.md
learning-notes/README.md
```

---

## Lesson Learned

To create a folder in GitHub web UI:

1. Click **Add file**
2. Click **Create new file**
3. Type the folder path and file name
4. Add content
5. Commit the file

Example:

```text
learning-notes/phase-00-github-foundation/checklist.md
```

Tiny rule:

> No file, no folder. GitHub demands tribute. 📜

---

# 3. Issue: GitHub Actions Workflow Failed ⚙️💥

## What Happened

A notification appeared saying the workflow failed:

```text
.github/workflows/validate.yml workflow run failed
```

At first, this looked scary.

The repo had just started, and suddenly GitHub was waving a red flag like a tiny DevOps referee.

---

## Why It Happened

A GitHub Actions workflow file was created too early.

Possible reasons for failure:

* Invalid YAML syntax
* Commands inside the workflow were not ready
* Validation tools were not installed
* The repository did not yet have stable rule content
* CI/CD was added before the foundation was ready

---

## Fix Applied

Decision made:

```text
Delay GitHub Actions until later.
```

For now, focus on:

* Repository structure
* README files
* Documentation
* Rules
* Queries
* Scripts
* Validation notes

GitHub Actions will be added later during the Detection-as-Code phase.

---

## Lesson Learned

GitHub Actions is useful, but timing matters.

CI/CD should come after:

* Rules exist
* Folder structure is stable
* Validation goals are clear
* Tools are understood

Do not automate confusion.

That just creates faster confusion. 🏃‍♂️💨

---

# 4. Issue: “Should Python be added?” 🐍

## What Happened

I wondered whether Python should be part of this repository because my main goal is Detection Engineering and Threat Research.

---

## Why It Happened

At first glance, Detection Engineering may look like:

```text
Sigma + KQL + YARA + Suricata
```

But real detection work often needs automation.

Python helps with:

* IOC extraction
* Log parsing
* CSV/JSON handling
* Rule validation
* Metadata checks
* YARA scanning
* Report generation
* Repetitive analysis tasks

---

## Fix Applied

Created a Python section:

```text
python/
├── README.md
└── scripts/
```

Planned scripts include:

```text
ioc_extractor.py
log_field_profiler.py
sigma_metadata_checker.py
yara_rule_runner.py
suspicious_command_parser.py
```

---

## Lesson Learned

Python is not replacing detection rules.

Python supports the detection workflow.

Tiny summary:

> Sigma detects behavior.
> KQL hunts through logs.
> YARA inspects files.
> Suricata watches packets.
> Python carries the boring buckets. 🪣

---

# 5. Issue: “Do we need separate README files everywhere?” 📚

## What Happened

As folders were created, it became clear that each major section needed its own explanation.

Without README files, folders can feel empty or confusing.

---

## Why It Happened

A folder name alone does not explain:

* What belongs there
* What should not belong there
* How files should be named
* What the learning goal is
* How the folder connects to Detection Engineering

Example:

```text
yara/
```

This tells me the topic.

But it does not explain:

* Safety rules
* Rule format
* Testing approach
* False positives
* How YARA connects to malware analysis

---

## Fix Applied

Added README files for major sections:

```text
kql/README.md
sigma/README.md
yara/README.md
suricata/README.md
python/README.md
learning-notes/README.md
```

Each README explains:

* Purpose
* Folder structure
* Use cases
* Safety rules
* Planned work
* Quality checklist
* Relationship with other folders

---

## Lesson Learned

README files are not decoration.

They are signboards.

Without them, visitors walk into the repo and whisper:

> “Where am I, and why is YAML staring at me?” 👀

---

# 6. Issue: Needed Phase-wise Learning Notes 🧭

## What Happened

The repository had technical sections, but I also wanted a dedicated place for learning and lab setup notes.

This was needed because the journey includes:

* GitHub basics
* Lab setup
* Windows telemetry
* Sigma and KQL
* YARA and malware analysis
* Suricata
* Python
* Detection-as-code
* Threat research projects

---

## Why It Happened

A Detection Engineering journey is not one single task.

It is a staircase.

Each phase builds on the previous one.

Without phase-wise notes, learning can become scattered across random files.

Random notes are sneaky.

They multiply in corners. 🐁

---

## Fix Applied

Created:

```text
learning-notes/
```

Inside it, created:

```text
phase-00-github-foundation/
```

With files:

```text
README.md
checklist.md
mistakes-and-fixes.md
```

Planned future phase folders:

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

---

## Lesson Learned

Phase-wise notes show progression.

They answer:

* What did I learn first?
* What did I build next?
* What problems did I solve?
* How did my skills improve?
* How does this connect to job readiness?

This turns the repo from a file cabinet into a learning trail. 🐾

---

# 7. Issue: Malware Analysis Scope Was Unclear 🧬

## What Happened

I wanted to include malware analysis because it is important for Threat Researcher and Detection Engineering roles.

The question was:

> Should I do dynamic analysis?
> How much?
> What can be safely uploaded to GitHub?

---

## Why It Happened

Malware analysis is sensitive.

There is a difference between:

* Learning malware analysis safely
* Uploading dangerous samples
* Sharing sensitive indicators
* Publishing unsafe content
* Creating useful detection logic

The repo should show skill, not risk.

---

## Fix Applied

Decided that the malware-analysis section should include:

* Methodology
* Checklists
* Safe reports
* IOC extraction notes
* Behavior-to-detection mapping
* YARA development notes
* Safety rules

It should not include:

* Real malware samples
* Password-protected malware ZIPs
* Client files
* Company data
* Real incident screenshots
* Proprietary indicators

---

## Lesson Learned

Malware analysis in this repo should say:

> “I can analyze behavior safely and convert findings into detections.”

Not:

> “Welcome to my public malware aquarium.” 🐟🧨

---

# 8. Issue: File and Folder Naming Consistency 🏷️

## What Happened

As folders and files were created, naming consistency became important.

Some names could become confusing if not standardized.

Example problems to avoid:

```text
ReadMe.md
README.md
readme.md
test-final.md
mynewquery.md
SigmaRule1.yml
```

---

## Why It Happened

GitHub displays files clearly, but inconsistent naming makes repositories look messy.

For a portfolio, naming matters because it reflects discipline.

---

## Fix Applied

Use simple naming conventions:

### README files

```text
README.md
```

### Markdown notes

```text
lowercase-with-hyphens.md
```

Example:

```text
lab-architecture.md
learning-log.md
mistakes-and-fixes.md
setup-notes.md
```

### Rules and scripts

```text
lowercase_with_underscores.ext
```

Examples:

```text
suspicious_powershell_encoded_command.yml
suspicious_script_obfuscation.yar
suspicious_user_agent.rules
ioc_extractor.py
```

---

## Lesson Learned

Good naming prevents future folder archaeology.

Future me should not have to dig through:

```text
final2-real-final-use-this-one.md
```

That filename has panic energy. 😅

---

# 9. Issue: Unsure What Counts as Safe Public Content 🔐

## What Happened

Because this repository is public, I needed to define what is allowed and what is forbidden.

---

## Why It Happened

Security work often involves sensitive information.

Even accidental exposure can be serious.

Public GitHub is not a private notebook.

It is a glass display case with a search bar. 🔎

---

## Fix Applied

Created safety rules across documentation.

Allowed:

* Lab-created notes
* Synthetic examples
* Sanitized outputs
* Personal learning notes
* Public references
* Detection rules written from my own understanding
* Dummy indicators
* Methodology and checklists

Forbidden:

* Company data
* Client logs
* Credentials
* API keys
* Real malware samples
* Proprietary detections
* Production screenshots
* Private incident data
* Sensitive hostnames or usernames

---

## Lesson Learned

Safety is part of professionalism.

The repository should demonstrate:

```text
Skill
Structure
Discipline
Ethics
```

Not:

```text
Oops
Leak
Panic
Delete
```

---

# 10. Issue: Too Much Too Soon Risk 🚦

## What Happened

There are many areas to learn:

* GitHub
* Sigma
* KQL
* YARA
* Suricata
* Python
* Malware analysis
* Dynamic analysis
* Forensics
* Detection-as-code
* Threat research

It is easy to try adding everything at once.

---

## Why It Happened

Detection Engineering is broad.

Threat Research is broad.

Malware Analysis is broad.

Together, they can become a hydra with certifications. 🐍

---

## Fix Applied

Created phase-wise learning approach.

Current focus:

```text
Phase 00: GitHub Foundation
```

Later phases:

```text
Phase 01: Lab Foundation
Phase 02: Windows Telemetry
Phase 03: Sigma and KQL
Phase 04: YARA and Malware Analysis
Phase 05: Suricata and Network Detection
Phase 06: Python for Detection Engineering
Phase 07: Detection-as-Code
Phase 08: Threat Research Projects
```

---

## Lesson Learned

Do not boil the ocean.

Boil one suspicious teacup at a time. ☕

---

## 🧠 General Lessons From Phase 00

* GitHub is less scary when the repo has a clear map.
* README files are important.
* Empty folders need files inside them.
* GitHub Actions should wait until the repo is ready.
* Python belongs in a detection engineering portfolio.
* Malware analysis belongs, but safely.
* Documentation is part of engineering.
* Mistakes are useful when recorded.
* Structure makes learning visible.
* Public repos need strict safety rules.
* Future me deserves readable notes.

---

## ✅ Phase 00 Fix Summary

| Area                   | Fix Applied                           |
| ---------------------- | ------------------------------------- |
| Repository confusion   | Created clear folder structure        |
| Empty folder issue     | Created files inside folder paths     |
| Workflow failure       | Delayed GitHub Actions                |
| Python uncertainty     | Added Python section                  |
| Section clarity        | Added README files                    |
| Learning tracking      | Added phase-wise notes                |
| Malware analysis scope | Planned safe methodology-based folder |
| Naming consistency     | Created naming rules                  |
| Public safety          | Added strict safety rules             |

---

## 🏁 Final Note

Phase 00 was not about writing elite detections.

It was about building the workshop.

The benches are in place.

The labels are on the drawers.

The YAML has a home.

The logs have a future.

The mistakes have been documented instead of being left to haunt the hallway. 👻

Next phase can now focus on building the lab and producing detection content with a cleaner foundation.

And if something breaks again?

Good.

That means there will be more notes. 📚🔥

