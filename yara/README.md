# 🧬 YARA Rules: File Pattern Hunting With a Magnifying Glass

> “Some files whisper. Some files scream. YARA helps us hear both.” 🔍📜

This folder contains my **YARA rules** for detecting suspicious file patterns, malware-like strings, script obfuscation, suspicious binaries, and other file-based indicators.

YARA is commonly used by malware analysts, threat hunters, incident responders, and detection engineers to identify files based on strings, byte patterns, metadata, and logical conditions.

In simple words:

> Sigma watches behavior.
> KQL questions telemetry.
> Suricata watches the network road.
> YARA stares at files and says, “You look familiar.” 👀

---

## 🎯 Purpose of This Folder

This folder is used to store YARA rules created for:

* Suspicious script detection
* Malware-like string patterns
* Obfuscation indicators
* Packed or suspicious binary traits
* File triage
* Threat research
* Malware analysis practice
* IOC-based file hunting
* Lab-safe YARA validation
* Detection engineering portfolio building

The goal is not to write magical rules that detect all evil forever.

The goal is to write rules that are:

* Clear
* Safe
* Testable
* Explainable
* Properly documented
* Honest about limitations
* Useful during investigation
* Helpful for malware analysis learning

Because a YARA rule without context is just a tiny spell with no instruction manual. 📘✨

---

## 📁 Folder Structure

Current structure:

```text
yara/
├── README.md
└── windows/
    └── suspicious_script_obfuscation.yar
```

Planned structure:

```text
yara/
├── README.md
│
├── windows/
│   ├── suspicious_script_obfuscation.yar
│   ├── powershell_obfuscation_keywords.yar
│   ├── suspicious_pe_strings.yar
│   └── suspicious_lolbin_script_patterns.yar
│
├── documents/
│   ├── suspicious_macro_indicators.yar
│   └── suspicious_document_strings.yar
│
├── malware_patterns/
│   ├── packed_binary_indicators.yar
│   ├── suspicious_imports.yar
│   └── generic_malware_like_strings.yar
│
└── lab_testing/
    ├── safe_test_strings.yar
    └── README.md
```

Folder purpose:

| Folder              | Purpose                                                       |
| ------------------- | ------------------------------------------------------------- |
| `windows/`          | Windows-focused scripts, binaries, and suspicious patterns    |
| `documents/`        | Suspicious document and macro-related indicators              |
| `malware_patterns/` | Generic malware-like strings, imports, and packing indicators |
| `lab_testing/`      | Safe rules and test notes for learning and validation         |

---

## 🧠 Why YARA Matters

YARA helps answer file-focused questions such as:

* Does this file contain suspicious strings?
* Does this script include obfuscation patterns?
* Does this binary contain suspicious imports?
* Does this file resemble a known malware family pattern?
* Can this indicator be converted into a reusable rule?
* Can I hunt for this pattern across multiple files?
* Can I support malware analysis with repeatable detection logic?

YARA is useful when the investigation moves from:

> “Something suspicious executed.”

to:

> “What exactly is this file, and have we seen similar patterns elsewhere?” 🧪

---

## 🧩 Basic YARA Rule Anatomy

A basic YARA rule looks like this:

```yara
rule Suspicious_Script_Obfuscation_Keywords
{
    meta:
        author = "PP"
        date = "2026-06-07"
        description = "Detects suspicious script obfuscation keywords in text-based files"
        status = "experimental"

    strings:
        $s1 = "FromBase64String" ascii nocase
        $s2 = "IEX" ascii nocase
        $s3 = "Invoke-Expression" ascii nocase
        $s4 = "-EncodedCommand" ascii nocase

    condition:
        2 of them
}
```

Main sections:

| Section     | Purpose                                                 |
| ----------- | ------------------------------------------------------- |
| `rule`      | Rule name                                               |
| `meta`      | Metadata about the rule                                 |
| `strings`   | Strings, byte patterns, or regex patterns to search for |
| `condition` | Logic that decides when the rule matches                |

