# 📚 Learning Log: Journey of a Future Threat Detective 🕵️‍♂️💻

> “I came. I saw. I Googled. I documented.” 📜
> This file tracks my learning journey in detection engineering, threat hunting, malware analysis, digital forensics, and detection-as-code.

This is not just a progress tracker.

This is my cyber training journal, where every tiny win, broken command, confusing error, and “wait, why did that work?” moment gets documented.

Because future me deserves breadcrumbs. 🍞

---

## 🎯 Purpose

The purpose of this learning log is to track:

* What I learned
* What I built
* What confused me
* What broke
* What I fixed
* What I need to revisit
* What turned into a useful detection idea

The goal is simple:

> Learn by doing.
> Break safely.
> Detect clearly.
> Document honestly.
> Improve consistently.

This log is proof that skills are not downloaded into the brain like software updates. They are built through repetition, curiosity, caffeine, screenshots, errors, and tiny victories. ☕⚙️

---

## 🧭 Current Learning Direction

My current focus is building hands-on capability in:

| Area                      | Current Goal                                                    |
| ------------------------- | --------------------------------------------------------------- |
| 🛡️ Detection Engineering | Write practical Sigma, KQL, YARA, and Suricata detections       |
| 🔎 Threat Hunting         | Understand attacker behavior and turn hypotheses into queries   |
| 🚨 Incident Response      | Investigate suspicious activity and document clear findings     |
| 🧬 Malware Analysis       | Learn safe file analysis using FLARE and REMnux                 |
| 🧾 Digital Forensics      | Use SIFT to understand artifacts and timelines                  |
| 🐍 Python Automation      | Automate IOC extraction, parsing, and validation tasks          |
| ⚙️ Detection-as-Code      | Use GitHub to organize, version, and eventually test detections |

---

## 🧪 Current Lab Stack

This is the current lab kingdom where the learning happens.

| Machine / Tool         | Role                            | Learning Use                                                         |
| ---------------------- | ------------------------------- | -------------------------------------------------------------------- |
| 🔥 OPNsense            | Firewall and network gateway    | Network segmentation, firewall logs, traffic control                 |
| 🪟 Windows Server / DC | Domain Controller               | Active Directory, authentication, domain telemetry                   |
| 💻 Windows Client      | Endpoint                        | Process creation, user activity, detection validation                |
| 🧙 Admin Workstation   | Admin simulation box            | PowerShell testing, admin behavior, remote activity                  |
| 🐧 Ubuntu Server       | Utility server                  | Future log collection, scripts, tools, and SIEM experiments          |
| 🔥 FLARE VM            | Windows malware analysis lab    | Static analysis, PE review, suspicious script inspection, YARA ideas |
| 🧊 REMnux VM           | Linux malware analysis toolkit  | IOC extraction, decoding, unpacking, network artifact review         |
| 🦜 Parrot VM           | Security testing and hunting VM | Controlled testing, recon simulation, network checks                 |
| 🔎 SIFT VM             | Digital forensics workstation   | Timeline analysis, artifact review, forensic investigation practice  |
| 📁 GitHub              | Portfolio and version control   | Documentation, rule storage, scripts, writeups                       |

Tiny summary:

> Windows gives me logs.
> Linux gives me tools.
> GitHub gives me memory.
> Errors give me character. 🧃

---

## 🛰️ Skills on My Radar

| Skill             | Why It Matters                        | Current Status |
| ----------------- | ------------------------------------- | -------------- |
| Sigma Rules       | Platform-agnostic detection logic     | 🟡 Learning    |
| KQL Queries       | Microsoft Sentinel / Defender hunting | 🟡 Learning    |
| YARA Rules        | File and malware-pattern detection    | 🟡 Learning    |
| Suricata Rules    | Network IDS detection                 | 🟡 Learning    |
| Python Scripting  | Automation and detection support      | 🟡 Learning    |
| GitHub Basics     | Portfolio and version control         | 🟢 Started     |
| GitHub Actions    | Future CI/CD for detections           | ⚪ Planned      |
| Sysmon            | Better Windows endpoint visibility    | ⚪ Planned      |
| Malware Analysis  | Understand file behavior and IOCs     | 🟡 Beginner    |
| Digital Forensics | Understand evidence and timelines     | 🟡 Beginner    |
| Threat Research   | Convert reports into detections       | ⚪ Planned      |

