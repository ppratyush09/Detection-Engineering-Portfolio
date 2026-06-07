# 🌐 Suricata Rules: Teaching Packets to Behave in Public

> “The endpoint tells you what happened on the machine.
> The network tells you who whispered to whom.” 🕵️‍♂️📡

This folder contains my **Suricata IDS rules** for network detection engineering, suspicious outbound traffic, strange HTTP behavior, DNS clues, scanning activity, and future packet-based threat hunting practice.

Suricata helps inspect network traffic and generate alerts when traffic matches detection logic.

In simple words:

> Sigma watches the endpoint.
> YARA watches the file.
> KQL questions the logs.
> Suricata watches the road outside the castle. 🏰🚗

---

## 🎯 Purpose of This Folder

This folder is used to store Suricata rules created for:

* Suspicious outbound traffic detection
* Strange HTTP User-Agent detection
* DNS-based indicators
* Possible command-and-control traffic clues
* Scanning and reconnaissance behavior
* Lab-generated network alerts
* Network detection validation
* PCAP-based analysis practice
* Threat hunting support
* Detection engineering portfolio building

The goal is not to create random noisy rules that scream at every packet wearing odd socks.

The goal is to write rules that are:

* Clear
* Testable
* Explainable
* Safe for lab use
* Organized by behavior
* Documented with purpose
* Mapped to investigation value
* Tuned to reduce unnecessary noise

Because a noisy IDS is just a parrot with a keyboard. 🦜⌨️

---

## 📁 Folder Structure

Current structure:

```text
suricata/
├── README.md
└── suspicious_outbound/
    └── suspicious_user_agent.rules
```

Planned structure:

```text
suricata/
├── README.md
│
├── suspicious_outbound/
│   ├── suspicious_user_agent.rules
│   ├── suspicious_http_method.rules
│   ├── suspicious_external_connection.rules
│   └── possible_c2_beaconing.rules
│
├── dns/
│   ├── suspicious_domain_lookup.rules
│   ├── dns_tunneling_indicators.rules
│   └── newly_observed_domain_pattern.rules
│
├── scanning/
│   ├── internal_port_scan.rules
│   ├── suspicious_nmap_user_agent.rules
│   └── repeated_connection_attempts.rules
│
├── http/
│   ├── suspicious_uri_pattern.rules
│   ├── suspicious_file_download.rules
│   └── suspicious_post_request.rules
│
└── lab_testing/
    ├── test_alert.rules
    └── README.md
```

Folder purpose:

| Folder                 | Purpose                                                               |
| ---------------------- | --------------------------------------------------------------------- |
| `suspicious_outbound/` | Rules for unusual outbound connections and suspicious client behavior |
| `dns/`                 | DNS query detections and domain-related indicators                    |
| `scanning/`            | Reconnaissance and network scan detection                             |
| `http/`                | HTTP method, URI, header, and download pattern rules                  |
| `lab_testing/`         | Safe rules used only for learning and validation                      |

---

## 🧠 Why Suricata Matters

Endpoint logs show what happened on a system.

Network logs show communication patterns.

Suricata helps answer questions such as:

* Which internal host connected outbound?
* What protocol was used?
* Was the traffic HTTP, DNS, TLS, SMB, or something else?
* Was there a strange User-Agent?
* Was a suspicious domain queried?
* Was a system scanning other systems?
* Did traffic look automated?
* Did the same connection happen repeatedly?
* Did endpoint behavior and network behavior line up?

Good network detection is not about staring at every packet until your soul leaves your body.

It is about finding patterns that matter. 🧠📡

---

## 🦈 Basic Suricata Rule Anatomy

A Suricata rule usually looks like this:

```text
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious User-Agent Observed"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

Important parts:

| Part            | Meaning                                 |
| --------------- | --------------------------------------- |
| `alert`         | Action to take when the rule matches    |
| `http`          | Protocol being inspected                |
| `$HOME_NET`     | Internal network                        |
| `$EXTERNAL_NET` | External network                        |
| `any -> any`    | Source and destination ports/direction  |
| `msg`           | Alert message shown when the rule fires |
| `flow`          | Direction and session state             |
| `content`       | String or pattern to match              |
| `nocase`        | Case-insensitive matching               |
| `classtype`     | Alert category                          |
| `sid`           | Unique rule ID                          |
| `rev`           | Rule revision number                    |

Tiny translation:

> If traffic from home network to external network over HTTP has a User-Agent containing `PowerShell`, raise your hand and make noise. 🚨

---

## 🧾 Standard Rule Format

Use this style for custom lab rules:

```text
alert <protocol> <source_ip> <source_port> -> <destination_ip> <destination_port> (msg:"LAB <Clear Alert Name>"; <rule_options>; classtype:<category>; sid:<custom_sid>; rev:<revision>;)
```

Example:

```text
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious PowerShell User-Agent"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

