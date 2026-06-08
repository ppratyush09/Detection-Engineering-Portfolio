# 🌐 Phase 05: Suricata and Network Detection

> “Endpoints tell you what happened on the machine.
> The network tells you who talked to whom, when, and with what suspicious little accent.” 🕵️‍♂️📡

This phase focuses on **Suricata**, **network detection engineering**, suspicious outbound traffic, DNS clues, HTTP behavior, traffic generation, and network alert validation.

Phase 01 built the lab foundation.
Phase 02 focused on Windows telemetry.
Phase 03 introduced Sigma and KQL.
Phase 04 explored YARA and malware analysis.
Phase 05 now watches the network road.

The goal is to learn how network activity becomes detection logic.

In simple words:

> Packets move.
> Suricata watches.
> Alerts appear.
> Analysts investigate.
> Suspicious traffic regrets being chatty. 🦈

---

## 🎯 Phase Objective

The objective of Phase 05 is to build practical understanding of network detection using Suricata.

This includes:

* Understanding Suricata rule syntax
* Writing basic Suricata rules
* Detecting suspicious outbound traffic
* Detecting suspicious HTTP User-Agent strings
* Learning DNS-based detection ideas
* Understanding scanning and reconnaissance traffic
* Generating safe lab traffic
* Validating Suricata alerts
* Correlating network alerts with endpoint telemetry
* Documenting false positives
* Creating network detection writeups

This phase is considered successful when I can take one network behavior and produce:

| Output               | Purpose                                         |
| -------------------- | ----------------------------------------------- |
| Suricata rule        | Detect suspicious network pattern               |
| Alert explanation    | Explain why the traffic matters                 |
| Validation note      | Show how the alert was tested safely            |
| Investigation steps  | Explain what an analyst should check next       |
| False-positive notes | Document legitimate reasons for similar traffic |
| Detection writeup    | Connect network evidence with endpoint context  |

Tiny network law:

> A packet is just a packet.
> A suspicious pattern is where the story begins. 📖

---

## 🧭 Phase Scope

This phase focuses on **beginner to intermediate network detection**.

Included in this phase:

* Suricata rule anatomy
* HTTP detection basics
* DNS detection basics
* Suspicious outbound traffic
* User-Agent detection
* Internal scanning detection
* Lab-only traffic generation
* OPNsense and firewall visibility
* Network alert fields
* Suricata validation notes
* Endpoint and network correlation

Not included yet:

* Production IDS tuning
* Large PCAP hunting
* Full malware C2 emulation
* Advanced protocol parsing
* Evasion-heavy network testing
* Live internet target scanning
* Real client traffic
* Proprietary network detections

This phase is about learning the road signs before building the whole traffic-control tower. 🚦

---

## 🧠 Why Network Detection Matters

Endpoint telemetry is powerful, but endpoints do not tell the whole story.

Network telemetry helps answer:

* Which host connected outbound?
* Which destination was contacted?
* Which protocol was used?
* Was DNS involved?
* Was the User-Agent unusual?
* Was the traffic automated?
* Was there scanning behavior?
* Did one host contact many ports?
* Did traffic repeat like a beacon?
* Does endpoint activity explain the network alert?

Network detection is valuable because attackers and malware usually need to communicate, move, scan, download, upload, or phone home.

Packets leave footprints.

Suricata notices the shoes. 👟

---

## 🏗️ Planned Phase 05 Files

This phase will contain notes, rules, validation steps, and traffic-generation documentation.

```text
phase-05-suricata-and-network-detection/
├── README.md
├── suricata-basics.md
├── suricata-rule-template.md
├── suspicious-outbound-notes.md
├── dns-detection-notes.md
├── http-detection-notes.md
├── scanning-detection-notes.md
├── traffic-generation-notes.md
├── alert-analysis.md
├── endpoint-network-correlation.md
└── phase-05-completion-summary.md
```