Legend:

* 🟢 Started and comfortable
* 🟡 Learning actively
* ⚪ Planned
* 🔴 Needs attention
* 🧠 Brain currently loading

---

## 📅 Learning Journey

| Date       | Topic / Activity     | What I Did                                                               | Key Takeaways                                                         | Mood                       |
| ---------- | -------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------- | -------------------------- |
| 2026-06-07 | GitHub Basics        | Created my first detection engineering portfolio repository              | GitHub is less scary when folders have a plan                         | 😎 Feeling official        |
| 2026-06-07 | Repository Structure | Created folders for docs, Sigma, KQL, YARA, Suricata, reports, and tests | Good structure now saves future chaos                                 | 🧹 Organized-ish           |
| 2026-06-07 | README Setup         | Added a professional repository README                                   | A repo without a README is a room with no door sign                   | 🚪 Better first impression |
| 2026-06-07 | Lab Architecture     | Documented the detection engineering lab layout                          | The lab has a story, not just random VMs sitting like furniture       | 🏰 Kingdom mapped          |
| 2026-06-07 | GitHub Actions Error | Saw a workflow failure notification                                      | CI/CD is powerful, but adding it too early creates noisy gremlins     | 🛠️ Lesson learned         |
| 2026-06-07 | FLARE VM             | Added FLARE to the lab architecture                                      | Useful for Windows malware analysis and YARA rule development         | 🔥 File detective mode     |
| 2026-06-07 | REMnux VM            | Added REMnux to the lab architecture                                     | Useful for IOC extraction, decoding, and Linux-based malware analysis | 🧊 Terminal wizardry       |
| 2026-06-07 | Parrot VM            | Added Parrot to the lab architecture                                     | Useful for controlled security testing and threat hunting support     | 🦜 Noisy but useful        |
| 2026-06-07 | SIFT VM              | Added SIFT to the lab architecture                                       | Useful for forensic timelines, artifacts, and post-incident thinking  | 🔎 Evidence goggles on     |

---

## 🧠 Things I Understand Better Now

### 1. GitHub Is Not Just for Developers

GitHub can be used as a professional security portfolio.

For detection engineering, it can store:

* Detection rules
* Hunting queries
* YARA rules
* Suricata rules
* Python helper scripts
* Lab notes
* Detection writeups
* Validation notes
* Learning logs

GitHub is basically my public cyber notebook with version control and fewer coffee stains. ☕

---

### 2. Structure Matters

A messy repository says:

> “I had energy but no map.”

A clean repository says:

> “I know how to organize security work.”

Current structure:

```text
docs/
sigma/
kql/
yara/
suricata/
python/
reports/
tests/
```

This structure helps each skill sit in its own chair instead of fighting in the hallway.

---

### 3. A Lab Should Have a Purpose

A lab is not useful just because it has many VMs.

A useful lab should answer:

* What behavior can I generate?
* What logs can I collect?
* What detection can I write?
* How can I validate it?
* What can I document?

The goal is not “more machines.”

The goal is:

> More useful evidence.
> Better detections.
> Sharper thinking.

---

### 4. Detection Engineering Is More Than Writing Rules

A detection is not just a YAML file wearing a helmet.

A good detection includes:

* Behavior understanding
* Data source knowledge
* Field selection
* Logic quality
* False positive thinking
* Validation
* Investigation guidance
* Documentation

The rule is the visible part.
The thinking behind it is the engine room. ⚙️

---

## 🧰 Tool Learning Notes

### 🛡️ Sigma

What I want to learn:

* Rule structure
* Logsource selection
* Detection conditions
* Field modifiers
* False positive documentation
* MITRE ATT&CK mapping
* Rule validation

Current understanding:

> Sigma is a common language for detection logic. It helps describe suspicious behavior in a way that can be converted into platform-specific queries.

Mini goal:

* Write simple process creation rules first
* Start with PowerShell, discovery commands, and account creation
* Validate rules using lab-generated activity

---

### 🔍 KQL

What I want to learn:

* Query structure
* Filtering
* Projection
* Sorting
* Joining tables
* Summarizing activity
* Hunting logic

