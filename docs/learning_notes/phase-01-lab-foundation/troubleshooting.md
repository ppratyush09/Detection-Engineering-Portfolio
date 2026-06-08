# 🧯 Phase 01: Troubleshooting Notes

> “Troubleshooting is just detective work where the suspect is usually DNS, DHCP, or my own confidence.” 🕵️‍♂️📡

This file documents issues, errors, fixes, and lessons learned while building the lab foundation.

The goal is not to hide mistakes.

The goal is to turn every broken network adapter, failed domain join, strange DHCP lease, and suspiciously silent ping into useful learning evidence.

Because in a lab:

> If it breaks, document it.
> If it works, document why.
> If it works randomly, document it twice and stare at it suspiciously. 👀

---

## 🎯 Purpose

This troubleshooting file tracks:

* What went wrong
* What symptoms appeared
* What caused the issue
* What fixed it
* What commands helped
* What screenshots or notes were useful
* What I should remember next time

This is useful because lab problems often repeat wearing different hats.

Today it is DNS.
Tomorrow it is also DNS, but with sunglasses. 🕶️

---

## 🧠 Troubleshooting Philosophy

The lab should be treated like a small enterprise environment.

When something fails, avoid random clicking.

Use a structured flow:

```text
Observe the symptom
        ↓
Identify affected system
        ↓
Check network basics
        ↓
Check DNS
        ↓
Check gateway/routing
        ↓
Check firewall rules
        ↓
Check services
        ↓
Fix one thing at a time
        ↓
Retest
        ↓
Document the lesson
```

Golden rule:

> Change one thing at a time.
> If I change five things and it works, I learned almost nothing. 🧪

---

## 🧾 Troubleshooting Log Template

Use this template for each issue.

````markdown
## Issue: <Short issue title>

### Date

YYYY-MM-DD

### Affected System

- VM:
- Role:
- IP Address:
- Network:

### Symptom

What did I see?

Example:

- Cannot ping gateway
- Cannot join domain
- No internet access
- DHCP lease missing
- DNS lookup failing
- VM cannot reach DC

### Expected Behavior

What should have happened?

### Checks Performed

- [ ] Checked IP configuration
- [ ] Checked gateway
- [ ] Checked DNS
- [ ] Checked firewall
- [ ] Checked VM network adapter
- [ ] Checked service status
- [ ] Checked logs

### Commands Used

```text
<commands used>
````

### Root Cause

What caused the issue?

### Fix Applied

What solved it?

### Validation

How did I confirm the fix worked?

### Lesson Learned

What should I remember next time?

````

---

## 🚦 Quick Triage Checklist

Before going deep into the rabbit hole, check these basics.

| Check | Command / Location | Why It Matters |
|---|---|---|
| IP address | `ipconfig /all` or `ip addr` | Confirms the machine has a valid address |
| Gateway | `ipconfig /all`, `ip route` | Confirms the route out of the subnet |
| DNS server | `ipconfig /all`, `/etc/resolv.conf` | Critical for domain and name resolution |
| Ping gateway | `ping <gateway-ip>` | Confirms local network reachability |
| Ping DC | `ping <dc-ip>` | Confirms domain controller reachability |
| DNS lookup | `nslookup <domain>` | Confirms domain resolution |
| DHCP lease | OPNsense DHCP leases | Confirms address assignment |
| Firewall logs | OPNsense logs | Confirms traffic allowed/blocked |
| VM adapter | VMware settings | Confirms VM is connected to correct network |
| Time sync | Windows time settings | Helps avoid domain authentication weirdness |

Mini wisdom:

> Always check the boring things first.  
> The boring thing is guilty more often than the dramatic thing. 🧃

---

# 1. Issue: VM Gets Wrong IP Address

## Symptom

A VM receives an IP address that does not belong to the lab network.

Example signs:

- VM cannot reach OPNsense LAN IP
- VM cannot reach the Domain Controller
- VM appears on the wrong subnet
- VM has internet but cannot see lab machines
- DHCP lease does not appear in OPNsense

---

## Likely Causes

| Cause | Explanation |
|---|---|
| Wrong VMware network adapter | VM connected to NAT/bridged instead of lab LAN |
| DHCP from wrong source | Host/VMware DHCP may be assigning IP |
| Static IP misconfigured | Manual IP does not match lab subnet |
| OPNsense LAN not selected | VM is not connected to internal lab network |
| Adapter disconnected | VM network adapter is not connected |

---

## Checks

### Windows

```powershell
ipconfig /all
route print
ping <opnsense-lan-ip>
ping <dc-ip>
````