| File                              | Purpose                                        |
| --------------------------------- | ---------------------------------------------- |
| `README.md`                       | Overview of Phase 05                           |
| `suricata-basics.md`              | Suricata concepts and rule syntax              |
| `suricata-rule-template.md`       | Standard reusable rule format                  |
| `suspicious-outbound-notes.md`    | Outbound traffic detection ideas               |
| `dns-detection-notes.md`          | DNS query patterns and detection ideas         |
| `http-detection-notes.md`         | HTTP User-Agent, URI, header, and method notes |
| `scanning-detection-notes.md`     | Internal scanning and reconnaissance detection |
| `traffic-generation-notes.md`     | Safe lab-only traffic generation steps         |
| `alert-analysis.md`               | How Suricata alerts are reviewed               |
| `endpoint-network-correlation.md` | Connecting network alerts with Windows logs    |
| `phase-05-completion-summary.md`  | Summary before Python automation phase         |

---

## 📁 Related Repository Folders

Phase 05 connects with these main folders:

| Folder                                               | Relationship                                                   |
| ---------------------------------------------------- | -------------------------------------------------------------- |
| `suricata/`                                          | Final Suricata rules live here                                 |
| `reports/`                                           | Network detection writeups live here                           |
| `tests/`                                             | Safe validation notes and expected alert results               |
| `docs/`                                              | Lab architecture and network design notes                      |
| `kql/`                                               | Endpoint and Defender telemetry can investigate network alerts |
| `sigma/`                                             | Endpoint behavior can support network detection                |
| `python/`                                            | Scripts can parse alerts or summarize logs                     |
| `learning-notes/phase-01-lab-foundation/`            | Network setup and VM roles                                     |
| `learning-notes/phase-04-yara-and-malware-analysis/` | Malware findings may inspire network rules                     |

Expected workflow:

```text
Observe network behavior
        ↓
Write Suricata rule
        ↓
Generate safe lab traffic
        ↓
Validate alert
        ↓
Correlate with endpoint logs
        ↓
Document false positives
        ↓
Publish rule and writeup
```

This is how packet sightings become detection engineering evidence. 🧾

---

## 🦈 What Is Suricata?

Suricata is an open-source network threat detection engine. It can inspect network traffic and generate alerts based on rules.

Suricata can help with:

* IDS detection
* Network security monitoring
* Protocol inspection
* Alert generation
* PCAP analysis
* Traffic pattern detection
* Suspicious outbound monitoring

A basic Suricata rule looks like this:

```text
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious User-Agent Observed"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

Tiny translation:

> If an internal machine sends HTTP traffic outward with a User-Agent containing `PowerShell`, create an alert and wave a little network flag. 🚩

---

## 🧩 Basic Suricata Rule Anatomy

| Rule Part        | Example                      | Meaning                     |
| ---------------- | ---------------------------- | --------------------------- |
| Action           | `alert`                      | What Suricata should do     |
| Protocol         | `http`                       | Protocol to inspect         |
| Source           | `$HOME_NET`                  | Internal network            |
| Source Port      | `any`                        | Any source port             |
| Direction        | `->`                         | Direction of traffic        |
| Destination      | `$EXTERNAL_NET`              | External network            |
| Destination Port | `any`                        | Any destination port        |
| Message          | `msg:"..."`                  | Alert name                  |
| Flow             | `flow:to_server,established` | Direction and session state |
| Content Match    | `content:"PowerShell"`       | Pattern to match            |
| Modifier         | `nocase`                     | Case-insensitive match      |
| Classification   | `classtype:trojan-activity`  | Alert category              |
| SID              | `sid:1000001`                | Unique rule ID              |
| Revision         | `rev:1`                      | Rule version                |

Suricata rules are picky.

One missing semicolon can turn a rule into a tiny tantrum. 🧨

---

## 🧾 Standard Suricata Rule Template

Use this format for custom lab rules:

```text
# Status: Draft
# Author: PP
# Purpose: <What this rule detects>
# Validation: <Not tested / Lab tested / Needs tuning>
# Notes: Lab use only. Validate before using anywhere else.