Current understanding:

> KQL helps search large telemetry datasets and ask security questions in a precise way.

Mini goal:

* Translate Sigma-style logic into KQL
* Write hunting queries for Windows process activity
* Understand important tables like process events, logon events, and device events

---

### 🧬 YARA

What I want to learn:

* Rule structure
* Metadata
* String matching
* Conditions
* File-pattern detection
* Safe test files
* Malware-like pattern research

Current understanding:

> YARA is useful for detecting suspicious files based on strings, byte patterns, or structural clues.

Mini goal:

* Write beginner YARA rules for suspicious scripts
* Use FLARE and REMnux to understand file indicators
* Never upload real malware samples to GitHub

---

### 🌐 Suricata

What I want to learn:

* Rule syntax
* HTTP fields
* DNS indicators
* User-Agent detection
* Flow direction
* Alert validation
* PCAP-based testing later

Current understanding:

> Suricata helps detect suspicious behavior at the network level.

Mini goal:

* Start with simple HTTP and DNS detections
* Use Parrot and lab systems to generate safe network activity
* Keep custom rule IDs organized

---

### 🐍 Python

What I want to learn:

* Reading files
* Parsing CSV and JSON
* Extracting IOCs
* Checking rule metadata
* Automating boring tasks
* Supporting CI/CD later

Current understanding:

> Python helps detection engineers move faster by automating repetitive work.

Mini goal:

* Build an IOC extractor
* Build a log field profiler
* Later build rule validation helpers

Python is the small robot assistant that says:

> “I can do that boring thing 400 times without sighing.” 🤖

---

### 🔥 FLARE VM

What I want to learn:

* Static file analysis
* Suspicious string review
* PE file basics
* Script analysis
* YARA rule ideas
* Windows malware investigation workflow

Current understanding:

> FLARE helps analyze suspicious Windows files and understand file-based indicators.

Mini goal:

* Use only safe samples or training files
* Practice extracting suspicious strings
* Convert findings into YARA rules and notes

---

### 🧊 REMnux

What I want to learn:

* IOC extraction
* Decoding payloads
* Network artifact analysis
* Suspicious script analysis
* Linux-based malware tooling

Current understanding:

> REMnux is a powerful toolkit for malware analysis and suspicious artifact review.

Mini goal:

* Practice decoding and extracting indicators
* Use it as the “calm Linux brain” next to FLARE

---

### 🦜 Parrot

What I want to learn:

* Controlled network testing
* Reconnaissance behavior
* Security tool usage
* OSINT workflows
* Threat hunting support

Current understanding:

> Parrot can help generate controlled behavior that defenders can detect.

Mini goal:

* Use it carefully inside the lab
* Generate safe detection test cases
* Document what was generated and what logs appeared

---

### 🔎 SIFT

What I want to learn:

* Timeline creation
* Windows artifact analysis
* File system investigation
* Incident reconstruction
* Evidence-based thinking

Current understanding:

> SIFT helps understand what happened after suspicious activity occurs.

Mini goal:

* Practice forensic artifact review
* Connect forensic findings back to better detection logic

---

## 🧪 Lab Experiment Template

Use this format whenever I test something.

```markdown
## Experiment: <Name>

### Date

YYYY-MM-DD

### Objective

What am I trying to learn or detect?

### Systems Used

- Source:
- Target:
- Tools:

### Activity Performed

What did I run or simulate?

### Logs Generated

Which logs or telemetry should contain evidence?

### Detection Idea

What rule or query could detect this?

### Result

Did it work?

### False Positives

What legitimate activity could look similar?

### Lessons Learned

What should I remember next time?
```

---

## 🚨 Detection Idea Backlog

| Idea                                  | Rule Type      | Priority | Status  |
| ------------------------------------- | -------------- | -------: | ------- |
| Suspicious PowerShell Encoded Command | Sigma + KQL    |     High | Planned |
| Windows Discovery Commands            | Sigma + KQL    |     High | Planned |
| New Local Admin Account Created       | Sigma + KQL    |     High | Planned |
| Suspicious Archive Creation           | Sigma + KQL    |   Medium | Planned |
| Suspicious User-Agent                 | Suricata       |   Medium | Planned |
| Suspicious Script Obfuscation         | YARA           |     High | Planned |
| IOC Extraction Script                 | Python         |   Medium | Planned |
| Log Field Profiler                    | Python         |   Medium | Planned |
| Basic Timeline Analysis Case          | SIFT           |   Medium | Planned |
| Safe Malware-Like String Analysis     | FLARE + REMnux |   Medium | Planned |