### Linux

```bash
ip addr
ip route
ping <opnsense-lan-ip>
ping <dc-ip>
```

### VMware

Check:

```text
VM Settings → Network Adapter
```

Confirm it is connected to the correct lab network.

### OPNsense

Check:

```text
Services → DHCPv4 → Leases
```

---

## Fix

* Connect the VM to the correct lab network adapter
* Renew DHCP lease
* Confirm OPNsense DHCP is assigning the IP
* If static IP is used, verify:

  * IP address
  * Subnet mask
  * Gateway
  * DNS server

Windows renew command:

```powershell
ipconfig /release
ipconfig /renew
ipconfig /all
```

Linux renew examples:

```bash
sudo dhclient -r
sudo dhclient
```

---

## Lesson Learned

If a VM gets the wrong IP, do not immediately blame Windows, Linux, or the firewall goblin.

First check the VMware adapter.

The VM may simply be standing in the wrong room. 🚪

---

# 2. Issue: Cannot Reach OPNsense Gateway

## Symptom

A lab machine cannot ping or reach the OPNsense LAN IP.

Example:

```powershell
ping <opnsense-lan-ip>
```

fails.

---

## Likely Causes

| Cause                        | Explanation                          |
| ---------------------------- | ------------------------------------ |
| Wrong VM network             | Client is not on lab LAN             |
| OPNsense LAN IP incorrect    | Wrong gateway IP used                |
| OPNsense not running         | Firewall VM is powered off           |
| Firewall interface issue     | LAN interface not assigned correctly |
| Client IP/subnet mismatch    | Client not in same subnet            |
| Local firewall blocking ping | ICMP blocked locally                 |

---

## Checks

On the client:

```powershell
ipconfig /all
ping <opnsense-lan-ip>
route print
```

On Linux:

```bash
ip addr
ip route
ping <opnsense-lan-ip>
```

On OPNsense:

```text
Interfaces → Overview
Interfaces → Assignments
Firewall → Log Files
Services → DHCPv4 → Leases
```

---

## Fix

* Confirm OPNsense is powered on
* Confirm LAN interface is assigned correctly
* Confirm client is on correct lab network
* Confirm client IP is in same subnet
* Confirm gateway is correct
* Restart client network adapter if needed
* Renew DHCP lease

---

## Lesson Learned

If the gateway is unreachable, the lab road system is broken.

Do not test domain join yet.

Do not install tools yet.

Fix the road first. 🛣️

---

# 3. Issue: Client Cannot Join Domain

## Symptom

Windows Client or Admin Workstation cannot join the Active Directory domain.

Possible errors:

* Domain controller could not be contacted
* DNS name does not exist
* Network path not found
* Authentication failure
* Domain join fails even though ping works

---

## Likely Causes

| Cause                              | Explanation                   |
| ---------------------------------- | ----------------------------- |
| Wrong DNS server                   | Client is not using DC as DNS |
| DC unreachable                     | Network path to DC is broken  |
| Domain name typed incorrectly      | Wrong FQDN or NetBIOS name    |
| Time mismatch                      | Kerberos may fail             |
| DC services not running            | AD DS or DNS issue            |
| Firewall blocking required traffic | Domain ports not reachable    |
| Client on wrong network            | VM adapter issue              |

---

## Checks

On Windows Client:

```powershell
ipconfig /all
ping <dc-ip>
nslookup <domain-name>
nltest /dsgetdc:<domain-name>
whoami
```

Check DNS server:

```text
Preferred DNS should be the Domain Controller IP
```

On Domain Controller:

```powershell
dcdiag
ipconfig /all
nslookup <domain-name>
```

---

## Fix

* Set client DNS to Domain Controller IP
* Confirm DC has static IP
* Confirm domain name is correct
* Confirm client and DC are on same lab network
* Confirm time is close between systems
* Restart DNS service if needed
* Retry domain join

---

## Lesson Learned

In Active Directory labs, DNS is not “one setting.”

DNS is the floor, ceiling, doors, windows, and sometimes the ghost in the hallway. 👻

Always check DNS first.

Then check DNS again.

---

# 4. Issue: DNS Resolution Fails

## Symptom

The machine can ping IP addresses but cannot resolve domain names.

Examples:

```powershell
ping 8.8.8.8
```

works, but:

```powershell
nslookup example.com
```

fails.

For domain systems:

```powershell
nslookup <domain-name>
```

fails.

---

## Likely Causes