alert <protocol> <source_ip> <source_port> -> <destination_ip> <destination_port> (msg:"LAB <Clear Alert Name>"; <rule_options>; classtype:<category>; sid:<custom_sid>; rev:<revision>;)
```

Example:

```text
# Status: Draft
# Author: PP
# Purpose: Detect PowerShell User-Agent in outbound HTTP traffic
# Validation: Not tested
# Notes: Lab use only. May trigger on legitimate admin automation.

alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious PowerShell User-Agent"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

---

## 🔢 SID Numbering Plan

Custom Suricata rules need unique SIDs.

For this lab, use:

```text
1000000 to 1999999
```

Suggested range plan:

|            SID Range | Category                      |
| -------------------: | ----------------------------- |
| `1000001 to 1000999` | Suspicious outbound traffic   |
| `1001000 to 1001999` | DNS detections                |
| `1002000 to 1002999` | HTTP detections               |
| `1003000 to 1003999` | Scanning and reconnaissance   |
| `1004000 to 1004999` | Malware-like network behavior |
| `1005000 to 1005999` | Lab testing rules             |

SID rule:

> Never reuse a SID for different logic.
> Duplicate SIDs are how alerts start wearing fake mustaches. 🥸

---

## 🌐 Core Network Detection Areas

### 1. Suspicious Outbound Traffic 🚀

Goal:

Detect unusual outbound traffic from lab systems.

Examples:

* PowerShell making HTTP requests
* Python scripts making unexpected web requests
* Curl or wget traffic from unexpected Windows hosts
* Repeated outbound requests
* Strange User-Agent strings
* Suspicious URI paths
* Unusual destination ports

Detection questions:

* Which internal host initiated the traffic?
* What process caused it?
* Was the destination expected?
* Was the User-Agent normal?
* Did this happen repeatedly?
* Was a file downloaded?
* Does endpoint telemetry explain it?

Network thought:

> Outbound traffic is where many stories leave the building. Watch the exits. 🚪

---

### 2. HTTP Detection 🕸️

Goal:

Detect suspicious HTTP behavior.

Useful fields:

* HTTP host
* URI path
* User-Agent
* HTTP method
* Referer
* Response codes
* Content type
* File extensions
* Repeated requests

Suspicious patterns:

```text
PowerShell
python-requests
curl
wget
bitsadmin
certutil
/putty.exe
/update
/checkin
/gate
/payload
```

Example detection idea:

```text
Suspicious scripted User-Agent from an endpoint
```

Why this matters:

Attackers and malware may use HTTP for downloads, command-and-control, staging, or exfiltration.

HTTP is not automatically suspicious.

But HTTP with odd headers, strange paths, and weird timing deserves a clipboard. 📋

---

### 3. DNS Detection 🧭

Goal:

Detect suspicious DNS activity.

Useful patterns:

* Long domain names
* Random-looking subdomains
* Repeated queries
* Failed queries
* Rare domains
* DNS tunneling indicators
* Newly observed domains
* Domain queries followed by outbound connection

Detection questions:

* Which host queried the domain?
* Was the domain resolved?
* Did the host connect afterward?
* Did multiple hosts query it?
* Is the domain expected?
* Is the domain newly observed in the lab?

DNS is the network’s gossip channel.

Sometimes it says:

> “Nothing to see here.”

Sometimes it says:

> “Why is this workstation asking for `xj29sd9q.example.test` every 10 seconds?” 👀

---

### 4. Scanning and Reconnaissance 🔦

Goal:

Detect internal scanning and reconnaissance traffic.

Lab source:

```text
PARROT01
```

Possible activities:

* Ping sweep
* Port scan
* Service detection
* Repeated connection attempts
* Internal host discovery

Important:

> All scanning must stay inside the lab.
> The public internet is not a practice target.

Detection questions:

* Which host scanned?
* Which targets were contacted?
* Which ports were touched?
* Was traffic repeated?
* Was this expected testing?
* Did OPNsense or Suricata alert?

Scanning is the network equivalent of knocking on every door in a hallway.

Sometimes admin work.

Sometimes suspicious.

Always worth context. 🚪

---

### 5. Possible Beaconing Behavior 📡