---

## 🗺️ Weekly Progress Tracker

| Week    | Focus                            | Output                                  |
| ------- | -------------------------------- | --------------------------------------- |
| Week 1  | GitHub basics and repo structure | Clean portfolio repository              |
| Week 2  | Windows logging and Sysmon       | Telemetry notes and event examples      |
| Week 3  | Sigma basics                     | First 3 Sigma rules                     |
| Week 4  | KQL basics                       | Matching KQL queries for Sigma rules    |
| Week 5  | YARA basics                      | First file-pattern rules                |
| Week 6  | Suricata basics                  | First network detection rules           |
| Week 7  | Python support scripts           | IOC extractor and log profiler          |
| Week 8  | Detection writeups               | Complete rule documentation             |
| Week 9  | GitHub Actions                   | Basic validation workflow               |
| Week 10 | Threat research mini-project     | Convert public behavior into detections |

---

## 🧾 Personal Learning Rules

1. **Do not just copy rules**

   * Understand the behavior first.

2. **Do not upload unsafe data**

   * No company logs, no credentials, no real malware, no client data.

3. **Document the “why”**

   * A rule without explanation is just a cryptic sandwich.

4. **Validate whenever possible**

   * A detection that was never tested is a hopeful spell.

5. **Write for future me**

   * Future me should not need a treasure map to understand past me.

6. **Stay practical**

   * The goal is role readiness, not tool collecting.

7. **Small progress still counts**

   * One good note, one fixed error, one working rule. That is progress.

---

## 🧠 Random Brain Dump

Things I want to remember:

* Logs do not lie, but they sometimes mumble.
* PowerShell is powerful. So are good detections.
* A false positive is not failure. It is feedback wearing a tiny hat.
* Good rule names matter.
* Good folder structure is future kindness.
* Screenshots help, but documentation explains.
* Sigma and KQL are cousins, not twins.
* YARA is pattern hunting with a magnifying glass.
* Suricata watches the network road.
* Python is the intern that never complains.
* FLARE and REMnux are malware analysis buddies.
* SIFT is for “what happened?” moments.
* Parrot is for controlled poking and noisy footprints.
* GitHub is not scary once the first commit survives.

---

## 📌 Current Status

| Area                        | Status        |
| --------------------------- | ------------- |
| Repository created          | ✅ Done        |
| README created              | ✅ Done        |
| Lab architecture documented | ✅ Done        |
| Learning log created        | ✅ In progress |
| Sigma folder created        | ✅ Done        |
| KQL folder created          | ✅ Done        |
| YARA folder created         | ✅ Done        |
| Suricata folder created     | ✅ Done        |
| Reports folder created      | ✅ Done        |
| Tests folder created        | ✅ Done        |
| Python folder               | ⏳ Planned     |
| GitHub Actions              | ⏳ Later       |
| First validated detection   | ⏳ Upcoming    |

---

## 🚀 Upcoming Quests

* [ ] Add first Sigma rule
* [ ] Add matching KQL query
* [ ] Create first detection writeup
* [ ] Add YARA rule for suspicious script patterns
* [ ] Add Suricata rule for suspicious User-Agent
* [ ] Add Python IOC extractor
* [ ] Add Python log field profiler
* [ ] Enable better Windows logging
* [ ] Add Sysmon
* [ ] Generate safe test activity
* [ ] Document first validation result
* [ ] Add GitHub Actions after basics are stable

---

## 🏁 Final Note to Future Me

Dear future me,

Do not forget why this started.

The goal was never to create a fancy repo full of shiny folders.
The goal was to become better at understanding suspicious behavior and turning it into clear, tested, useful detections.

Every commit is a footprint.
Every note is a checkpoint.
Every rule is a tiny alarm owl learning to shout at the right moment. 🦉🚨

Keep building.

Keep testing.

Keep documenting.

Future you will thank present you.

Probably with coffee. ☕