| Cause                       | Explanation                                 |
| --------------------------- | ------------------------------------------- |
| Wrong DNS server            | Client points to external DNS instead of DC |
| DNS service stopped         | DC DNS service not running                  |
| Forwarders missing          | Internet names cannot resolve               |
| DHCP option wrong           | DHCP gave wrong DNS                         |
| OPNsense DNS settings wrong | DNS forwarding/resolution issue             |
| Static DNS mistake          | Manual DNS typo                             |

---

## Checks

Windows:

```powershell
ipconfig /all
nslookup <domain-name>
nslookup example.com
```

Linux:

```bash
cat /etc/resolv.conf
nslookup <domain-name>
dig <domain-name>
```

Domain Controller:

```powershell
Get-Service DNS
dcdiag /test:dns
```

---

## Fix

* For domain clients, set DNS to DC IP
* Configure DNS forwarders on DC if internet resolution is needed
* Update DHCP DNS option
* Renew DHCP lease
* Restart DNS service if needed
* Confirm DNS zones exist

---

## Lesson Learned

Ping by IP proves the road exists.

DNS proves the signboards exist.

Without signboards, everyone drives around confused. 🪧

---

# 5. Issue: No Internet Access From Lab Machine

## Symptom

A lab VM can reach internal systems but cannot access internet.

Examples:

* Windows Update fails
* Browser cannot open websites
* `ping 8.8.8.8` fails
* DNS works internally but external domains fail
* OPNsense WAN seems disconnected

---

## Likely Causes

| Cause                    | Explanation                        |
| ------------------------ | ---------------------------------- |
| OPNsense WAN issue       | Firewall cannot reach outside      |
| NAT missing or broken    | Traffic not translated outbound    |
| Firewall rule missing    | LAN traffic blocked                |
| Wrong gateway            | Client gateway not set to OPNsense |
| DNS forwarder issue      | External domain resolution broken  |
| Host network unavailable | VMware host connectivity issue     |

---

## Checks

On client:

```powershell
ipconfig /all
ping <gateway-ip>
ping 8.8.8.8
nslookup example.com
tracert 8.8.8.8
```

On Linux:

```bash
ip route
ping <gateway-ip>
ping 8.8.8.8
dig example.com
traceroute 8.8.8.8
```

On OPNsense:

```text
Interfaces → Overview
System → Gateways
Firewall → Rules
Firewall → NAT → Outbound
Firewall → Log Files
```

---

## Fix

* Confirm OPNsense WAN has internet
* Confirm client gateway is OPNsense LAN IP
* Confirm LAN-to-WAN rule exists
* Confirm NAT is working
* Confirm DNS forwarding/forwarders are working
* Restart network service or renew DHCP

---

## Lesson Learned

Internet failure can be routing, NAT, firewall, or DNS.

Do not fight all four dragons at once.

Pick one. Test. Move. 🐉

---

# 6. Issue: OPNsense DHCP Lease Not Showing

## Symptom

Client is powered on, but no DHCP lease appears in OPNsense.

---

## Likely Causes

| Cause                           | Explanation                     |
| ------------------------------- | ------------------------------- |
| Client not connected to lab LAN | Wrong VMware adapter            |
| Static IP configured            | Client is not requesting DHCP   |
| DHCP disabled on OPNsense       | No DHCP service                 |
| Wrong OPNsense interface        | DHCP enabled on wrong interface |
| Client network adapter disabled | VM adapter issue                |
| Lease not renewed               | Old IP still cached             |

---

## Checks

Client:

```powershell
ipconfig /all
ipconfig /release
ipconfig /renew
```

OPNsense:

```text
Services → DHCPv4 → Leases
Services → DHCPv4 → LAN
Interfaces → LAN
```

VMware:

```text
VM Settings → Network Adapter
```

---

## Fix

* Enable DHCP on correct OPNsense LAN interface
* Connect VM to correct lab network
* Remove wrong static IP if DHCP should be used
* Renew lease
* Restart client network adapter
* Check OPNsense DHCP logs

---

## Lesson Learned

No DHCP lease means either the client never asked, OPNsense never answered, or they are speaking from different rooms.

Networks are social systems with cables. 🧵

---

# 7. Issue: Static IP Misconfiguration

## Symptom

Machine has a static IP but cannot communicate properly.

Possible signs:

* Can ping some hosts but not gateway
* Can reach gateway but not DC
* DNS does not work
* Domain join fails
* Internet does not work

---

## Common Mistakes