Goal:

Learn basic beaconing concepts.

Possible clues:

* Repeated outbound connections
* Similar timing intervals
* Same destination
* Same URI path
* Same User-Agent
* Small request/response sizes
* Traffic from unusual process or host

Beginner scope:

This phase should only use safe simulated traffic, not real malware beaconing.

Example safe simulation:

```text
A script making repeated HTTP requests to an internal Ubuntu web server.
```

Detection thought:

> One request is a dot.
> Repeated requests become a rhythm.
> Suspicious rhythms become hunting questions. 🥁

---

## 🧪 Safe Traffic Generation

Traffic should be generated safely inside the lab.

Allowed lab traffic examples:

| Traffic Type           | Source            | Destination       | Purpose                          |
| ---------------------- | ----------------- | ----------------- | -------------------------------- |
| HTTP request           | Windows Client    | Ubuntu web server | Test HTTP logging                |
| PowerShell web request | Admin Workstation | Internal server   | Test User-Agent behavior         |
| DNS query              | Windows Client    | DC / DNS server   | Test DNS visibility              |
| Ping sweep             | Parrot            | Lab subnet only   | Test scanning visibility         |
| Port scan              | Parrot            | Lab target only   | Test Suricata or firewall alerts |
| Repeated HTTP request  | Windows / Linux   | Internal server   | Simulate beacon-like pattern     |

Not allowed:

* Scanning public IPs
* Testing unknown external systems
* Running uncontrolled scripts
* Using real malware traffic
* Uploading sensitive PCAPs
* Capturing personal/home traffic unnecessarily

Safe traffic rule:

> If I do not own it or control it, I do not test against it. 🔐

---

## 🧰 Lab Systems Used in Phase 05

| System            | Use                                                   |
| ----------------- | ----------------------------------------------------- |
| OPNsense          | Firewall logs, routing, segmentation                  |
| Parrot            | Lab-only scanning and traffic generation              |
| Windows Client    | Endpoint-generated network traffic                    |
| Admin Workstation | PowerShell and admin traffic testing                  |
| Ubuntu Server     | Internal web server or utility target                 |
| REMnux            | Network artifact review and malware-analysis support  |
| FLARE             | Windows-side artifact analysis if needed              |
| SIFT              | Forensic context if network events relate to evidence |
| Suricata sensor   | IDS alert generation and network monitoring           |

Initial beginner lab combination:

```text
OPNsense + Windows Client + Ubuntu Server + Parrot
```

Add REMnux later when network artifact analysis becomes more detailed.

---

## 🔍 Useful Suricata Alert Fields

When an alert fires, document useful fields.

| Field            | Why It Matters                       |
| ---------------- | ------------------------------------ |
| Timestamp        | When the activity happened           |
| Source IP        | Internal host that initiated traffic |
| Source Port      | Client-side port                     |
| Destination IP   | Remote target                        |
| Destination Port | Service being contacted              |
| Protocol         | HTTP, DNS, TLS, TCP, UDP             |
| Alert Message    | Rule name                            |
| SID              | Rule identifier                      |
| Revision         | Rule version                         |
| HTTP Host        | Domain or host header                |
| URI              | Requested path                       |
| User-Agent       | Tool/client clue                     |
| Flow Direction   | Traffic direction                    |
| Severity         | Alert importance                     |
| PCAP Reference   | Evidence for validation, if safe     |

Good alert fields turn:

```text
Something happened.
```

into:

```text
This host contacted this destination using this pattern at this time.
```

That is much better. Less fog. More flashlight. 🔦

---

## 🧪 Validation Workflow

Use this workflow for each Suricata rule.

```text
Choose network behavior
        ↓
Write Suricata rule
        ↓
Generate safe lab traffic
        ↓
Confirm alert fires
        ↓
Review alert details
        ↓
Compare with firewall logs
        ↓
Compare with endpoint logs if possible
        ↓
Document false positives
        ↓
Tune rule if needed
        ↓
Publish rule and writeup
```

Validation result labels:

| Status       | Meaning                           |
| ------------ | --------------------------------- |
| Draft        | Rule written but not tested       |
| Lab Tested   | Rule fired successfully in lab    |
| Needs Tuning | Rule works but is too noisy       |
| Improved     | Rule updated after review         |
| Retired      | Rule replaced or no longer useful |

Important:

> A rule that looks good but has never been tested is a decorative shark. 🦈

---

## 🧾 Suricata Validation Note Template

```markdown
# Suricata Validation: <Rule Name>

## Rule

- Rule Path: `suricata/<folder>/<rule-name>.rules`
- SID:
- Status:

## Behavior Tested

What network behavior was generated?

## Lab Systems Used

| System | Role |
|---|---|
| PARROT01 | Traffic generation |
| UBUNTU01 | Target server |
| OPNsense | Firewall |
| Suricata | IDS alerting |

## Expected Alert

What should Suricata detect?

## Observed Alert

What alert appeared?

## Useful Fields

| Field | Value |
|---|---|
| Source IP | `<lab-ip>` |
| Destination IP | `<lab-ip>` |
| Protocol | `<protocol>` |
| User-Agent | `<value>` |
| URI | `<value>` |

## False Positives

What legitimate activity might look similar?

## Endpoint Correlation

Was matching endpoint telemetry available?

## Result

- [ ] Alert fired
- [ ] Alert did not fire
- [ ] Rule needs tuning
- [ ] More testing needed

## Lessons Learned

What did this test teach?
```

---

## 🔗 Endpoint and Network Correlation

Network alerts become stronger when combined with endpoint logs.

Example workflow:

```text
Suricata alert fires
        ↓
Identify source IP
        ↓
Map source IP to host
        ↓
Check endpoint logs
        ↓
Find process responsible
        ↓
Review command line
        ↓
Check user context
        ↓
Write Sigma/KQL follow-up
```

Example:

| Network Alert              | Endpoint Follow-up                                     |
| -------------------------- | ------------------------------------------------------ |
| PowerShell User-Agent      | Check process creation for `powershell.exe`            |
| Suspicious DNS query       | Check which process made DNS query if Sysmon available |
| Internal scan              | Check source host process and user                     |
| HTTP download              | Check file creation and process tree                   |
| Repeated outbound requests | Check scheduled task, script, or process loop          |

Detection thought:

> Network tells me communication happened.
> Endpoint tells me who caused it.
> Together, they gossip usefully. 🗣️

---

## 🧯 False Positive Thinking

Network detections can be noisy.

Common false-positive sources:

* Admin scripts
* Monitoring tools
* Software updates
* Security tools
* Package managers
* Browsers
* Developer tools
* Backup tools
* Internal scanners
* Vulnerability scanners
* Lab testing

Good questions:

* Is the source host expected?
* Is the destination expected?
* Is the User-Agent normal?
* Is the timing unusual?
* Is the traffic repeated?
* Is the host a server, admin box, or user endpoint?
* Does endpoint telemetry explain it?
* Is this part of a known lab test?

Network detection goal:

```text
Useful clues, not packet confetti.
```

A noisy rule is not heroic.

It is just loud. 📣

---

## 📚 MITRE ATT&CK Mapping Ideas

Some network behaviors may map to ATT&CK techniques.

| Behavior                           | Possible Technique                  |
| ---------------------------------- | ----------------------------------- |
| Command-and-control traffic        | T1071 Application Layer Protocol    |
| DNS-based communication            | T1071.004 DNS                       |
| Web protocol communication         | T1071.001 Web Protocols             |
| Network service discovery          | T1046 Network Service Discovery     |
| System discovery via network tools | T1018 Remote System Discovery       |
| Exfiltration over web service      | T1567 Exfiltration Over Web Service |
| Ingress tool transfer              | T1105 Ingress Tool Transfer         |

MITRE mapping should be accurate and evidence-based.

Do not throw ATT&CK IDs at a rule just because it looks lonely. 🎯

---

## 📌 Initial Suricata Rule Ideas