Tiny translation:

> “If a file contains at least two of these suspicious strings, raise a tiny flag.” 🚩

---

## 🧾 Standard YARA Template

Use this template for new rules:

```yara
rule <Rule_Name>
{
    meta:
        author = "PP"
        date = "YYYY-MM-DD"
        modified = "YYYY-MM-DD"
        description = "<What this rule detects>"
        status = "experimental"
        category = "<script/binary/document/generic>"
        reference = "<public reference if available>"

    strings:
        $s1 = "<string_one>" ascii nocase
        $s2 = "<string_two>" ascii nocase
        $s3 = "<string_three>" ascii nocase

    condition:
        2 of them
}
```

Rule naming style:

```text
Suspicious_Script_Obfuscation_Keywords
PowerShell_Encoded_Command_Strings
Suspicious_PE_Import_Combination
Possible_Packed_Binary_Indicators
```

Avoid names like:

```text
test
yararule1
malwarething
final_final_rule
evil_file_detector_ultimate
```

That last one has confidence, but not discipline. 😄

---

## 🔥 Current Focus Area: Suspicious Script Patterns

Current rule:

```text
yara/windows/suspicious_script_obfuscation.yar
```

Focus patterns:

```text
FromBase64String
Invoke-Expression
IEX
-EncodedCommand
DownloadString
System.Net.WebClient
ConvertTo-SecureString
New-Object Net.WebClient
```

Why this matters:

Attackers may use scripting languages to hide behavior, download payloads, decode content, or execute commands in memory. These patterns can also appear in legitimate admin scripts, so YARA matches must be reviewed carefully.

Detection thinking:

> One suspicious string may be normal.
> Multiple suspicious strings together may be a file waving a tiny red flag while pretending to be paperwork. 🚩📄

---

## 🧬 YARA Use Cases in This Portfolio

### 1. Suspicious PowerShell Script Detection ⚡

Goal:

Detect scripts that include suspicious PowerShell patterns.

Possible indicators:

* Encoded commands
* Base64 decoding
* Download cradles
* Invoke-Expression
* Obfuscation strings
* Suspicious web requests

Useful for:

* Malware analysis
* Script triage
* Threat hunting
* Lab validation
* Detection writeups

---

### 2. Malware-Like String Detection 🦠

Goal:

Identify files that contain strings often associated with suspicious tooling or malware-like behavior.

Possible strings:

* Process injection terms
* Persistence-related paths
* Suspicious API names
* Anti-analysis terms
* Network communication strings
* Command execution strings

Important note:

> Strings alone do not prove malware. They create investigation leads. YARA points at the smoke, then the analyst checks for fire. 🔥

---

### 3. Suspicious PE File Indicators 🪟

Goal:

Practice detecting suspicious Windows executable traits.

Possible indicators:

* Suspicious imports
* Packing indicators
* Strange section names
* Embedded URLs
* Command execution strings
* Known tool artifacts

Useful tools:

* FLARE VM
* REMnux
* PE analysis tools
* Strings utilities
* Hashing tools

---

### 4. Document and Macro Indicators 📄

Goal:

Create beginner-safe rules for suspicious document patterns.

Possible indicators:

* Auto-execution macro terms
* PowerShell invocation
* Command shell invocation
* Suspicious URLs
* Obfuscated strings
* Script-related keywords

Important safety note:

> Real malicious documents should not be uploaded to GitHub. Only safe test files, sanitized examples, or rule logic belong here.

---

## 🧪 Lab Workflow for YARA Rule Development

```text
Pick suspicious file behavior
        ↓
Study safe sample or lab-created file
        ↓
Extract strings or patterns
        ↓
Write YARA rule
        ↓
Test against safe files
        ↓
Review false positives
        ↓
Improve condition logic
        ↓
Document findings
        ↓
Push rule to GitHub
```

Simple version:

> Find pattern.
> Write rule.
> Test safely.
> Tune.
> Document.
> Repeat until the rule stops behaving like a caffeinated pigeon. 🐦

