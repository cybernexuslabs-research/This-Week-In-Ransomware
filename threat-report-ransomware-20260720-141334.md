# Threat Intelligence Report: ransomware

**Generated:** 2026-07-20 14:13:34 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-07-14 → 2026-07-20
**Articles Analyzed:** 8
**Sources:** darkreading, The Hacker News, SecurityWeek, Cybersecurity Dive - Latest News, Zero Day Initiative - Blog, Malwarebytes

---

## Executive Summary

The week of July 14–20, 2026 shows ransomware operators continuing to exploit two very different fronts simultaneously: fast-moving edge-device zero-days and long-standing identity weaknesses. Inc Ransomware chained a maximum-severity SonicWall SMA SSRF flaw (CVE-2026-15409, CVSS 10.0) with a second injection bug to reach root access and domain controllers within days of disclosure, while Sophos's State of Ransomware 2026 survey confirms that phishing and credential compromise — not exploits — are now the dominant root cause industry-wide, with MFA present but failing in 97% of credential-based intrusions. Real-world operational impact was significant this week: Coca-Cola's Fairlife dairy unit halted U.S. production, Japan's largest taxi operator went offline amid suspected AiLock activity, and a newly identified Rust-based ransomware family, Spirals, fully encrypted an Asian IT services firm's network within 24 hours of initial access. A parallel and less technical but equally consequential story emerged from the DigitalMint sentencing: insiders within the ransomware incident-response and negotiation industry itself colluded with BlackCat/ALPHV to inflate victim payouts by over $75 million, underscoring that the ransomware ecosystem's trusted intermediaries are now also a targetable attack surface. Recommended focus areas: prioritize the SonicWall SMA hotfix plus forensic re-verification of any exposed appliance, treat AD FS and SharePoint patches from this month's record Microsoft release as ransomware-relevant given historical pairing with RCE, and reassess vetting/monitoring controls for third-party incident-response and negotiation vendors.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 2 |
| 🟠 High | 2 |
| 🟡 Medium | 3 |
| 🟢 Low | 1 |

---

## Cross-Article Connections

### Shared IOCs
_No shared IOCs identified across articles._

### Shared Threat Actors
_No single threat actor was named across multiple articles this week; see Campaign Threads below for the one connected campaign (Spirals) that appears in two separate write-ups._

### Campaign Threads

#### Spirals Ransomware Debut Campaign
- **Articles:** 3, 4
- **Description:** A previously undocumented, Rust-based ransomware family called Spirals struck an IT services company in South Asia in June 2026. The attacker compromised an internet-facing IIS web server, uploaded an ASP.NET web shell, dumped the SAM credential hive, disabled endpoint security, and used PsExec to push the payload network-wide — encrypting the entire environment in under 24 hours. A Tor negotiation portal and a six-day data-leak threat were used to pressure the victim.
- **Timeline:** SecurityWeek's July 17 roundup first flagged the incident briefly ("Sophisticated Spirals ransomware targets IT firm"); The Hacker News's July 16 ThreatsDay column (drawing on Broadcom/Symantec and Carbon Black research) provided the full technical breakdown of the same June 2026 intrusion.

### Emerging Patterns

- **Edge-device zero-days remain a fast, high-yield ransomware vector even as identity attacks dominate root-cause statistics:** Inc Ransomware's chained exploitation of two SonicWall SMA zero-days to reach domain controllers (Article 1) shows exploit-based intrusion is still highly effective when a critical flaw surfaces — even though Sophos's industry-wide survey (Article 5) finds phishing and credential compromise have overtaken exploits (18%, down from 32%) as the leading ransomware root cause. Both realities require active defense simultaneously: rapid patch/forensic response for edge appliances, and identity threat detection for the broader majority of intrusions.
- **Ransomware's operational blast radius keeps widening across manufacturing, food & beverage, and transportation:** Coca-Cola's Fairlife dairy unit halting U.S. production (Article 2), Japan's largest taxi operator Nihon Kotsu taking systems offline amid suspected AiLock activity (Article 3), and a German textile manufacturer's bankruptcy following a six-week ransomware-driven shutdown (also Article 3) all illustrate that ransomware continues to translate directly into physical-world business disruption, not just data loss.
- **The ransomware response/negotiation ecosystem is itself becoming a target of corruption and insider abuse:** The DigitalMint case (Article 7) shows a licensed incident-response negotiator and two co-conspirators secretly fed victim intelligence to BlackCat/ALPHV and even ran ransomware deployments as gang affiliates, netting over $75 million from five victims. This is a structural insider-threat vector distinct from technical intrusion and argues for tighter vetting of third-party IR/negotiation vendors.

