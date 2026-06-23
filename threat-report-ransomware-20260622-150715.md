# Threat Intelligence Report: ransomware

**Generated:** 2026-06-22 15:07:15 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-06-09 → 2026-06-22
**Articles Analyzed:** 14
**Sources:** The Hacker News, Microsoft Security Blog, BleepingComputer, Cybersecurity Blog | SentinelOne, darkreading, Rapid7 Cybersecurity Blog, Krebs on Security, Zero Day Initiative - Blog, BankInfoSecurity.com RSS Syndication

---

## Executive Summary

The two-week window shows the post-LockBit/BlackCat power vacuum continuing to reshape the RaaS landscape: **The Gentlemen**, **INC**, **DragonForce**, and a new entrant **Prinz Eugen** are absorbing displaced affiliates and scaling rapidly using "good enough" tradecraft rather than novel malware. A clear tactical convergence has emerged — BYOVD (bring-your-own-vulnerable-driver) EDR-killing has become a baseline capability across nearly every active group (Gentlemen's GentleKiller, DragonForce's driver chain, INC's filwfp.sys/filnk.sys/fildds.sys), with groups increasingly centralizing and commoditizing these toolkits for affiliates. Attribution work (Krebs/Check Point/PRODAFT/Intel 471) unmasked The Gentlemen's administrator as a Russia-based individual using AI to help build and maintain the group's tooling, reinforcing Rapid7's broader finding that criminal AI-as-a-service is now embedded as a productivity layer across the cybercrime economy rather than a novelty. Microsoft's DART case also illustrates rising attacker sophistication at the incident level: a single ransomware intrusion (Storm-2603) concealed a second, unrelated threat actor operating in parallel — a detection and attribution challenge defenders should anticipate more often. Healthcare, legal services, manufacturing, and construction remain the preferred high-pressure verticals for double-extortion actors, and regulators continue retroactively punishing weak security postures years after ransomware incidents (Spencer's Gifts/Conti, $450K HIPAA fine).

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 0 |
| 🟠 High | 8 |
| 🟡 Medium | 5 |
| 🟢 Low | 1 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2023-3519` | Articles 6, 8 | Citrix NetScaler flaw used by INC affiliates for initial access; corroborated independently by Acronis (via The Hacker News) and Dark Reading's reporting of the same Acronis research. |
| CVE | `CVE-2025-5777` | Articles 6, 8 | Citrix Bleed 2 flaw used by INC for initial access — confirms INC's reliance on edge-device exploitation across both reports. |
| CVE | `CVE-2023-48788` | Articles 6, 8 | Fortinet EMS vulnerability exploited by INC affiliates for initial access. |
| CVE | `CVE-2024-57727` | Articles 6, 8 | SimpleHelp RMM vulnerability used by INC for initial access; SimpleHelp/RMM abuse is a recurring entry vector across multiple groups this period. |
| Driver/File | `PoisonX.sys` | Article 5 (Gentlemen) | BYOVD driver also previously tied to CrowdStrike Falcon EDR kills and a separate Huntress-documented BeyondTrust intrusion — shows driver reuse across unrelated ransomware operators. |
| Threat Actor | `The Gentlemen` | Articles 1, 5, 12 | Consistent reporting across THN's weekly recap, ESET's GentleKiller deep-dive, and Krebs' attribution piece — same group, escalating capability and now de-anonymized leadership. |
| Threat Actor | `DragonForce` | Articles 6, 8 | SentinelOne's weekly roundup and The Hacker News/Symantec report describe the same Backdoor.Turn/Teams-TURN-relay campaign against a U.S. services firm. |

### Shared Threat Actors

#### The Gentlemen (RaaS; admin alias Hastalamuerte/Zeta88)
- **Seen in:** Articles 1, 5, 12
- **Activity:** Emerged mid-2025, now the second most active ransomware group by victim count (504+ claimed victims per ESET/Ransomware.live data, 332+ per Check Point). Centralizes a mature EDR-killer suite (GentleKiller, 8 variants abusing different vulnerable drivers) for affiliates, offers an unusually generous 90/10 affiliate split, and was attributed by Krebs/Check Point/Intel 471/PRODAFT to Alexander Andreevich Yapaev, a 36-year-old Russian national who also previously operated as a Qilin affiliate. PRODAFT additionally found the administrator uses AI to help build and maintain the ransomware and assist post-exploitation activity.

#### DragonForce (ransomware cartel)
- **Seen in:** Articles 6, 8
- **Activity:** Deployed a custom Go-based RAT, Backdoor.Turn, that abuses Microsoft Teams TURN relay infrastructure to hide C2 traffic — the first documented in-the-wild abuse of this technique, building on the theoretical "Ghost Calls" research. Achieved up to two months of undetected dwell time in a U.S. services firm by blending in with legitimate Microsoft Teams traffic, alongside extensive BYOVD use (Huawei audio driver, ABYSSWORKER).

#### INC Ransomware (RaaS)
- **Seen in:** Articles 7, 9
- **Activity:** Grew to 830+ victims since August 2023 by absorbing affiliates displaced from LockBit/BlackCat. Rewrote Windows and Linux/ESXi encryptors in Rust; relies on commodity TTPs (spear-phishing, IABs, edge-device exploitation, LOLBins, Cobalt Strike/AnyDesk/ScreenConnect, Rclone exfiltration) rather than novel tooling. Source code sale in 2024 spawned related families Lynx and Sinobi.

### Campaign Threads

#### Post-LockBit/BlackCat Affiliate Migration
- **Articles:** 5, 7, 9, 12
- **Description:** Multiple independent reports (Acronis on INC, ESET/Krebs on The Gentlemen) converge on the same narrative: the 2024 disruption of LockBit and shutdown of ALPHV/BlackCat created an affiliate vacuum that INC and The Gentlemen have both aggressively filled, alongside Qilin and Akira, reshaping the RaaS leaderboard for 2026 (Qilin 338, Akira 197, The Gentlemen 192-240+, INC 120-124 per ZeroFox/Check Point Q1 2026 data cited across articles).
- **Timeline:** 2024 (LockBit takedown/BlackCat exit scam) → 2025 (Gentlemen and INC affiliate scaling) → Q1 2026 (INC enters ZeroFox top-5; Gentlemen becomes #2 by victim count) → June 2026 (attribution and EDR-killer tooling disclosures).

#### BYOVD-as-a-Service Convergence
- **Articles:** 1, 5, 6, 7, 8, 9
- **Description:** Independent of any single group, BYOVD-based EDR killing has become the default defense-evasion method across the current ransomware top tier — Gentlemen's GentleKiller (8 variants, 400+ processes/48 vendors), DragonForce's driver chain (CVE-2023-52271, CVE-2025-61155, CVE-2025-1055, ABYSSWORKER), and INC's filwfp.sys/filnk.sys/fildds.sys. ESET notes affiliates can integrate newly disclosed driver PoCs "within days" of public release, indicating tight feedback loops between public vulnerability research and criminal tooling.
- **Timeline:** Ongoing/ accelerating through June 2026.

### Emerging Patterns

- **Centralized EDR-killer-as-a-service:** Rather than delegating defense evasion to affiliates, leading RaaS operators (The Gentlemen, and per Huntress' separate BeyondTrust case) are now building and maintaining standardized, impersonation-based EDR-killer frameworks in-house, lowering the technical bar for affiliates and accelerating time-to-encryption. (Supporting articles: 1, 5)
- **Ransomless extortion / no ransom note tradecraft:** New entrant Prinz Eugen deliberately omits a ransom note and moves all extortion communication out-of-band (email, phone, dark-web portal) specifically to reduce forensic artifacts and frustrate automated detection — a notable evolution from earlier "smash and grab" ransomware design. (Supporting article: 4)
- **Legitimate cloud-service C2 abuse:** DragonForce's abuse of Microsoft Teams TURN relays mirrors a broader 2026 trend of attackers tunneling C2 through trusted SaaS infrastructure (Teams, Cloudflare tunnels, Zoho Assist per the Microsoft DART case) to defeat network-based detection. (Supporting articles: 2, 6, 8)
- **AI as a criminal productivity layer, not an autonomous actor:** Both the Rapid7 underground-market research and PRODAFT's findings on The Gentlemen's administrator confirm threat actors are using AI primarily to accelerate routine tasks (malware maintenance, phishing content, post-exploitation assistance) rather than to run autonomous attacks — a shift in degree, not kind. (Supporting articles: 11, 12)
- **Multi-actor intrusions complicating attribution:** Microsoft's DART case of two unrelated threat actors operating in the same compromised environment simultaneously suggests ransomware responders should not assume a single coherent actor behind observed activity, especially in environments with prior unpatched exposure. (Supporting article: 2)

---

## Article Analysis

---

### [1] One intrusion, two cyberattackers: Uncovering parallel threat activity

| Field | Value |
|---|---|
| **Source** | Microsoft Security Blog |
| **Published** | 2026-06-22 |
| **Severity** | 🟠 High |
| **URL** | [microsoft.com/.../one-intrusion-two-cyberattackers](https://www.microsoft.com/en-us/security/blog/2026/06/22/one-intrusion-two-cyberattackers-uncovering-parallel-threat-activity/) |

**Summary:** Microsoft's DART details a ransomware investigation involving Storm-2603 exploiting on-prem SharePoint vulnerabilities for initial access, then deploying Velociraptor, Cloudflare tunnels, Zoho Assist, and SSH-over-VS Code for persistence. Correlation work uncovered a second, unrelated threat actor operating in parallel via DLL sideloading and custom backdoors, complicating attribution and detection.

**Severity Rationale:** Real-world ransomware intrusion against an enterprise environment with privilege escalation, defense evasion via vulnerable drivers, and concurrent multi-actor compromise — high operational impact and detection difficulty.

**Threat Actors:** Storm-2603

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account | Persistence |
| [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunneling | Command and Control |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion / Persistence |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [2] New Prinz Eugen ransomware prioritizes recent files for encryption

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | 2026-06-20 |
| **Severity** | 🟠 High |
| **URL** | [bleepingcomputer.com/.../new-prinz-eugen-ransomware](https://www.bleepingcomputer.com/news/security/new-prinz-eugen-ransomware-prioritizes-recent-files-for-encryption/) |

**Summary:** A new non-RaaS ransomware operation, Prinz Eugen, uses stolen RDP credentials and legitimate RMM tools for hands-on-keyboard intrusions, then deploys a Go-based encryptor (ChaCha20-Poly1305, Argon2id/SHA-256/HKDF-SHA256 KDF) that prioritizes recently modified files and deliberately leaves no ransom note to reduce forensic footprint. At least five victims identified, including Standard Bank (1 BTC demand, refused).

**Severity Rationale:** Active, technically competent new ransomware strain with deliberate anti-forensic design and confirmed real-world victims, though currently small-scale and non-RaaS.

**Threat Actors:** Prinz Eugen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion |
| [T1070](https://attack.mitre.org/techniques/T1070/) | Indicator Removal | Defense Evasion |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** servertool.exe (payload filename); `.prinzeugen` (encrypted file extension)
- **CVEs:** _none_
- **URLs:** _none_

---

### [3] The Gentlemen RaaS Uses GentleKiller EDR Framework Targeting 400 Security Processes

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-06-19/20 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/.../the-gentlemen-raas-uses-gentlekiller](https://thehackernews.com/2026/06/the-gentlemen-raas-uses-gentlekiller.html) |

**Summary:** ESET details The Gentlemen RaaS's in-house GentleKiller EDR-killer framework — eight variants impersonating legitimate security products, each abusing a different vulnerable/malicious driver via BYOVD, targeting 400+ processes across 48 security vendors. The group, led by Alexander Andreevich Yapaev (hastalamuerte/Zeta88), has claimed 504 victims to date and also operates a Rust-based credential stealer (OxideHarvest).

**Severity Rationale:** Centralized, rapidly-iterated EDR-evasion tooling distributed to affiliates significantly lowers the barrier to successful ransomware deployment and has driven the group to #2 by victim count.

**Threat Actors:** The Gentlemen, Alexander Andreevich Yapaev (hastalamuerte/Zeta88)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation |
| [T1036](https://attack.mitre.org/techniques/T1036/) | Masquerading | Defense Evasion |
| [T1555.003](https://attack.mitre.org/techniques/T1555/003/) | Credentials from Web Browsers | Credential Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** eb.sys, nseckrnl.sys, GameDriverX64.sys, stpm_old.sys, stpm_new.sys, dmx.sys, 360netmon_wfp.sys, IMFForceDelete.sys, PoisonX.sys, googleApiUtil64.sys (HexKiller), ThrottleBlood.sys, havoc.sys (HavocKiller)
- **CVEs:** _none_
- **URLs:** _none_

---

### [4] INC Ransomware Emerges as Major RaaS Threat in 2026 with 830+ Victims Since 2023

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-06-18 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/.../inc-ransomware-claims-830-victims-since](https://thehackernews.com/2026/06/inc-ransomware-claims-830-victims-since.html) |

**Summary:** Acronis charts INC's evolution into one of 2026's most prolific RaaS operations (830+ victims since August 2023, 65%+ US-based), driven by Rust-rewritten Windows/Linux/ESXi encryptors, Veeam DPAPI credential dumping, and exploitation of edge-device CVEs. INC's source code sale in 2024 spawned related families Lynx and Sinobi.

**Severity Rationale:** Large, sustained victim count with confirmed exploitation of known, unpatched CVEs in widely deployed enterprise products (Citrix, Fortinet, SimpleHelp) — high real-world risk for unpatched organizations.

**Threat Actors:** INC, Lynx, Sinobi, Qilin, Akira (referenced as competing groups)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1078.002](https://attack.mitre.org/techniques/T1078/002/) | Valid Accounts: Domain Accounts | Initial Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** filwfp.sys, filnk.sys, fildds.sys
- **CVEs:** CVE-2023-3519, CVE-2025-5777, CVE-2023-48788, CVE-2024-57727
- **URLs:** _none_

---

### [5] DragonForce Hackers Abuse Microsoft Teams Relays to Hide Backdoor.Turn C2 Traffic

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-06-18 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/.../dragonforce-hackers-abuse-microsoft](https://thehackernews.com/2026/06/dragonforce-hackers-abuse-microsoft.html) |

**Summary:** Symantec/Carbon Black documented DragonForce ransomware actors using a custom Go-based RAT (Backdoor.Turn) that abuses Microsoft Teams' TURN relay infrastructure to hide C2 traffic, achieving 1-2 months of dwell time at a U.S. services firm. Initial access likely via an SQL/MS-SQL server flaw; extensive BYOVD usage for defense evasion.

**Severity Rationale:** First documented in-the-wild abuse of a novel, hard-to-detect C2 channel by an established ransomware cartel, combined with multi-vector BYOVD evasion and long undetected dwell time.

**Threat Actors:** DragonForce, Hackledorb

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion / Persistence |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1071](https://attack.mitre.org/techniques/T1071/) | Application Layer Protocol | Command and Control |
| [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunneling | Command and Control |
| [T1555.003](https://attack.mitre.org/techniques/T1555/003/) | Credentials from Web Browsers | Credential Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** HWAuidoOs2Ec.sys, wsftprm.sys, GameDriverX64.sys, K7RKScan.sys, ABYSSWORKER, DbgView64.exe (process injection target)
- **CVEs:** CVE-2023-52271, CVE-2025-61155, CVE-2025-1055
- **URLs:** _none_

---

### [6] INC Ransomware Thrives by Mastering the Basics

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-06-17 |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/.../inc-ransomware-thrives-by-mastering-the-basics](https://www.darkreading.com/cyberattacks-data-breaches/inc-ransomware-thrives-by-mastering-the-basics) |

**Summary:** Dark Reading's coverage of the same Acronis research as Article 4, with additional analyst commentary (Acronis, ZeroFox) on INC's victim selection strategy (healthcare, legal, manufacturing), Q1 2026 ranking (#4 with 124 incidents behind Qilin, Akira, The Gentlemen), and defensive recommendations (3-2-1 backup, immutable backups, network segmentation).

**Severity Rationale:** Same underlying threat as Article 4 — confirmed exploitation of known CVEs against high-pressure sectors at scale — corroborated by a second independent source with additional analyst context.

**Threat Actors:** INC, Lynx, Sinobi, Qilin, Akira, RansomHub, Play, Cl0p, The Gentlemen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2025-5777, CVE-2024-57727, CVE-2023-3519, CVE-2023-48788
- **URLs:** _none_

---

### [7] The Good, the Bad and the Ugly in Cybersecurity – Week 25

| Field | Value |
|---|---|
| **Source** | Cybersecurity Blog \| SentinelOne |
| **Published** | 2026-06-19 |
| **Severity** | 🟡 Medium |
| **URL** | [sentinelone.com/.../week-25-7](https://www.sentinelone.com/blog/the-good-the-bad-and-the-ugly-in-cybersecurity-week-25-7/) |

**Summary:** Weekly roundup covering an FBI-led takedown of the "Outsider Enterprise" PhaaS operation and Operation Endgame's disruption of ~15,000 SocGholish-infected WordPress sites/106 servers (linked to Evil Corp), DragonForce's Backdoor.Turn/Teams-relay campaign, and Chinese espionage group UNC6508's breach of REDCap medical research servers via custom malware "InfiniteRed."

**Severity Rationale:** Mixed roundup; the ransomware-relevant content (DragonForce) duplicates Article 5's findings, while the PhaaS takedown and REDCap espionage are non-ransomware but contextually significant.

**Threat Actors:** DragonForce, Evil Corp, UNC6508

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Server Software Component: Web Shell | Persistence |
| [T1114.002](https://attack.mitre.org/techniques/T1114/002/) | Email Forwarding Rule | Collection |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [8] 'Lorem Ipsum' Malware Pivots to ClickFix Delivery

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-06-16 |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/.../lorem-ipsum-malware-clickfix-delivery](https://www.darkreading.com/cyberattacks-data-breaches/lorem-ipsum-malware-clickfix-delivery) |

**Summary:** BlueVoyant assesses the Lorem Ipsum shellcode loader/backdoor campaign — previously delivered via Trojanized, code-signed Teams installers — has pivoted to ClickFix lures on compromised WordPress sites after Microsoft's takedown of the Fox Tempest signing service. BlueVoyant links the campaign with high confidence to Rapid Brigantine (aka Vanilla Tempest/DEV-0832/Vice Society), a ransomware actor tied to Rhysida, BlackCat, Zeppelin, and Quantum Locker.

**Severity Rationale:** Demonstrates rapid operational resilience by a ransomware-affiliated initial-access operation following a major takedown, broadening the victim pool via a new, harder-to-block delivery method.

**Threat Actors:** Rapid Brigantine (Vanilla Tempest / DEV-0832 / Vice Society), Fox Tempest (Forging Marauder)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1204.002](https://attack.mitre.org/techniques/T1204/002/) | User Execution: Malicious File | Execution |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | Execution |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion / Persistence |
| [T1583.001](https://attack.mitre.org/techniques/T1583/001/) | Acquire Infrastructure: Domains | Resource Development |
| [T1583.006](https://attack.mitre.org/techniques/T1583/006/) | Acquire Infrastructure: Web Services | Resource Development |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** LetsDiskuss[.]com (C2 dead-drop)
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [9] ⚡ Weekly Recap: Browser Bugs, EDR Killers, TV Botnet, OpenBSD Flaw, Android Trojan, and More

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-06-22 |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com/.../weekly-recap-browser-bugs-edr-killers](https://thehackernews.com/2026/06/weekly-recap-browser-bugs-edr-killers.html) |

**Summary:** Weekly roundup covering the FortiBleed campaign against 80K+ FortiGate devices, the Klue/Salesforce extortion incident by group "Icarus," the Gentlemen RaaS's GentleKiller EDR-killer suite, an actively exploited critical Splunk Enterprise flaw (CVE-2026-20253), an unpatchable Apple SecureROM exploit, and Operation Endgame's SocGholish takedown.

**Severity Rationale:** Broad roundup; ransomware-specific content (Gentlemen) duplicates Article 3, but FortiBleed and the Splunk RCE represent significant concurrent infrastructure risk that commonly precedes ransomware deployment.

**Threat Actors:** The Gentlemen, Icarus

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-24858, CVE-2025-59718, CVE-2025-59719, CVE-2026-20253
- **URLs:** _none_

---

### [10] INTERPOL Warns Phishing, Ransomware, and AI Scams Are Rising Across Asia-Pacific

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-06-22 |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com/.../interpol-warns-phishing-ransomware-and](https://thehackernews.com/2026/06/interpol-warns-phishing-ransomware-and.html) |

**Summary:** INTERPOL's 2025/2026 Asia and South Pacific Cyberthreat Assessment reports 135,000+ ransomware-related attacks in the region in 2024 (concentrated in real estate, manufacturing, financial services), alongside surging RaaS adoption, deepfake-driven scams, and 92% YoY DDoS growth.

**Severity Rationale:** Regional strategic intelligence rather than a specific incident — informs threat landscape context but carries no immediate actionable IOC.

**Threat Actors:** _None identified (regional/aggregate reporting)_

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

### [11] Who Runs the Ransomware Group 'The Gentlemen?'

| Field | Value |
|---|---|
| **Source** | Krebs on Security |
| **Published** | 2026-06-10 |
| **Severity** | 🟠 High |
| **URL** | [krebsonsecurity.com/.../who-runs-the-ransomware-group-the-gentlemen](https://krebsonsecurity.com/2026/06/who-runs-the-ransomware-group-the-gentlemen/) |

**Summary:** Krebs, drawing on Check Point, Intel 471, Flashpoint, Constella, and Epieos data, traces The Gentlemen's administrator alias (Hastalamuerte/Zeta88) to Alexander Andreevich Yapaev, a 36-year-old from Izhevsk, Russia, via reused emails, phone numbers, and social media accounts. PRODAFT's follow-up confirms the persona with high confidence and notes the admin supplies affiliates with brute-forced/leaked Fortinet SSL-VPN credentials and uses AI to develop and maintain the ransomware.

**Severity Rationale:** Real-world attribution of a top-tier active RaaS administrator carries high intelligence value for law enforcement and sanctions/targeting purposes, even though it is not a technical IOC disclosure.

**Threat Actors:** The Gentlemen, Hastalamuerte, Zeta88, Alexander Andreevich Yapaev

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |

**IOCs Extracted:**
_No IOCs extracted._

---

### [12] No Joke: Gag Gift Store's Health Plan Pays $450K HIPAA Fine

| Field | Value |
|---|---|
| **Source** | BankInfoSecurity.com RSS Syndication |
| **Published** | 2026-06-19 |
| **Severity** | 🟡 Medium |
| **URL** | [bankinfosecurity.com/.../hipaas-no-joke-gag-gift-firms-health-plan-pays-450k-fine-a-32032](https://www.bankinfosecurity.com/hipaas-no-joke-gag-gift-firms-health-plan-pays-450k-fine-a-32032) |

**Summary:** Spencer's Gifts' employee health plan paid a $450,000 HIPAA settlement over a 2021 Conti ransomware breach affecting 10,023 people, following HHS OCR findings of inadequate security risk analysis — the agency's 20th ransomware-related enforcement action.

**Severity Rationale:** Historical incident (2021, defunct Conti gang); current relevance is regulatory/compliance precedent rather than active threat, but illustrates ongoing downstream legal exposure from ransomware breaches.

**Threat Actors:** Conti (defunct)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [13] Criminal AI-as-a-Service in 2026: How the Underground Market Is Operationalizing Cybercrime

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | 2026-06-11 |
| **Severity** | 🟡 Medium |
| **URL** | [rapid7.com/.../tr-criminal-ai-underground-market-operationalizing-cybercrime-2026](https://www.rapid7.com/blog/post/tr-criminal-ai-underground-market-operationalizing-cybercrime-2026) |

**Summary:** Rapid7 surveys the "Criminal AI-as-a-Service" underground market (FraudGPT, WormGPT, Xanthorox, jailbreak wrappers, stolen API access), finding AI is primarily used to accelerate phishing, social engineering, malware maintenance, and data processing rather than enabling autonomous attacks. Directly relevant to ransomware as one of the workflow stages AI tooling now accelerates.

**Severity Rationale:** Strategic/trend reporting on tooling that supports ransomware operations indirectly (e.g., The Gentlemen's AI-assisted tooling per Article 11) rather than a specific incident or active campaign.

**Threat Actors:** _None identified (market/tooling survey, not actor-specific)_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1588.006](https://attack.mitre.org/techniques/T1588/006/) | Obtain Capabilities: Vulnerabilities | Resource Development |
| [T1566.002](https://attack.mitre.org/techniques/T1566/002/) | Phishing: Spearphishing Link | Initial Access |

**IOCs Extracted:**
_No IOCs extracted._

---

### [14] The June 2026 Security Update Review

| Field | Value |
|---|---|
| **Source** | Zero Day Initiative - Blog |
| **Published** | 2026-06-09 |
| **Severity** | 🟢 Low |
| **URL** | [thezdi.com/.../the-june-2026-security-update-review](https://www.thezdi.com/blog/2026/6/9/the-june-2026-security-update-review) |

**Summary:** ZDI's recap of the largest-ever Patch Tuesday (208 Microsoft CVEs, 123 Adobe CVEs), including a wormable CVSS 9.8 Windows kernel RCE and an actively exploited Microsoft Defender EoP flaw. Ransomware relevance is incidental — the author notes Acrobat Reader patches matter because malicious PDFs are common in ransomware delivery chains.

**Severity Rationale:** General vulnerability disclosure roundup with only tangential ransomware relevance; no specific ransomware campaign, actor, or IOC discussed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-41091, CVE-2026-45657, CVE-2026-47291, CVE-2026-44815, CVE-2026-45585, CVE-2026-50507
- **URLs:** _none_

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2023-3519` | 4, 6 |
| CVE | `CVE-2023-48788` | 4, 6 |
| CVE | `CVE-2023-52271` | 5 |
| CVE | `CVE-2024-57727` | 4, 6 |
| CVE | `CVE-2025-1055` | 5 |
| CVE | `CVE-2025-5777` | 4, 6 |
| CVE | `CVE-2025-59718` | 9 |
| CVE | `CVE-2025-59719` | 9 |
| CVE | `CVE-2025-61155` | 5 |
| CVE | `CVE-2026-20253` | 9 |
| CVE | `CVE-2026-24858` | 9 |
| CVE | `CVE-2026-41091` | 14 |
| CVE | `CVE-2026-44815` | 14 |
| CVE | `CVE-2026-45585` | 14 |
| CVE | `CVE-2026-45657` | 14 |
| CVE | `CVE-2026-47291` | 14 |
| CVE | `CVE-2026-50507` | 14 |
| Domain | `LetsDiskuss[.]com` | 8 |
| File/Driver | `360netmon_wfp.sys` | 3 |
| File/Driver | `ABYSSWORKER` | 5 |
| File/Driver | `DbgView64.exe` (injection target) | 5 |
| File/Driver | `GameDriverX64.sys` | 3, 5 |
| File/Driver | `HWAuidoOs2Ec.sys` | 5 |
| File/Driver | `IMFForceDelete.sys` | 3 |
| File/Driver | `K7RKScan.sys` | 5 |
| File/Driver | `PoisonX.sys` | 3 |
| File/Driver | `ThrottleBlood.sys` | 3 |
| File/Driver | `dmx.sys` | 3 |
| File/Driver | `eb.sys` | 3 |
| File/Driver | `fildds.sys` | 4 |
| File/Driver | `filnk.sys` | 4 |
| File/Driver | `filwfp.sys` | 4 |
| File/Driver | `googleApiUtil64.sys` | 3 |
| File/Driver | `havoc.sys` | 3 |
| File/Driver | `nseckrnl.sys` | 3 |
| File/Driver | `servertool.exe` | 2 |
| File/Driver | `stpm_new.sys` | 3 |
| File/Driver | `stpm_old.sys` | 3 |
| File/Driver | `wsftprm.sys` | 5 |
| File Extension | `.prinzeugen` | 2 |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access | 9, 11 |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | 4, 6 |
| [T1555.003](https://attack.mitre.org/techniques/T1555/003/) | Credentials from Web Browsers | Credential Access | 3, 5 |
| [T1583.001](https://attack.mitre.org/techniques/T1583/001/) | Acquire Infrastructure: Domains | Resource Development | 8 |
| [T1583.006](https://attack.mitre.org/techniques/T1583/006/) | Acquire Infrastructure: Web Services | Resource Development | 8 |
| [T1588.006](https://attack.mitre.org/techniques/T1588/006/) | Obtain Capabilities: Vulnerabilities | Resource Development | 13 |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access | 2, 4, 9, 11 |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 1, 4, 5, 6, 7, 14 |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access | 6, 7 |
| [T1566.002](https://attack.mitre.org/techniques/T1566/002/) | Phishing: Spearphishing Link | Initial Access | 13 |
| [T1204.002](https://attack.mitre.org/techniques/T1204/002/) | User Execution: Malicious File | Execution | 8 |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | Execution | 8 |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement | 2, 4 |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account | Persistence | 1 |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Server Software Component: Web Shell | Persistence | 7 |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | 2 |
| [T1036](https://attack.mitre.org/techniques/T1036/) | Masquerading | Defense Evasion | 3 |
| [T1070](https://attack.mitre.org/techniques/T1070/) | Indicator Removal | Defense Evasion | 2 |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation | 3 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | 1, 3, 4, 5, 6, 9 |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion / Persistence | 1, 5, 8 |
| [T1071](https://attack.mitre.org/techniques/T1071/) | Application Layer Protocol | Command and Control | 5 |
| [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunneling | Command and Control | 1, 5 |
| [T1114.002](https://attack.mitre.org/techniques/T1114/002/) | Email Forwarding Rule | Collection | 7 |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration | 4 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 2, 3, 4, 5, 6, 12 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 14 |
| **Articles Analyzed** | 14 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-06-22 15:07:15 UTC |
