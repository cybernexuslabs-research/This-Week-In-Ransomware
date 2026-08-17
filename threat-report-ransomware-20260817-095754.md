# Threat Intelligence Report: ransomware

**Generated:** 2026-08-17 09:57:54 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-08-11 → 2026-08-17
**Articles Analyzed:** 8
**Sources:** DataBreaches.Net, Cybersecurity Blog | SentinelOne, Check Point Research, darkreading, The Hacker News, Zero Day Initiative - Blog

---

## Executive Summary

The dominant story of the week is the joint US/UK/South Korea advisory on **Gunra**, a Conti-derived RaaS operation that has weaponized two Fortinet FortiOS/FortiProxy authentication-bypass flaws (CVE-2024-55591, CVE-2025-24472) for initial access and is now actively bypassing MFA via VDI session hijacking and OTP tampering against critical infrastructure and government targets worldwide. Independent reporting continues to note loose technical overlap between Gunra and North Korean state-sponsored clusters (Lazarus/Andariel), reinforcing a pattern of cybercriminal-nation-state tool sharing. Separately, Microsoft disclosed that the **DeadLock** group is pioneering blockchain-based (Polygon smart contract) proxy rotation for its data-leak and victim-communication infrastructure, a meaningful evolution aimed at resisting takedown efforts. Check Point's Q2 2026 ransomware landscape data shows the ecosystem broadening (93 active groups, up from 71) even as concentration among leaders persists, while a real-world confirmed ransomware attack against Colombia's Ministry of Justice — timed days before a presidential transition — illustrates continued targeting of Latin American government infrastructure. Defenders should prioritize patching the two Fortinet CVEs immediately, treat unexplained MFA/OTP anomalies on VDI portals as a high-fidelity Gunra indicator, and monitor for AnyDesk and blockchain-resolved C2 as emerging DeadLock tradecraft.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 2 |
| 🟠 High | 3 |
| 🟡 Medium | 1 |
| 🟢 Low | 2 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2024-55591` | Articles [1], [2], [3] | Critical FortiOS/FortiProxy auth-bypass flaw used by Gunra for initial "super admin" access; corroborated across all three Gunra-focused sources, confirming it as the group's primary entry vector this period. |
| CVE | `CVE-2025-24472` | Articles [1], [2], [3] | Second Fortinet auth-bypass flaw paired with CVE-2024-55591 in Gunra intrusions; both are in CISA's KEV catalog, indicating organizations still haven't patched despite sustained ransomware targeting. |

### Shared Threat Actors

#### Gunra
- **Seen in:** Articles [1], [2], [3]
- **Activity:** A joint US-UK-South Korea advisory (FBI, CISA, NSA, Secret Service, DC3, KNPA) details Gunra's evolution from a Windows-only Conti derivative (April 2025) into a cross-platform RaaS with a "Golden Community" affiliate rebrand (Jan 2026). Confirmed techniques include exploitation of Fortinet auth-bypass CVEs for initial access, VDI session hijacking via SSL-VPN traffic manipulation, OTP-based MFA bypass, Hiware access-control-server key theft for credential decryption, Impacket-based lateral movement and NTDS credential dumping, and deletion of primary/DR backups before and after encryption. Multiple independent researchers (AhnLab, CloudSEK) note technical and infrastructure overlap with North Korean state-sponsored activity (Lazarus/Andariel payloads Struggle/SIGNBT and Brandoor/COPPERHEDGE), suggesting tool- or infrastructure-sharing rather than common ownership.

### Campaign Threads

#### Joint Gunra Ransomware Advisory Coverage
- **Articles:** [1], [2], [3]
- **Description:** US, UK, and South Korean authorities published a coordinated advisory (dated on or around Aug 10-11, 2026) warning that Gunra is exploiting long-unpatched Fortinet vulnerabilities to breach critical infrastructure and bypass MFA. Dark Reading and The Hacker News both published detailed technical breakdowns on Aug 11; SentinelOne's weekly roundup (Aug 14) folded the same advisory into its "The Bad" section, confirming the story's persistence through the week.
- **Timeline:** Apr 2025 — Gunra first observed (Windows-only). ~Jan 2026 — RaaS affiliate program launched under "Golden Community" branding. Mar 2026 — Breakglass Intelligence discloses a catastrophic crypto flaw in the Linux variant enabling free decryption. Aug 10-11, 2026 — Joint international advisory published; Dark Reading and Hacker News coverage same day. Aug 14, 2026 — SentinelOne weekly digest reiterates the warning.

### Emerging Patterns

- **Blockchain-resilient ransomware infrastructure:** DeadLock's use of Polygon smart contracts to store and rotate proxy server addresses and host its data-leak blog (via the Wasabi protocol) removes the need for registered, seizable domains — a takedown-resistance technique that TI teams should expect other RaaS operators to copy. (Article [5])
- **Nation-state / ransomware technique overlap continues:** For the second consecutive advisory cycle, a financially-motivated RaaS group (Gunra) shows infrastructure and TTP overlap with DPRK-linked clusters (Lazarus/Andariel), per AhnLab and CISA. This blurs attribution and complicates sanctions-driven defensive prioritization. (Articles [1], [2])
- **Ecosystem fragmentation despite continued top-heavy concentration:** Check Point's Q2 2026 data shows active RaaS groups rising from 71 to 93 quarter-over-quarter even as the top 10 groups' combined victim share fell from 71% to 57.6% — the barrier to launching a new RaaS brand keeps dropping. (Article [6])
- **Government/critical-infrastructure targeting in Latin America persists:** The confirmed ransomware attack on Colombia's Ministry of Justice, coming days before a presidential transition and following a separate breach at Ecopetrol and an alleged compromise of the national tax authority, continues a documented year-long escalation of attacks on Colombian public-sector and state-linked targets. (Article [4])

---

## Article Analysis

---

### [1] Gunra Ransomware Gang Exploits Fortinet Flaws, Bypasses MFA

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Tue, 11 Aug 2026 21:16:25 GMT |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com/.../gunra-ransomware-gang-fortinet-flaws-bypasses-mfa](https://www.darkreading.com/cyberattacks-data-breaches/gunra-ransomware-gang-fortinet-flaws-bypasses-mfa) |

**Summary:** A joint US/South Korean government advisory details Gunra ransomware's exploitation of two Fortinet FortiOS/FortiProxy authentication-bypass vulnerabilities for initial access against critical infrastructure and government organizations globally. The group has also been observed hijacking VDI authentication sessions and tampering with OTP validation logic to fully bypass multi-factor authentication, then deploying double-extortion ransomware after deleting primary and disaster-recovery backups.

**Severity Rationale:** Active, government-confirmed exploitation of known vulnerabilities against critical infrastructure, combined with a working MFA-bypass technique, represents the highest tier of real-world impact.

**Threat Actors:** Gunra

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1556](https://attack.mitre.org/techniques/T1556/) | Modify Authentication Process | Credential Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Clear Windows Event Logs | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2024-55591, CVE-2025-24472
- **URLs:** _none_

---

### [2] Gunra Ransomware Exploits Fortinet FortiOS, FortiProxy Flaws to Breach Networks

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Tue, 11 Aug 2026 14:46:24 +0530 |
| **Severity** | 🔴 Critical |
| **URL** | [thehackernews.com/.../gunra-ransomware-exploits-fortinet-and.html](https://thehackernews.com/2026/08/gunra-ransomware-exploits-fortinet-and.html) |

**Summary:** Expanded technical coverage of the same joint advisory confirms Gunra has claimed 51 victims (concentrated in South Korea, Brazil, Spain, Thailand, Hong Kong) since April 2025, using Impacket tools for lateral movement and NTDS credential dumping, exfiltrating data to OneDrive/SharePoint and MEGA, and compromising a Hiware access-control server to steal a symmetric key and decrypt stored enterprise credentials. Researchers again flag overlap between Gunra intrusions and North Korean state-sponsored campaigns using Lazarus-linked payloads (Struggle/SIGNBT, Brandoor/COPPERHEDGE).

**Severity Rationale:** Confirms active exploitation of the same critical Fortinet flaws plus additional credential-theft and MFA-bypass tradecraft against critical infrastructure, with corroborated nation-state tooling overlap.

**Threat Actors:** Gunra, Golden Community, Lazarus Group, Andariel

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1102](https://attack.mitre.org/techniques/T1102/) | Web Service | Command and Control |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1556](https://attack.mitre.org/techniques/T1556/) | Modify Authentication Process | Credential Access |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Clear Windows Event Logs | Defense Evasion |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Defense Evasion |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2024-55591, CVE-2025-24472
- **URLs:** _none_

---

### [3] The Good, the Bad and the Ugly in Cybersecurity – Week 33

| Field | Value |
|---|---|
| **Source** | Cybersecurity Blog \| SentinelOne |
| **Published** | Fri, 14 Aug 2026 15:21:37 +0000 |
| **Severity** | 🟠 High |
| **URL** | [sentinelone.com/.../week-33-8](https://www.sentinelone.com/blog/the-good-the-bad-and-the-ugly-in-cybersecurity-week-33-8/) |

**Summary:** SentinelOne's weekly roundup covers the Gunra ransomware advisory as its "Bad" story of the week, reiterating exploitation of the two Fortinet CVEs and Conti-derived tradecraft, and reports a "catastrophic cryptographic flaw" in Gunra's Linux ransomware variant that allows victims to fully recover encrypted files without paying. The roundup also covers an unrelated Defender zero-day ("ShieldBreak") and a UK sextortion prosecution against a member of "The Com," a loosely organized cybercrime collective that among its subgroups runs corporate ransomware operations.

**Severity Rationale:** Restates active, government-flagged Gunra exploitation but adds no new incident data beyond the primary advisory articles; rated High rather than Critical since it is a secondary digest rather than an original disclosure.

**Threat Actors:** Gunra

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2024-55591, CVE-2025-24472
- **URLs:** _none_

---

### [4] Ransomware Hits Colombian Justice Ministry Days Before Presidential Transition

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Wed, 12 Aug 2026 14:00:00 GMT |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/.../ransomware-hits-colombian-justice-ministry-presidential-transition](https://www.darkreading.com/cyberattacks-data-breaches/ransomware-hits-colombian-justice-ministry-presidential-transition) |

**Summary:** A ransomware attack struck Colombia's Ministry of Justice on Aug 2, 2026, encrypting files and degrading drug-monitoring and legal-process services just five days before a presidential handover; officials stated no data was confirmed stolen. The incident follows a documented pattern of escalating attacks on Colombian government and state-linked organizations, including a March compromise of the national tax authority and a July breach at oil company Ecopetrol affecting over a dozen subsidiaries.

**Severity Rationale:** Confirmed ransomware deployment against a national government ministry disrupting public services during a politically sensitive transition, though no specific threat actor or novel technique was disclosed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:** _No IOCs extracted._

---

### [5] DeadLock Ransomware Uses Polygon Smart Contracts to Make Extortion Infra Harder to Disrupt

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Tue, 11 Aug 2026 22:05:27 +0530 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/.../deadlock-ransomware-uses-polygon-smart.html](https://thehackernews.com/2026/08/deadlock-ransomware-uses-polygon-smart.html) |

**Summary:** Microsoft Threat Intelligence details how DeadLock ransomware, active since July 2025 with 96 claimed victims (mostly Italy, Spain, Poland, Türkiye, US), uses the Session messaging network and Polygon blockchain smart contracts to deliver and rotate proxy addresses for its victim-communication and data-leak infrastructure, avoiding reliance on seizable domains. The malware uses Curve25519/XChaCha20 encryption, geofences CIS and select Middle Eastern countries, throttles itself to avoid detection, and relies on AnyDesk for remote access while deleting Volume Shadow Copies and self-erasing post-encryption.

**Severity Rationale:** Represents an active, technically sophisticated double-extortion campaign with a genuinely novel takedown-resistant C2 architecture, though victim count and observed scope are smaller than the Gunra advisory.

**Threat Actors:** DeadLock

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1102](https://attack.mitre.org/techniques/T1102/) | Web Service | Command and Control |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Clear Windows Event Logs | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:**
- **IPs:** 138.226.236[.]51
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** hxxp://138.226.236[.]51/prrq.php

_Additional artifacts (not standard IOC types): wallet addresses `0x8EF7c3e531d871D3B9D559722DE77EB1dEc19dAe` (stores proxy server URL) and `0x757984507c82c8dA1d3969c535dB5706eEE6426C` (stores data-leak blog posts) on the Polygon blockchain._

---

### [6] The State of Ransomware Q2 2026

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | Thu, 13 Aug 2026 12:54:35 +0000 |
| **Severity** | 🟡 Medium |
| **URL** | [research.checkpoint.com/2026/the-state-of-ransomware-q2-2026](https://research.checkpoint.com/2026/the-state-of-ransomware-q2-2026/) |

**Summary:** Check Point's Q2 2026 landscape report finds the number of active RaaS groups climbed to 93 (from 71) even as the top 10 groups' victim share fell to 57.6%; data-leak sites recorded 2,139 victims (flat QoQ, +33% YoY). Qilin (279 victims, -17%) and The Gentlemen (269 victims, +62%) fought for the top spot, with a leak of The Gentlemen's internal chat logs confirming the group used AI coding assistants to build its ransomware management panel in roughly three days.

**Severity Rationale:** A strategic threat-landscape report without a specific active-exploitation incident; valuable for trend-tracking but not an immediate defensive action item.

**Threat Actors:** Qilin, The Gentlemen, Krybit

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._

---

### [7] CISA Unveils New Cybersecurity Resources for K-12 Schools and Districts

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Sat, 15 Aug 2026 11:20:49 +0000 |
| **Severity** | 🟢 Low |
| **URL** | [databreaches.net/2026/08/15/cisa-unveils-new-cybersecurity-resources-for-k-12-schools-and-districts](https://databreaches.net/2026/08/15/cisa-unveils-new-cybersecurity-resources-for-k-12-schools-and-districts/) |

**Summary:** CISA released a K-12 Cybersecurity Foundations Resource Package — guides, videos, and reference materials covering credential protection, backup testing, and incident response — in response to sustained ransomware and cyber targeting of the education sector. The article notes conflicting reports on whether K-12 ransomware attacks are trending up or down through H1 2026, but frames schools as persistently attractive, low-resourced targets.

**Severity Rationale:** Purely a policy/awareness resource release with no incident, vulnerability, or active threat data.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._

---

### [8] The August 2026 Security Update Review

| Field | Value |
|---|---|
| **Source** | Zero Day Initiative - Blog |
| **Published** | Tue, 11 Aug 2026 17:56:34 +0000 |
| **Severity** | 🟢 Low |
| **URL** | [thezdi.com/blog/2026/8/11/the-august-2026-security-update-review](https://www.thezdi.com/blog/2026/8/11/the-august-2026-security-update-review) |

**Summary:** ZDI's monthly Patch Tuesday roundup covers Adobe and Microsoft's August 2026 releases (51 and 398 CVEs respectively), highlighting one actively-exploited Windows privilege-escalation flaw (CVE-2026-68820) that the authors note is the type of bug "often paired with code execution bugs to take over a system, often through phishing or ransomware." No ransomware campaign, group, or victim is otherwise discussed.

**Severity Rationale:** Only tangentially references ransomware as a generic risk category rather than reporting any ransomware-specific activity; informational patch guidance.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._ _(Dozens of general Patch Tuesday CVEs were disclosed in this article but are not ransomware-specific and were excluded as noise; see the source for the full CVE list.)_

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2024-55591` | [1], [2], [3] |
| CVE | `CVE-2025-24472` | [1], [2], [3] |
| IP | `138.226.236[.]51` | [5] |
| URL | `hxxp://138.226.236[.]51/prrq.php` | [5] |
| Wallet (Polygon) | `0x8EF7c3e531d871D3B9D559722DE77EB1dEc19dAe` | [5] |
| Wallet (Polygon) | `0x757984507c82c8dA1d3969c535dB5706eEE6426C` | [5] |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1102](https://attack.mitre.org/techniques/T1102/) | Web Service | Command and Control | [2], [5] |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control | [5] |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | [1], [2], [3] |
| [T1556](https://attack.mitre.org/techniques/T1556/) | Modify Authentication Process | Credential Access | [1], [2] |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Clear Windows Event Logs | Defense Evasion | [1], [2], [5] |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Defense Evasion | [2] |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration | [2] |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | [1], [2], [3], [4], [5] |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact | [1], [2], [3], [5] |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | [1], [2], [3] |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement | [2] |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 (3 failed: BleepingComputer 403, Mandiant XML parse error, BankInfoSecurity 403) |
| **Articles Retrieved** | 8 |
| **Articles Analyzed** | 8 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-08-17 09:57:54 UTC |