| Rule                               | Purpose                                                   | Status    |
| ---------------------------------- | --------------------------------------------------------- | --------- |
| `suspicious_user_agent.rules`      | Detect suspicious scripted User-Agent strings             | 🟡 Draft  |
| `powershell_user_agent.rules`      | Detect PowerShell HTTP traffic                            | ⚪ Planned |
| `python_requests_user_agent.rules` | Detect Python requests traffic                            | ⚪ Planned |
| `curl_wget_from_windows.rules`     | Detect command-line web clients from Windows-like sources | ⚪ Planned |
| `suspicious_dns_query.rules`       | Detect suspicious domain patterns                         | ⚪ Planned |
| `internal_port_scan.rules`         | Detect lab-only internal scanning                         | ⚪ Planned |
| `possible_beaconing_pattern.rules` | Detect repeated outbound pattern in lab                   | ⚪ Planned |
| `suspicious_http_uri.rules`        | Detect suspicious URI keywords                            | ⚪ Planned |

---

## 🛡️ Detection Engineering Relevance

Phase 05 supports Detection Engineering by adding network visibility.

| Detection Area  | How Network Detection Helps                                 |
| --------------- | ----------------------------------------------------------- |
| Sigma           | Endpoint detections can support Suricata alerts             |
| KQL             | Queries can investigate hosts that triggered network alerts |
| YARA            | File analysis may produce network indicators                |
| Suricata        | Network behavior becomes IDS rules                          |
| Python          | Scripts can parse alerts and summarize traffic              |
| Reports         | Network writeups explain alert value                        |
| Threat Research | Public reports often include network behaviors and IOCs     |

Strong detection engineering often combines:

```text
Endpoint behavior + Network behavior + File indicators + Analyst context
```

That is how small clues become a case. 🧩

---

## 🔐 Safety and Ethics

This phase must not include:

* Client PCAPs
* Company traffic
* Sensitive firewall logs
* Work IP ranges
* Credentials
* API keys
* Production hostnames
* Private incident infrastructure
* Real malware network traffic
* Uncontrolled scanning activity
* Public target testing without authorization

Allowed:

* Lab-only traffic
* Synthetic examples
* Sanitized alert notes
* Custom Suricata rules
* Dummy indicators
* Internal lab IP examples
* Safe screenshots
* Public-learning references

Golden rule:

> Watch the lab road.
> Do not patrol streets you do not own. 🔐

---

## ✅ Phase 05 Checklist

| Task                                    | Status |
| --------------------------------------- | ------ |
| Suricata basics documented              | ⏳      |
| Suricata rule template created          | ⏳      |
| SID numbering plan documented           | ⏳      |
| Suspicious outbound notes created       | ⏳      |
| HTTP detection notes created            | ⏳      |
| DNS detection notes created             | ⏳      |
| Scanning detection notes created        | ⏳      |
| Safe traffic generation notes created   | ⏳      |
| First Suricata rule drafted             | ⏳      |
| First Suricata rule validated           | ⏳      |
| Alert analysis notes created            | ⏳      |
| Endpoint-network correlation documented | ⏳      |
| No unauthorized scanning performed      | ✅      |
| No sensitive traffic uploaded           | ✅      |

---

## 🚀 Next Phase

After Phase 05, the next phase should be:

```text
Phase 06: Python for Detection Engineering
```

Phase 06 will focus on:

* Python helper scripts
* IOC extraction
* Log parsing
* CSV and JSON analysis
* YARA helper scripts
* Sigma metadata checks
* Alert summarization
* Automation for detection workflows

Phase 05 watches packets.

Phase 06 builds small robots to help sort the evidence. 🤖

---

## 🏁 Final Note

Phase 05 is where the lab learns to watch the network.

A strong network detection should answer:

* Who communicated?
* With what destination?
* Over which protocol?
* What pattern triggered the rule?
* Why is it suspicious?
* What false positives exist?
* What endpoint evidence supports it?
* What should an analyst check next?

The goal is not to alert on everything.

The goal is to create useful network clues that support investigation.

Packets may be tiny.

But with good detection logic, they can tell very large stories. 🌐📜

