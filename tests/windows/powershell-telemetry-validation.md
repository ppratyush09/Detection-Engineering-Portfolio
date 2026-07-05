# 🧪 Validation Test: PowerShell Telemetry and Encoded Command Visibility

> “First we run the command. Then we find the log. Then we teach the detection owl what to hoot at.” 🦉⚡

This document records a PowerShell telemetry validation test performed in the lab.

The goal was to confirm that normal PowerShell execution, encoded PowerShell execution, and PowerShell script block logging can be observed through Windows telemetry.

This is not a finished detection rule yet.

This is the evidence-building stage:

```text
Behavior generated
        ↓
Telemetry observed
        ↓
Commands documented
        ↓
Detection logic planned
        ↓
Sigma and KQL later
```

---

## 🎯 Test Objective

Validate whether PowerShell activity is visible in lab telemetry.

The specific objectives were:

* Confirm normal PowerShell execution appears in Sysmon process creation logs
* Confirm encoded PowerShell execution appears in Sysmon process creation logs
* Confirm PowerShell Script Block Logging events are available
* Identify which log sources are useful for future Sigma and KQL detections
* Document the exact commands tested

---

## 🧠 Why This Test Matters

PowerShell is commonly used by both administrators and attackers.

That makes it a high-value telemetry source for detection engineering.

PowerShell can be used for:

* System administration
* Automation
* Discovery
* Script execution
* Payload download
* Obfuscation
* Defense evasion
* Post-exploitation activity

Encoded PowerShell is especially important because attackers may use encoded command parameters to hide the command content from quick visual inspection.

Important note:

> PowerShell is not evil.
> PowerShell without context is spicy. 🌶️

The goal of this test was not to prove maliciousness.

The goal was to prove visibility.

---

## 🧪 Lab Environment

| Item                    | Details                                               |
| ----------------------- | ----------------------------------------------------- |
| Lab Phase               | Phase 02: Windows Telemetry / Phase 03: Sigma and KQL |
| Test Category           | PowerShell telemetry validation                       |
| Host Tested             | `WIN11-USER01`                                        |
| Telemetry Source 1      | `Microsoft-Windows-Sysmon/Operational`                |
| Telemetry Source 2      | `Microsoft-Windows-PowerShell/Operational`            |
| Sysmon Event Tested     | Event ID `1` - Process Creation                       |
| PowerShell Event Tested | Event ID `4104` - Script Block Logging                |
| Safety Level            | Benign lab commands only                              |
| Detection Status        | Telemetry observed, detection logic planned           |

---

## 🔐 Safety Notice

The commands used in this test were benign and executed only inside the lab.

This test did **not** include:

* Malware execution
* Payload download
* Credential access
* Persistence creation
* Lateral movement
* Destructive commands
* Public target interaction
* Company or client data

This was a safe telemetry-generation test.

Tiny safety rule:

> Generate logs, not chaos. 🧯

---

# ✅ Test 1: Normal PowerShell Baseline

## Purpose

The purpose of this test was to confirm that normal PowerShell execution appears in Sysmon process creation telemetry.

This gives a baseline before testing suspicious or encoded PowerShell behavior.

---

## Run On

```text
WIN11-USER01
```

---

## Command Executed

```powershell
powershell -NoProfile -Command "Get-Process | Select-Object -First 5"
```

---

## What This Command Does

This command starts PowerShell without loading the user profile and runs a harmless command to display the first five running processes.

It is a safe baseline test.

Expected behavior:

```text
powershell.exe should execute normally and appear as a process creation event.
```

---

## Telemetry Check Command

```powershell
Get-WinEvent -FilterHashtable @{
    LogName="Microsoft-Windows-Sysmon/Operational"
    Id=1
} -MaxEvents 5 | Select-Object TimeCreated, Message | Format-List
```

---

## Expected Output

The output should show a Sysmon Event ID `1` process creation event containing:

```text
powershell.exe
```

Expected evidence:

| Field / Evidence | Expected Value                         |
| ---------------- | -------------------------------------- |
| Log Source       | `Microsoft-Windows-Sysmon/Operational` |
| Event ID         | `1`                                    |
| Process          | `powershell.exe`                       |
| Command Line     | PowerShell command visible             |
| Host             | `WIN11-USER01`                         |

---

## Observed Output

The normal PowerShell baseline test was visible in Sysmon process creation output.

Observed result:

| Observation                  | Result |
| ---------------------------- | ------ |
| Sysmon Event ID 1 generated  | ✅ Yes  |
| `powershell.exe` visible     | ✅ Yes  |
| Command execution visible    | ✅ Yes  |
| Baseline telemetry confirmed | ✅ Yes  |

---

## What We Learned

* Sysmon is capturing process creation events.
* Normal PowerShell execution is visible.
* Event ID `1` is useful for PowerShell process monitoring.
* This baseline helps compare normal PowerShell activity with encoded PowerShell activity.
* Before writing suspicious detections, it is useful to know what normal telemetry looks like.

Tiny lesson:

> Baseline first. Suspicion later. Otherwise everything looks like a dragon. 🐉

---

# ⚡ Test 2: Suspicious Encoded PowerShell

## Purpose

The purpose of this test was to confirm that PowerShell execution using `-EncodedCommand` appears in Sysmon process creation telemetry.

This behavior is important because encoded commands are commonly used in suspicious PowerShell activity.

---

## Run On

```text
WIN11-USER01
```

---

## Commands Executed

```powershell
$Command = 'Write-Output "Detection Engineering Lab Test"'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Command)
$EncodedCommand = [Convert]::ToBase64String($Bytes)
powershell.exe -NoProfile -EncodedCommand $EncodedCommand
```

---

## What These Commands Do

These commands perform four steps:

| Step | Action                                    |
| ---- | ----------------------------------------- |
| 1    | Create a benign PowerShell command        |
| 2    | Convert the command into Unicode bytes    |
| 3    | Convert the bytes into Base64             |
| 4    | Execute PowerShell with `-EncodedCommand` |

The decoded command is harmless:

```powershell
Write-Output "Detection Engineering Lab Test"
```

The suspicious-looking part is the execution style:

```text
powershell.exe -NoProfile -EncodedCommand <Base64 string>
```

This creates useful telemetry for detection engineering without performing malicious activity.

---

## Telemetry Search Command

```powershell
Get-WinEvent -FilterHashtable @{
    LogName="Microsoft-Windows-Sysmon/Operational"
    Id=1
} -MaxEvents 30 | Where-Object {
    $_.Message -match "EncodedCommand"
} | Select-Object TimeCreated, Message | Format-List
```

---

## Expected Output

The output should show a Sysmon Event ID `1` process creation event where the command line includes:

```text
powershell.exe
```

and:

```text
-EncodedCommand
```

Expected evidence:

| Field / Evidence | Expected Value                         |
| ---------------- | -------------------------------------- |
| Log Source       | `Microsoft-Windows-Sysmon/Operational` |
| Event ID         | `1`                                    |
| Process          | `powershell.exe`                       |
| Command Line     | Contains `-EncodedCommand`             |
| Host             | `WIN11-USER01`                         |
| Behavior Type    | Encoded PowerShell execution           |

---

## Observed Output

The encoded PowerShell execution was visible in Sysmon process creation output.

Observed result:

| Observation                         | Result |
| ----------------------------------- | ------ |
| Sysmon Event ID 1 generated         | ✅ Yes  |
| `powershell.exe` visible            | ✅ Yes  |
| `-EncodedCommand` visible           | ✅ Yes  |
| Filter matched expected event       | ✅ Yes  |
| Encoded command telemetry confirmed | ✅ Yes  |

---

## What We Learned