---

## 🔬 Tools That Support YARA Learning

| Tool / VM | How It Helps                                                                |
| --------- | --------------------------------------------------------------------------- |
| FLARE VM  | Windows malware analysis, strings, PE inspection, reverse engineering tools |
| REMnux    | Linux malware analysis, decoding, IOC extraction, file triage               |
| SIFT      | Forensic artifact context and incident reconstruction                       |
| Python    | Automate scanning, parse results, clean indicators                          |
| GitHub    | Store rules, documentation, and validation notes                            |

YARA works best when supported by analysis.

A rule should not be born from vibes alone.

It should come from evidence, patterns, and testing. 🧠

---

## ✅ YARA Rule Quality Checklist

Before adding a YARA rule, check:

* [ ] Does the rule have a clear name?
* [ ] Is the metadata complete?
* [ ] Is the description useful?
* [ ] Are the strings specific enough?
* [ ] Is the condition reasonable?
* [ ] Could this create obvious false positives?
* [ ] Is the rule marked experimental if not fully tested?
* [ ] Was it tested against safe files?
* [ ] Is the filename clear?
* [ ] Is the rule stored in the correct folder?
* [ ] Can another analyst understand what it is hunting?
* [ ] Did I avoid uploading real malware?

Because “it matched something once” is not a detection strategy.

That is just file astrology. 🔮

---

## 🧯 False Positive Thinking

YARA rules can match legitimate files.

Common false positive sources:

* Admin scripts
* Security tools
* Developer tools
* Testing scripts
* Automation frameworks
* Documentation files
* Training material
* Red team tools
* Benign PowerShell scripts

A good rule should balance:

```text
Specific enough to be useful
Broad enough to catch the pattern
Documented enough to investigate
Safe enough to share
```

YARA is sharp.

Use gloves. 🧤

---

## 🚦 Rule Status Guidelines

Use honest status values.

| Status         | Meaning                                     |
| -------------- | ------------------------------------------- |
| `experimental` | New rule, needs testing and tuning          |
| `test`         | Used for lab validation                     |
| `stable`       | Tested and reliable enough for repeated use |
| `deprecated`   | Old rule, replaced or no longer useful      |

Most rules here should start as:

```yara
status = "experimental"
```

Experimental does not mean bad.

It means:

> “This rule is learning to walk. Please do not throw it into a production volcano yet.” 🌋

---

## 📌 Suggested Metadata Fields

Use metadata to make rules easier to understand.

Recommended fields:

```yara
meta:
    author = "PP"
    date = "YYYY-MM-DD"
    modified = "YYYY-MM-DD"
    description = "Short explanation"
    status = "experimental"
    category = "script"
    technique = "T1059.001"
    reference = "https://attack.mitre.org/techniques/T1059/001/"
```

Useful metadata fields:

| Field         | Why It Helps                      |
| ------------- | --------------------------------- |
| `author`      | Ownership                         |
| `date`        | Creation date                     |
| `modified`    | Last update                       |
| `description` | What the rule detects             |
| `status`      | Maturity level                    |
| `category`    | Script, binary, document, generic |
| `technique`   | ATT&CK mapping when useful        |
| `reference`   | Public source or research link    |

Metadata is kindness for future analysts.

Also for future you, who may otherwise stare at the rule and whisper, “Who wrote this cryptic sandwich?” 🥪

---

## 🧪 Testing Rules Safely

Example command:

```bash
yara suspicious_script_obfuscation.yar safe_test_file.txt
```

Possible safe test file content:

```text
This is a safe lab test file.
It contains Invoke-Expression and FromBase64String for YARA testing only.
No malware here. Just suspicious-looking training confetti.
```

Expected result:

```text
Suspicious_Script_Obfuscation_Keywords safe_test_file.txt
```

Important:

> Test files should be safe, synthetic, and clearly marked as lab material.

No real malware samples.

No live incident files.

No client files.

No “I found this weird EXE on the internet and pushed it to GitHub” energy. 🧯