---

## 🔢 SID Numbering Plan

Custom rules need unique SIDs.

For this lab, I will use this custom SID range:

```text
1000000 to 1999999
```

Suggested categories:

|            SID Range | Category                      |
| -------------------: | ----------------------------- |
| `1000001 to 1000999` | Suspicious outbound traffic   |
| `1001000 to 1001999` | DNS detections                |
| `1002000 to 1002999` | HTTP detections               |
| `1003000 to 1003999` | Scanning and reconnaissance   |
| `1004000 to 1004999` | Malware-like network behavior |
| `1005000 to 1005999` | Lab testing rules             |

Rule goblin rule:

> Never reuse the same SID for different logic. That creates confusion soup. 🍲

---

## 🔥 Current Focus Area: Suspicious Outbound Traffic

The first folder is:

```text
suricata/suspicious_outbound/
```

This is focused on outbound network behavior from internal systems.

Why outbound traffic matters:

* Malware often communicates outward
* Attackers may use remote tools
* Scripts may download payloads
* Compromised hosts may call external infrastructure
* Suspicious User-Agents can reveal automation
* DNS and HTTP patterns may support hunting

Current rule:

```text
suspicious_user_agent.rules
```

Possible detection ideas:

| Rule Idea                               | Why It Matters                                    |
| --------------------------------------- | ------------------------------------------------- |
| Suspicious PowerShell User-Agent        | PowerShell making HTTP requests can be suspicious |
| Curl or wget from Windows host          | May indicate script-based download behavior       |
| Python User-Agent from non-dev endpoint | Could indicate automation or tooling              |
| Unusual HTTP method                     | Odd methods can indicate suspicious tooling       |
| Repeated outbound beacon-like traffic   | Could suggest command-and-control behavior        |
| Suspicious URI pattern                  | Randomized paths may indicate automation          |
| Known lab test domain access            | Useful for safe validation                        |

---

## 🧪 Example Rule: Suspicious User-Agent

```text
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious User-Agent Observed"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

Purpose:

Detect HTTP traffic where the User-Agent contains `PowerShell`.

Why this can matter:

PowerShell can be used for legitimate administrative automation, but it can also be used for suspicious download activity, payload retrieval, or command execution workflows.

Expected false positives:

* Admin scripts
* Security automation
* Software deployment tools
* Internal testing
* Lab-generated activity

Investigation questions:

* Which host generated the traffic?
* Which user was active on that host?
* What process created the connection?
* Was PowerShell also visible in endpoint logs?
* What URL or domain was contacted?
* Was this expected admin behavior?
* Did any file get downloaded?

---

## 🌐 Protocol Areas I Want to Learn

### 1. HTTP Detection 🕸️

Focus:

* User-Agent strings
* URI paths
* HTTP methods
* Suspicious downloads
* Odd headers
* POST activity
* Automation clues

Example patterns:

```text
PowerShell
curl
wget
python-requests
bitsadmin
certutil
```

Network thought:

> A strange User-Agent is not automatically evil, but it deserves a raised eyebrow and maybe a tiny clipboard. 📋

---

### 2. DNS Detection 🧭

Focus:

* Suspicious domain lookups
* Very long domains
* Repeated failed lookups
* Random-looking subdomains
* Potential tunneling indicators
* Newly observed domains in lab data

Investigation questions:

* Which host queried the domain?
* Was the query successful?
* Was there a connection after the query?
* Is the domain expected?
* Did multiple hosts query the same domain?

DNS is the network’s gossip channel.

Sometimes it says useful things.

Sometimes it mumbles. 🗣️

---

### 3. Scanning and Reconnaissance 🔦

Focus:

* Port scanning
* Service discovery
* Repeated connection attempts
* Internal host probing
* Tool-generated traffic

Main lab VM for testing:

```text
Parrot VM
```

Detection value:

Parrot can generate controlled testing traffic so I can observe how scans appear in Suricata alerts and firewall logs.

Important note:

> Testing stays inside the lab. The outside world is not a practice dummy.

---

### 4. Possible C2-Like Behavior 📡

Focus:

* Repeated outbound connections
* Beacon-like timing
* Suspicious URI patterns
* Odd headers
* Automated client behavior
* Unusual external destinations

Detection idea:

> One packet is a dot.
> Repeated patterns become a trail.
> Trails become hunting questions. 🧭

---

## 🧪 Validation Workflow

Each Suricata rule should eventually be validated in the lab.

```text
Choose network behavior
        ↓