* Encoded PowerShell execution is visible in Sysmon Event ID `1`.
* The command line contains `-EncodedCommand`, which can be used for detection logic.
* This behavior can become a Sigma process creation rule.
* This behavior can become a KQL hunting query.
* The test confirms that the lab has enough telemetry to detect encoded PowerShell at a basic level.

Detection thought:

> The encoded command switch is the smoke.
> Context decides whether there is fire. 🔥

---

# 📜 Test 3: PowerShell Script Block Logging

## Purpose

The purpose of this test was to confirm whether PowerShell Script Block Logging events are available.

Script Block Logging is useful because it may show PowerShell script content, not just the process command line.

This can provide deeper visibility into what PowerShell actually executed.

---

## Command Executed

```powershell
Get-WinEvent -FilterHashtable @{
    LogName="Microsoft-Windows-PowerShell/Operational"
    Id=4104
} -MaxEvents 10 | Select-Object TimeCreated, Id, Message | Format-List
```

---

## What This Command Does

This command searches the PowerShell Operational log for Event ID `4104`.

Event ID `4104` represents PowerShell Script Block Logging.

Expected behavior:

```text
PowerShell script block events should appear if script block logging is enabled and events exist.
```

---

## Expected Output

The output should show PowerShell script block events from:

```text
Microsoft-Windows-PowerShell/Operational
```

with Event ID:

```text
4104
```

Expected evidence:

| Field / Evidence | Expected Value                                    |
| ---------------- | ------------------------------------------------- |
| Log Source       | `Microsoft-Windows-PowerShell/Operational`        |
| Event ID         | `4104`                                            |
| Event Type       | Script Block Logging                              |
| Fields           | `TimeCreated`, `Id`, `Message`                    |
| Visibility       | PowerShell script content or script block details |

---

## Observed Output

PowerShell Script Block Logging events were expected from the query.

Observed result:

| Observation                              | Result |
| ---------------------------------------- | ------ |
| PowerShell Operational log queried       | ✅ Yes  |
| Event ID `4104` checked                  | ✅ Yes  |
| Script block logging visibility reviewed | ✅ Yes  |
| Useful for deeper PowerShell analysis    | ✅ Yes  |

```text
Event ID 4104 output was observed
```

---

## What We Learned

* PowerShell process creation and PowerShell script content are different telemetry layers.
* Sysmon Event ID `1` shows PowerShell process execution.
* PowerShell Event ID `4104` can show script block content if logging is enabled.
* Script Block Logging is valuable for understanding what PowerShell executed.
* For detection engineering, process logs and script block logs can support each other.

Telemetry thought:

> Sysmon shows that PowerShell ran.
> Script Block Logging may show what PowerShell said. 🗣️

---

# 📊 Overall Test Results

| Test                       | Telemetry Source       | Event ID | Result     | Detection Value                                 |
| -------------------------- | ---------------------- | -------: | ---------- | ----------------------------------------------- |
| Normal PowerShell baseline | Sysmon Operational     |        1 | ✅ Observed | Confirms baseline PowerShell process visibility |
| Encoded PowerShell         | Sysmon Operational     |        1 | ✅ Observed | Confirms `-EncodedCommand` visibility           |
| Script Block Logging       | PowerShell Operational |     4104 | ✅ Checked  | Helps review PowerShell script content          |

---

## 📌 Important Fields for Future Detection

| Field                                       | Why It Matters                                           |
| ------------------------------------------- | -------------------------------------------------------- |
| `Image` / `FileName`                        | Confirms PowerShell executable                           |
| `CommandLine` / `ProcessCommandLine`        | Shows `-EncodedCommand` or other suspicious switches     |
| `ParentImage` / `InitiatingProcessFileName` | Shows what launched PowerShell                           |
| `User` / `AccountName`                      | Shows user context                                       |
| `ComputerName` / `DeviceName`               | Shows affected host                                      |
| `ProcessId`                                 | Helps correlate process activity                         |
| `ParentProcessId`                           | Helps reconstruct process tree                           |
| `UtcTime` / `Timestamp`                     | Shows when the activity happened                         |
| `EventID`                                   | Confirms the log type                                    |
| `Message`                                   | Contains the full event details in `Get-WinEvent` output |