---

## 🧠 Relationship with Other Folders

YARA connects to the rest of the repository.

| Folder      | Relationship                                                                           |
| ----------- | -------------------------------------------------------------------------------------- |
| `sigma/`    | YARA detects file patterns, Sigma detects behavior around those files                  |
| `kql/`      | KQL can hunt for execution, file creation, or Defender alerts related to YARA findings |
| `suricata/` | Network indicators from file analysis can inspire Suricata rules                       |
| `python/`   | Python can run YARA scans and parse results                                            |
| `reports/`  | Writeups explain why the rule exists and how it was tested                             |
| `tests/`    | Stores safe test notes and synthetic sample references                                 |
| `docs/`     | Lab architecture and learning notes explain the workflow                               |

Example combined workflow:

```text
Analyze suspicious script in FLARE or REMnux
        ↓
Extract strings
        ↓
Write YARA rule
        ↓
Test against safe file
        ↓
Write Sigma rule for execution behavior
        ↓
Write KQL query for hunting
        ↓
Document in reports/
```

This is how file analysis becomes detection engineering.

Not just “found string.”

More like:

> “Found string, understood behavior, wrote rule, validated safely, documented like a civilized analyst.” 🎩

---

## 🗺️ Planned YARA Rules

| Rule                                     | Purpose                                       | Status    |
| ---------------------------------------- | --------------------------------------------- | --------- |
| `suspicious_script_obfuscation.yar`      | Detect suspicious script obfuscation keywords | 🟡 Draft  |
| `powershell_encoded_command_strings.yar` | Detect encoded PowerShell-related strings     | ⚪ Planned |
| `powershell_download_cradle.yar`         | Detect download-and-execute script patterns   | ⚪ Planned |
| `suspicious_pe_strings.yar`              | Detect suspicious strings in Windows binaries | ⚪ Planned |
| `packed_binary_indicators.yar`           | Detect possible packed binary traits          | ⚪ Planned |
| `suspicious_macro_keywords.yar`          | Detect suspicious document macro strings      | ⚪ Planned |
| `generic_webshell_keywords.yar`          | Detect generic web shell-like strings         | ⚪ Planned |
| `credential_access_keywords.yar`         | Detect suspicious credential-related strings  | ⚪ Planned |

---

## 🔐 Safety and Ethics

This folder must not contain:

* Real malware samples
* Client files
* Company files
* Private investigation artifacts
* Proprietary signatures
* Passwords
* API keys
* Tokens
* Sensitive documents
* Live incident data

Allowed content:

* YARA rules written by me
* Safe synthetic test files
* Lab-created samples
* Public-learning notes
* Sanitized examples
* Metadata and references
* Validation notes without sensitive data

Golden rule:

> Upload rules, not dangerous files.
> Share knowledge, not chaos. 🔐

---

## 🧠 Personal YARA Notes

Things to remember:

* Strings are clues, not verdicts.
* Conditions matter more than string quantity.
* Avoid overly broad rules.
* Document false positives.
* Use safe test files.
* Never upload real malware.
* Use FLARE and REMnux for analysis.
* Use Python later to automate scans.
* Keep rule names clear.
* Keep metadata useful.
* Test before trusting.
* YARA is powerful, but it needs analyst judgment.

Also:

> A good YARA rule is not a magic sword.
> It is a well-labeled flashlight. 🔦

---

## 🏁 Final Note

This YARA folder is where file patterns become detection logic.

The mission is not to collect random strings like shiny cyber pebbles.

The mission is to build clear, safe, tested, explainable rules that answer:

* What file pattern is suspicious?
* Why does it matter?
* What strings or structures are being matched?
* What could cause false positives?
* How was the rule tested?
* How can this support malware analysis or threat hunting?

Every YARA rule should create a useful investigation lead.

Not panic.

Not noise.

A clue.

And when a file tries to look boring while carrying suspicious strings in its pockets, YARA politely taps the glass and says:

> “I saw that.” 🧬🚨