Write Suricata rule
        ↓
Generate safe lab traffic
        ↓
Confirm alert fires
        ↓
Review alert fields
        ↓
Compare with firewall logs
        ↓
Compare with endpoint logs
        ↓
Document result
        ↓
Tune rule if noisy
```

Validation is important because a rule that looks good but never fires is a decorative fish tank.

Pretty, but not useful. 🐠

---

## 🧰 Lab Systems Used for Network Testing

| System            | Network Detection Use                                          |
| ----------------- | -------------------------------------------------------------- |
| OPNsense          | Firewall logs, traffic control, segmentation                   |
| Windows Client    | Endpoint traffic generation                                    |
| Admin Workstation | Admin script and PowerShell traffic testing                    |
| Ubuntu Server     | Server-side services and log collection                        |
| Parrot VM         | Controlled security testing and scanning                       |
| REMnux VM         | Network artifact analysis and malware-lab support              |
| FLARE VM          | Windows malware-analysis support and file-driven network clues |
| SIFT VM           | Post-incident forensic context when needed                     |

Suricata does not work alone.

It becomes more powerful when combined with:

* Endpoint logs
* Firewall logs
* DNS logs
* Process data
* Forensic timelines
* Detection writeups

That is how one packet becomes part of a larger story. 📖

---

## 🧠 Useful Alert Fields to Document

When a Suricata alert fires, useful details may include:

| Field                    | Why It Helps                         |
| ------------------------ | ------------------------------------ |
| Timestamp                | When the activity happened           |
| Source IP                | Internal host that initiated traffic |
| Source Port              | Client-side connection detail        |
| Destination IP           | Remote target                        |
| Destination Port         | Service being contacted              |
| Protocol                 | HTTP, DNS, TLS, TCP, UDP, etc.       |
| Alert Message            | Rule name and alert summary          |
| SID                      | Rule identifier                      |
| HTTP Host                | Domain or host header                |
| URI                      | Requested path                       |
| User-Agent               | Client/tool clue                     |
| Flow Direction           | Traffic direction                    |
| Packet or PCAP Reference | Evidence for validation              |

Good alert fields turn “something happened” into “here is what happened.” 🧾

---

## 🧩 Relationship with Other Folders

Suricata connects to the rest of the repository.

| Folder     | Relationship                                                |
| ---------- | ----------------------------------------------------------- |
| `sigma/`   | Endpoint behavior can support network alerts                |
| `kql/`     | KQL can investigate matching endpoint or Defender telemetry |
| `yara/`    | File indicators may explain network behavior                |
| `python/`  | Scripts can parse Suricata alerts or PCAP metadata          |
| `reports/` | Writeups explain the detection and validation process       |
| `tests/`   | Safe test traffic notes and expected alert results          |
| `docs/`    | Lab architecture explains where traffic comes from          |

Example combined investigation:

```text
Suricata alert fires
        ↓
Check source IP
        ↓
Map IP to hostname
        ↓
Review endpoint process logs
        ↓
Check PowerShell or browser activity
        ↓
Review DNS/firewall logs
        ↓
Document full behavior chain
```

This is how network alerts become investigation stories instead of isolated packet confetti. 🎊

---

## 🧾 Rule Documentation Template

Each rule should have notes like this in a matching report later:

```markdown
# Detection Writeup: <Rule Name>

## Summary

What does this rule detect?

## Why It Matters

Why could this traffic be suspicious?

## Rule Location

`suricata/<folder>/<rule_name>.rules`

## Required Visibility

What traffic/protocol must Suricata inspect?

## Expected Alert Fields

Source IP, destination IP, protocol, URI, User-Agent, SID, timestamp.

## False Positives

What legitimate activity may trigger this?

## Validation Steps

How was this tested safely in the lab?

## Investigation Steps