| Setting      | Common Mistake                      |
| ------------ | ----------------------------------- |
| IP Address   | Outside the lab subnet              |
| Subnet Mask  | Wrong mask                          |
| Gateway      | Not set to OPNsense LAN IP          |
| DNS          | Not set to DC IP for domain systems |
| Duplicate IP | Another VM uses same IP             |
| Typo         | One digit chaos                     |

---

## Checks

Windows:

```powershell
ipconfig /all
arp -a
ping <gateway-ip>
ping <dc-ip>
nslookup <domain-name>
```

Linux:

```bash
ip addr
ip route
cat /etc/resolv.conf
ping <gateway-ip>
```

---

## Fix

Use the correct values:

```text
IP Address: Must be in lab subnet
Subnet Mask: Match lab subnet
Gateway: OPNsense LAN IP
DNS: Domain Controller IP for domain systems
```

Check for duplicate IPs.

---

## Lesson Learned

Static IPs are useful, but one wrong digit can turn a VM into a silent island. 🏝️

---

# 8. Issue: Time Sync Problems

## Symptom

Domain-related operations fail or behave strangely.

Possible signs:

* Domain login fails
* Kerberos errors
* Authentication issues
* Domain join problems
* Logs have confusing timestamps

---

## Likely Causes

| Cause              | Explanation                   |
| ------------------ | ----------------------------- |
| VM time drift      | VM clock differs from DC      |
| Host time mismatch | Guest sync issue              |
| DC time issue      | Domain time source not stable |
| Snapshot restore   | Restored VM with old time     |

---

## Checks

Windows:

```powershell
time /t
date /t
w32tm /query /status
```

Domain Controller:

```powershell
w32tm /query /status
```

---

## Fix

* Sync time with domain controller
* Restart Windows Time service
* Check VMware time sync settings
* After restoring snapshots, confirm time

Example:

```powershell
w32tm /resync
```

---

## Lesson Learned

Time is a security control.

If time breaks, Kerberos starts acting like a grumpy librarian. 📚

---

# 9. Issue: VM Is Slow or Freezes

## Symptom

VM takes too long to boot, freezes, or performs poorly.

---

## Likely Causes

| Cause                 | Explanation                                           |
| --------------------- | ----------------------------------------------------- |
| Too little RAM        | VM does not have enough memory                        |
| Too many VMs running  | Host resource pressure                                |
| Disk I/O bottleneck   | Storage is overloaded                                 |
| CPU overcommit        | Too many vCPUs assigned overall                       |
| Updates running       | Windows or Linux updates consuming resources          |
| Heavy tools installed | FLARE, SIFT, or analysis tools can be resource-hungry |

---

## Checks

Host machine:

```text
Task Manager → Performance
VMware running VM list
Disk usage
Memory usage
CPU usage
```

Inside VM:

```text
Task Manager
top / htop
df -h
```

---

## Fix

* Shut down unnecessary VMs
* Increase RAM if available
* Reduce unnecessary startup programs
* Wait for updates to finish
* Avoid running all heavy VMs together
* Snapshot before major tool installation
* Keep only required VMs powered on

---

## Lesson Learned

A lab is not a VM buffet.

Turn on only what the current task needs. 🍽️

---

# 10. Issue: Snapshot Confusion

## Symptom

Too many snapshots exist, or snapshot names are unclear.

Examples:

```text
Snapshot 1
Working
Before test
New one
Final
Final fixed
```

This creates confusion during rollback.

---

## Likely Causes

| Cause                        | Explanation                        |
| ---------------------------- | ---------------------------------- |
| No naming convention         | Snapshots named casually           |
| Too many temporary snapshots | Testing snapshots not cleaned      |
| No notes                     | Reason for snapshot forgotten      |
| Repeated experiments         | Multiple similar snapshots created |

---

## Fix

Use naming convention:

```text
<vm-name>-<state>-<purpose>
```

Examples:

```text
dc01-domain-baseline
winclient-domain-joined
opnsense-working-network-baseline
flare-clean-analysis-baseline
```

Document snapshots in:

```text
snapshots.md
```

Delete unclear temporary snapshots after confirming stable baselines.

---

## Lesson Learned

A snapshot without a clear name is a future trap.

It smiles today.

It confuses tomorrow. 🪤

---

# 11. Issue: GitHub Folder Naming or File Naming Mistakes

## Symptom

Files or folders are named inconsistently.

Examples:

```text
ReadMe.md
readme.md
README.md
phase-01-lab-foudation
trouble.md
networksetup.md
```

---

## Why It Matters

In a professional portfolio, naming reflects organization.

Inconsistent names make the repo harder to navigate.

---

## Fix

Use consistent naming.

For README:

```text
README.md
```

For Markdown notes:

```text
lowercase-with-hyphens.md
```

Examples:

```text
network-setup.md
snapshot-notes.md
troubleshooting.md
phase-01-completion-summary.md
```

For rules/scripts:

```text
lowercase_with_underscores.ext
```

Examples:

```text
suspicious_powershell_encoded_command.yml
suspicious_script_obfuscation.yar
ioc_extractor.py
```

---

## Lesson Learned

Clean names are tiny acts of kindness for future investigators.

Also, typos are sneaky little raccoons. 🦝

---

## 🧪 Troubleshooting Records

Add real troubleshooting records below as they happen.

---

## Record 001: DHCP Lease Visibility

### Date

YYYY-MM-DD

### Affected System

* VM:
* Role:
* IP Address:
* Network:

### Symptom

The VM did/did not appear in OPNsense DHCP leases.

### Expected Behavior

The VM should appear in the correct DHCP lease table.

### Checks Performed

* [ ] Checked VM network adapter
* [ ] Checked OPNsense DHCP lease page
* [ ] Checked client IP configuration
* [ ] Renewed DHCP lease
* [ ] Confirmed correct network

### Commands Used

```powershell
ipconfig /all
ipconfig /release
ipconfig /renew
```

### Root Cause

To be updated.

### Fix Applied

To be updated.

### Validation

To be updated.

### Lesson Learned

To be updated.

---

## Record 002: Domain Join Issue

### Date

YYYY-MM-DD

### Affected System

* VM:
* Role:
* IP Address:
* Network:

### Symptom

The Windows machine could not join the domain.

### Expected Behavior

The machine should resolve the domain and successfully join.

### Checks Performed

* [ ] Checked DNS server
* [ ] Checked DC reachability
* [ ] Checked domain name
* [ ] Checked time sync
* [ ] Checked firewall
* [ ] Used `nltest`

### Commands Used

```powershell
ipconfig /all
ping <dc-ip>
nslookup <domain-name>
nltest /dsgetdc:<domain-name>
```

### Root Cause

To be updated.

### Fix Applied

To be updated.

### Validation

To be updated.

### Lesson Learned

To be updated.

---

## Record 003: Internet Access Issue

### Date

YYYY-MM-DD

### Affected System

* VM:
* Role:
* IP Address:
* Network:

### Symptom

The machine could not access the internet.

### Expected Behavior

The machine should reach the internet if allowed by firewall policy.

### Checks Performed

* [ ] Checked gateway
* [ ] Checked DNS
* [ ] Checked OPNsense WAN
* [ ] Checked firewall rules
* [ ] Checked NAT
* [ ] Tested IP and domain connectivity

### Commands Used

```powershell
ping <gateway-ip>
ping 8.8.8.8
nslookup example.com
tracert 8.8.8.8
```

### Root Cause

To be updated.

### Fix Applied

To be updated.

### Validation

To be updated.

### Lesson Learned

To be updated.

---

## 🔐 Safety Notes

Do not include:

* Company IP addresses
* Client logs
* Credentials
* API keys
* Work screenshots
* Real incident details
* Malware samples
* Private hostnames
* Public IPs tied to personal/work infrastructure

Allowed:

* Lab-only private IPs
* Sanitized screenshots
* Troubleshooting steps
* Generic commands
* Lab VM names
* Learning notes
* Safe examples

Golden rule:

> Troubleshooting notes should reveal learning, not secrets. 🔐

---

## ✅ Troubleshooting Checklist

| Task                                       | Status |
| ------------------------------------------ | ------ |
| Common network issues documented           | ✅      |
| Domain join troubleshooting documented     | ✅      |
| DNS troubleshooting documented             | ✅      |
| DHCP troubleshooting documented            | ✅      |
| Internet access troubleshooting documented | ✅      |
| Snapshot confusion documented              | ✅      |
| Safety rules included                      | ✅      |
| Real issue records started                 | ⏳      |
| Future fixes to be added                   | ⏳      |

---

## 🏁 Final Note

Troubleshooting is part of the lab.

The goal is not to avoid every error.

The goal is to become better at diagnosing them.

A good lab builder does not panic when things break.

A good lab builder asks:

> What changed?
> What is affected?
> What still works?
> What logs exist?
> What does the network say?
> What does DNS say?
> Why is DHCP acting like a tiny shape-shifting gremlin? 🧌

Every fix is a lesson.

Every lesson becomes documentation.

Every documented mistake makes the next phase stronger.

The lab may break.

The notes will remember. 📚🔥