---

## Article Analysis

---

### [1] Inc Ransomware Exploits SonicWall SMA Zero-Days

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Fri, 17 Jul 2026 20:01:13 GMT |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com/.../inc-ransomware-exploits-sonicwall-sma-zero-days](https://www.darkreading.com/vulnerabilities-threats/inc-ransomware-exploits-sonicwall-sma-zero-days) |

**Summary:** Two chained vulnerabilities in SonicWall's SMA 1000 Series appliances — an unauthenticated, CVSS 10.0 SSRF flaw (CVE-2026-15409) and a CVSS 7.2 authenticated code-injection flaw (CVE-2026-15410) — have been exploited as zero-days by a threat actor tied to the Inc ransomware-as-a-service group. Rapid7 telemetry shows attackers using the appliances for initial access, credential and OTP-seed theft, lateral movement to domain controllers, and at least one confirmed case of full ransomware deployment; CISA added both CVEs to its KEV catalog on July 14.

**Severity Rationale:** Two chained zero-day vulnerabilities (one with a maximum CVSS 10.0) are being actively exploited in the wild by an established ransomware-as-a-service group, with at least one confirmed case of full ransomware deployment despite patching becoming available.

**Threat Actors:** Inc Ransomware (Inc Ransom)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1111](https://attack.mitre.org/techniques/T1111/) | Multi-Factor Authentication Interception | Credential Access |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-15409, CVE-2026-15410
- **URLs:** _none_

---

### [2] Ransomware attack forces Coca-Cola to suspend US production at dairy unit

| Field | Value |
|---|---|
| **Source** | Cybersecurity Dive - Latest News |
| **Published** | Fri, 17 Jul 2026 10:35:34 -0400 |
| **Severity** | 🔴 Critical |
| **URL** | [cybersecuritydive.com/.../ransomware-attack-coca-cola-suspend-production-dairy](https://www.cybersecuritydive.com/news/ransomware-attack-coca-cola-suspend-production-dairy/825540/) |

**Summary:** Coca-Cola disclosed a ransomware attack against its Fairlife dairy business that forced a suspension of all U.S. production facilities, while Canadian operations remained unaffected. The company has not attributed the attack to a specific group and is working with law enforcement and outside cybersecurity advisers; the food and agriculture sector has now logged roughly 205 attacks in 2026 (4.9% of all attacks tracked).

**Severity Rationale:** A ransomware attack forced Coca-Cola to halt all U.S. production at its billion-dollar Fairlife dairy business, representing significant real-world operational and financial impact even though attribution remains unconfirmed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [3] In Other News: Iran Tracks US Military Phones, CrashStealer macOS Malware, CVD Blueprint

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Fri, 17 Jul 2026 14:27:54 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/.../in-other-news-iran-tracks-us-military-phones-crashstealer-macos-malware-cvd-blueprint](https://www.securityweek.com/in-other-news-iran-tracks-us-military-phones-crashstealer-macos-malware-cvd-blueprint/) |

**Summary:** Weekly roundup covering several ransomware-relevant incidents: Japan's largest taxi operator, Nihon Kotsu, took its dispatch and IT systems offline following a suspected attack by the AiLock ransomware group; a newly discovered ransomware variant, Spirals, hit an Asian IT services firm; and the extortion group "The Gentlemen" posted naval defense manufacturer Thyssenkrupp Marine Systems (TKMS) and subsidiary Atlas Elektronik to its leak site, claiming over 1TB stolen (TKMS says the affected environment was segmented and held no classified data). Also notable: a German textile manufacturer filed for bankruptcy after a six-week cyberattack-driven shutdown.

**Severity Rationale:** Multiple ransomware and extortion incidents in a single roundup — including a Japanese transportation giant taken offline, a new ransomware group hitting an Asian IT firm, and a defense contractor subsidiary listed on a leak site — reflect active, ongoing campaigns against operationally significant targets, though no single incident here individually reaches confirmed critical-scale impact within this article.

**Threat Actors:** AiLock, Spirals, The Gentlemen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [4] ThreatsDay: Game Cheat Spyware, 24-Hour Ransomware, Chrome Sync Stalking + 12 More Stories

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Thu, 16 Jul 2026 21:11:15 +0530 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/2026/07/threatsday-game-cheat-spyware-24-hour.html](https://thehackernews.com/2026/07/threatsday-game-cheat-spyware-24-hour.html) |

**Summary:** Weekly digest whose lead ransomware item details Spirals, a new Rust-based ransomware family that fully encrypted an Asian IT services company's network within 24 hours of initial access. The attacker used an ASP.NET web shell on a compromised IIS server, dumped the SAM credential hive, disabled endpoint protection, and deployed the payload via PsExec, then threatened to leak stolen data via a Tor portal within six days. The digest also covers CISA's KEV additions for Oracle E-Business Suite and the KNX protocol.

**Severity Rationale:** A new, previously undocumented ransomware family fully encrypted a victim network within 24 hours of initial access, demonstrating a fast, effective attack chain against enterprise IT infrastructure, though confined to a single known victim so far.

**Threat Actors:** Spirals

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Web Shell | Persistence |
| [T1003.002](https://attack.mitre.org/techniques/T1003/002/) | OS Credential Dumping: Security Account Manager | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-46817, CVE-2023-4346
- **URLs:** _none_

---

### [5] Identity Attacks Overtake Exploits as Top Ransomware Cause

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Wed, 15 Jul 2026 20:16:13 GMT |
| **Severity** | 🟡 Medium |
| **URL** | [darkreading.com/.../identity-attacks-overtake-exploits-top-ransomware-cause](https://www.darkreading.com/identity-access-management-security/identity-attacks-overtake-exploits-top-ransomware-cause) |

**Summary:** Sophos's State of Ransomware 2026 survey of 2,158 IT/security leaders across 17 countries finds malicious email (26%) and phishing (24%) have overtaken vulnerability exploitation (18%, down from 32%) as the top ransomware root cause, with compromised credentials involved in 23% of cases. MFA was deployed in 97% of credential-based-attack victims yet still failed to prevent compromise; 56% of attacks achieved encryption overall.

**Severity Rationale:** A large-scale industry survey rather than a specific incident, but it provides critical structural intelligence — identity-based attacks now account for over half of ransomware root causes even where MFA was deployed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [6] The July 2026 Security Update Review

| Field | Value |
|---|---|
| **Source** | Zero Day Initiative - Blog |
| **Published** | Tue, 14 Jul 2026 17:56:54 +0000 |
| **Severity** | 🟡 Medium |
| **URL** | [thezdi.com/blog/2026/7/14/the-july-2026-security-update-review](https://www.thezdi.com/blog/2026/7/14/the-july-2026-security-update-review) |

**Summary:** ZDI's review of a record-breaking Microsoft Patch Tuesday (621 CVEs) highlights two actively exploited zero-days — an Active Directory Federation Services elevation-of-privilege bug (CVE-2026-56155) explicitly noted as the kind of flaw "often paired with an RCE as we see in ransomware," and a SharePoint elevation-of-privilege bug (CVE-2026-56164). Also flagged: a maximum-severity Hyper-V VMSwitch EoP (CVE-2026-57092), unauthenticated SharePoint RCE pair demonstrated at Pwn2Own Berlin (CVE-2026-50522/58644), and critical RDP, DHCP, and Exchange OWA bugs.

**Severity Rationale:** A record-breaking Microsoft patch release with two actively exploited zero-days and several critical, ransomware-relevant RCE bugs (AD FS, SharePoint), but this is a proactive vulnerability advisory rather than a confirmed ransomware incident.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-56155, CVE-2026-56164, CVE-2026-57092, CVE-2026-50522, CVE-2026-58644, CVE-2026-56190, CVE-2026-55008, CVE-2026-50518, CVE-2026-56188
- **URLs:** _none_

---

### [7] The inside job that cost ransomware victims millions

| Field | Value |
|---|---|
| **Source** | Malwarebytes |
| **Published** | Tue, 14 Jul 2026 09:26:51 GMT |
| **Severity** | 🟡 Medium |
| **URL** | [malwarebytes.com/blog/news/2026/07/the-inside-job-that-cost-ransomware-victims-millions](https://www.malwarebytes.com/blog/news/2026/07/the-inside-job-that-cost-ransomware-victims-millions) |

**Summary:** Angelo Martino, a ransomware negotiator at incident-response firm DigitalMint, was sentenced to 70 months in prison for secretly feeding client cyber-insurance limits and negotiation strategy to the BlackCat/ALPHV gang between April and September 2023, inflating ransom payments across five victims to over $75 million. Martino and two co-conspirators (a fellow negotiator and a Sygnia IR manager) also became BlackCat affiliates themselves, personally deploying ransomware against additional victims including a medical device company.

**Severity Rationale:** A significant $75M+ ransomware-adjacent fraud scheme is now resolved via sentencing; it reveals a structural insider-risk vector in the ransomware response industry but describes historical (2023) activity rather than an active ongoing threat.

**Threat Actors:** BlackCat, ALPHV

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

### [8] Armenia Detains Russian Tourist on U.S. Warrant for REvil Hacker, Lawyers Say Wrong Man

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Fri, 17 Jul 2026 16:23:31 +0530 |
| **Severity** | 🟢 Low |
| **URL** | [thehackernews.com/2026/07/armenia-detains-russian-tourist-on-us.html](https://thehackernews.com/2026/07/armenia-detains-russian-tourist-on-us.html) |

**Summary:** Armenia has detained a Russian tourist, Aleksandr Yuryevich Ermakov, on a U.S. extradition warrant intended for a different person, Aleksandr Gennadievich Ermakov — sanctioned for the 2022 Medibank breach and linked to REvil/Sodinokibi and the SugarLocker ransomware operation. Defense lawyers argue the U.S. warrant lacked distinguishing identity data (patronymic, fingerprints), leading Armenian border officers to detain the wrong man based on a name match alone.

**Severity Rationale:** Purely a law enforcement identification/legal dispute story with no new technical threat information; informational value only.

**Threat Actors:** REvil, Sodinokibi, SugarLocker

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2023-4346` | 4 |
| CVE | `CVE-2026-15409` | 1 |
| CVE | `CVE-2026-15410` | 1 |
| CVE | `CVE-2026-46817` | 4 |
| CVE | `CVE-2026-50518` | 6 |
| CVE | `CVE-2026-50522` | 6 |
| CVE | `CVE-2026-55008` | 6 |
| CVE | `CVE-2026-56155` | 6 |
| CVE | `CVE-2026-56164` | 6 |
| CVE | `CVE-2026-56188` | 6 |
| CVE | `CVE-2026-56190` | 6 |
| CVE | `CVE-2026-57092` | 6 |
| CVE | `CVE-2026-58644` | 6 |

_No IP, domain, hash, or URL IOCs were extracted from this article set._

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access | 5 |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 1, 4, 6 |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access | 5 |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Web Shell | Persistence | 4 |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation | 6 |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | 1 |
| [T1003.002](https://attack.mitre.org/techniques/T1003/002/) | OS Credential Dumping: Security Account Manager | Credential Access | 4 |
| [T1111](https://attack.mitre.org/techniques/T1111/) | Multi-Factor Authentication Interception | Credential Access | 1 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | 4 |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement | 1 |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement | 4 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 1, 2, 3, 4, 5 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 (1 parse warning: Mandiant; 1 blocked: BleepingComputer 403) |
| **Articles Retrieved** | 8 |
| **Articles Analyzed** | 8 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-07-20 14:13:34 UTC |