---

## 🛡️ Detection Logic Supported

This test supports future detection logic for:

```text
PowerShell executable + encoded command parameter in command line
```

Possible detection conditions:

| Condition                               | Purpose                                 |
| --------------------------------------- | --------------------------------------- |
| Process image contains `powershell.exe` | Confirms PowerShell execution           |
| Command line contains `-EncodedCommand` | Detects encoded command execution       |
| Command line contains `-enc`            | Detects short encoded command syntax    |
| Command line contains `/enc`            | Detects alternate encoded command style |
| Parent process is unusual               | Adds suspicious context                 |
| User or host is unusual                 | Adds investigation priority             |

---

## 📁 Planned Related Files

These files should be created after this validation note:

```text
sigma/windows/process_creation/suspicious_powershell_encoded_command.yml
kql/windows/suspicious_powershell_encoded_command.kql
reports/suspicious_powershell_encoded_command.md
```

Current priority:

```text
1. Document test commands
2. Document observed telemetry
3. Identify useful fields
4. Write Sigma rule
5. Write KQL query
6. Write detection report
```

---

## 🧯 False Positive Considerations

Encoded PowerShell can appear in legitimate environments.

Possible false positives:

* Administrative scripts
* Software deployment tools
* Endpoint management platforms
* Security automation
* Helpdesk scripts
* Monitoring tools
* Scheduled tasks
* Internal IT automation

Tuning ideas for later:

* Review parent process
* Review user context
* Review host role
* Check whether the encoded content can be decoded safely
* Look for network activity after execution
* Look for file creation after execution
* Compare against known admin automation
* Combine with suspicious parent-child process patterns

Important:

> The encoded switch is suspicious.
> The surrounding activity decides how loud the alert should be. 🦉

---

## 🔎 Analyst Investigation Questions

If this behavior is detected later, an analyst should ask:

1. Which host executed PowerShell?
2. Which user ran the command?
3. What parent process launched PowerShell?
4. Was this expected administrative activity?
5. Can the encoded content be decoded safely?
6. Did PowerShell connect to the network?
7. Did PowerShell create or modify files?
8. Did it create persistence?
9. Did similar activity happen on other hosts?
10. Was this part of a larger suspicious sequence?

---

## 🧠 Lessons Learned

* Normal PowerShell should be baselined before suspicious PowerShell testing.
* Sysmon Event ID `1` is useful for process creation visibility.
* Encoded PowerShell using `-EncodedCommand` is visible in Sysmon process creation events.
* Command-line visibility is critical for detecting encoded PowerShell.
* PowerShell Script Block Logging Event ID `4104` provides deeper visibility into PowerShell script content.
* Process telemetry and PowerShell logging complement each other.
* The lab can now support basic PowerShell detection development.
* Sigma and KQL should be written after confirming telemetry exists.

Tiny lesson:

> Commands are the input.
> Logs are the evidence.
> Rules are the memory. 📚

---

## 🚀 Next Steps

* [ ] Add sanitized event output details from Sysmon Event ID `1`
* [ ] Confirm whether Event ID `4104` produced script block output
* [ ] Create Sigma rule for encoded PowerShell
* [ ] Create matching KQL query
* [ ] Create detection writeup under `reports/`
* [ ] Test the same behavior on `ADMIN01`
* [ ] Compare normal PowerShell versus encoded PowerShell activity
* [ ] Later forward logs to a SIEM for validation

---

## 🏁 Final Note

This validation confirms an important early detection engineering milestone:

```text
A safe behavior was generated.
The lab produced telemetry.
The event was observed.
The commands were documented.
Detection logic will come next.
```

This is how a detection begins.

Not with a fancy rule.

With evidence.

The alert owl is still in training, but it has found its first breadcrumb. 🦉📜