What should an analyst check next?
```

---

## ✅ Suricata Rule Quality Checklist

Before adding a rule, check:

* [ ] Does the rule have a clear `msg`?
* [ ] Is the protocol correct?
* [ ] Is the traffic direction correct?
* [ ] Is the content match specific enough?
* [ ] Does the rule use a unique SID?
* [ ] Is the revision number correct?
* [ ] Is the classtype reasonable?
* [ ] Are false positives documented?
* [ ] Was it tested or marked as lab-only?
* [ ] Is the rule stored in the right folder?
* [ ] Can another analyst understand the purpose?
* [ ] Would this alert be useful, or just noisy confetti?

Because “alert everything” is not detection engineering.

That is just a network smoke machine. 💨

---

## 🚦 Rule Status Thinking

Suricata rules in this repo may fall into these informal stages:

| Stage     | Meaning                                       |
| --------- | --------------------------------------------- |
| Draft     | Rule is written but not tested                |
| Lab Test  | Rule is being tested with safe traffic        |
| Validated | Rule fired successfully in lab                |
| Tuned     | Rule was improved after false-positive review |
| Retired   | Rule is no longer useful or replaced          |

Suggested comment above custom rules:

```text
# Status: Draft
# Purpose: Detect suspicious PowerShell User-Agent in HTTP traffic
# Validation: Not yet validated
```

Example:

```text
# Status: Draft
# Author: PP
# Purpose: Detect suspicious User-Agent strings commonly associated with scripted HTTP activity
# Notes: Lab-use only. Validate before using anywhere else.

alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"LAB Suspicious User-Agent Observed"; flow:to_server,established; http.user_agent; content:"PowerShell"; nocase; classtype:trojan-activity; sid:1000001; rev:1;)
```

---

## 🔐 Safety and Ethics

This folder must not contain:

* Real client traffic
* Company PCAPs
* Sensitive firewall logs
* Internal production IPs
* Proprietary detections
* Credentials
* API keys
* Private incident data
* Real malware infrastructure details from active cases

Allowed content:

* Lab-created rules
* Public-learning examples
* Sanitized test notes
* Rules written from personal research
* Safe validation traffic
* Non-sensitive custom SIDs

Golden rule:

> The repo should show detection skill, not leak network laundry. 🧺🔐

---

## 🧠 Personal Suricata Notes

Things to remember:

* Start simple.
* Validate safely.
* Use unique SIDs.
* Document false positives.
* Direction matters.
* Protocol matters.
* Overly broad content matches create noise.
* Network alerts need endpoint context.
* DNS is useful but slippery.
* HTTP headers can be revealing.
* PCAPs are evidence snacks.
* Parrot should only poke inside the lab.
* REMnux can help analyze suspicious network artifacts.
* OPNsense helps understand traffic flow.
* Suricata rules should be useful, not dramatic.

Also:

> Packets are tiny travelers.
> Suricata is the customs officer with questions. 🛃

---

## 🗺️ Planned Suricata Rules

| Rule                               | Purpose                                       | Status    |
| ---------------------------------- | --------------------------------------------- | --------- |
| `suspicious_user_agent.rules`      | Detect suspicious scripted User-Agent strings | 🟡 Draft  |
| `powershell_user_agent.rules`      | Detect PowerShell-based HTTP activity         | ⚪ Planned |
| `python_requests_user_agent.rules` | Detect Python requests traffic                | ⚪ Planned |
| `suspicious_dns_query.rules`       | Detect suspicious DNS patterns                | ⚪ Planned |
| `possible_dns_tunneling.rules`     | Detect DNS tunneling indicators               | ⚪ Planned |
| `internal_port_scan.rules`         | Detect internal scanning activity             | ⚪ Planned |
| `suspicious_http_post.rules`       | Detect unusual HTTP POST behavior             | ⚪ Planned |
| `possible_c2_beaconing.rules`      | Detect repeated outbound connection patterns  | ⚪ Planned |

---

## 🏁 Final Note

This Suricata folder is where network behavior becomes detection logic.

The mission is not to create noisy rules that alert on every packet with a personality.

The mission is to build clear, tested, explainable network detections that answer:

* Who communicated?
* With what destination?
* Over which protocol?
* Why is it suspicious?
* What field triggered the alert?
* What should an analyst check next?
* Does endpoint telemetry support the network alert?

Every good network alert should be a starting point for investigation.

Not a panic button.

Not a packet horoscope.

A clue. 🔍

And when the packet trail gets weird, Suricata raises a fin and says:

> “I saw that.” 🦈🚨

