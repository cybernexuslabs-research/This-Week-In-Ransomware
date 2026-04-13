# Threat Intelligence Report: Ransomware

**Generated:** 2026-04-13 11:00:34 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-04-06 → 2026-04-13
**Articles Analyzed:** 8
**Sources:** DataBreaches.Net, BleepingComputer, Rapid7 Cybersecurity Blog, darkreading, The Hacker News, Microsoft Security Blog

---

## Executive Summary

The week of April 6–13, 2026 saw a concentrated ransomware surge with healthcare as the dominant impact sector, reflected across five of the eight articles analyzed. Storm-1175's Medusa campaigns are the most operationally significant threat profiled this period: Microsoft Threat Intelligence documented the group's ability to move from initial exploitation to full ransomware deployment within 24 hours by targeting the critical gap between CVE disclosure and patch adoption — weaponizing N-days within days and zero-days before public disclosure. The near-simultaneous ransomware incidents at Brockton Hospital (Anubis RaaS) and Dutch healthcare IT provider ChipSoft demonstrate that healthcare infrastructure is being targeted by multiple independent threat actor groups, amplifying sector-wide risk. BYOVD is emerging as a cross-group standard for EDR evasion — used by Qilin (kernel-mode driver chain), Warlock (NSec driver), and Storm-1175 (Defender registry tampering) — signaling a mature, shared ecosystem of defense-impairment tooling. Security teams should treat patching of web-facing enterprise software (BeyondTrust, CrushFTP, GoAnywhere MFT, SmarterMail, JetBrains TeamCity, Ivanti) as a 24–48 hour SLA, not a maintenance window.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 5 |
| 🟠 High | 1 |
| 🟡 Medium | 1 |
| 🟢 Low | 1 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2026-1731` | Articles 3, 4, 5 | Critical BeyondTrust RCE flaw actively exploited by Storm-1175; mentioned across all three Storm-1175 coverage articles as the most recently exploited N-day. |
| CVE | `CVE-2025-31161` | Articles 3, 4, 5 | Critical CrushFTP authentication bypass exploited by Storm-1175; appeared in the primary Microsoft report and both secondary coverage pieces. |
| CVE | `CVE-2024-27198` | Articles 3, 4, 5 | JetBrains TeamCity authentication bypass exploited by Storm-1175 days after disclosure in 2024; still appearing as an active initial-access vector. |
| CVE | `CVE-2025-10035` | Articles 3, 4, 5 | GoAnywhere MFT zero-day exploited by Storm-1175 one week before public disclosure, indicating access to exploit broker resources. |
| CVE | `CVE-2026-23760` | Articles 3, 4, 5 | SmarterMail critical authentication bypass exploited as a zero-day by Storm-1175 and also weaponized by China-linked Storm-2603. |

### Shared Threat Actors

#### Storm-1175
- **Seen in:** Articles 3, 4, 5
- **Activity:** Storm-1175 is a financially motivated, China-linked cybercriminal group operating high-tempo Medusa ransomware campaigns. Across all three articles (Microsoft Security Blog as primary source, Dark Reading and The Hacker News as secondary coverage), the group is shown weaponizing 16+ CVEs since 2023, with zero-day exploitation capability emerging in 2025–2026. The group targets healthcare, education, professional services, and finance in Australia, UK, and US, and can complete attacks within 24 hours.

#### Medusa (Ransomware)
- **Seen in:** Articles 3, 4, 5
- **Activity:** Medusa ransomware is the payload consistently attributed to Storm-1175 across all three reporting articles. Deployed after credential theft and security tool tampering, Medusa is the final-stage impact tool in Storm-1175's attack chain, with the group acting as both operator and affiliate distributor.

### Campaign Threads

#### Storm-1175 Medusa High-Velocity Campaign (April 2026)
- **Articles:** 3, 4, 5
- **Description:** Microsoft Threat Intelligence published a comprehensive profile of Storm-1175 on April 6, with Dark Reading and The Hacker News independently reporting on the same findings on April 7. The campaign thread reveals a China-linked RaaS operator exploiting enterprise software vulnerabilities across a 3-year window (2023–2026) with an accelerating zero-day capability, targeting multiple critical sectors globally.
- **Timeline:** 2023 — Initial Exchange/PaperCut exploitation observed. 2024 — Ivanti, ConnectWise, JetBrains, SimpleHelp exploitation. Mid-2025 — CrushFTP exploitation; GoAnywhere MFT zero-day (CVE-2025-10035) exploited pre-disclosure. Early 2026 — SmarterMail zero-day (CVE-2026-23760) and BeyondTrust (CVE-2026-1731) exploitation. April 2026 — Microsoft publishes comprehensive threat profile.

#### Healthcare Ransomware Wave (April 7–11, 2026)
- **Articles:** 1, 2
- **Description:** Within a five-day window, two distinct ransomware attacks hit healthcare infrastructure: Anubis RaaS encrypted systems at Brockton Hospital (Signature Healthcare) on approximately April 7, forcing ambulance diversions and canceling chemotherapy appointments; and an unnamed ransomware group hit ChipSoft, a Dutch EHR vendor, cascading outages to at least five Dutch hospitals and several Belgian facilities. These are independent events from separate threat actors targeting the same high-value sector.
- **Timeline:** ~2026-04-07 — Anubis ransomware hits Brockton Hospital, ambulances diverted. 2026-04-09 — ChipSoft ransomware incident confirmed by Z-CERT; Zorgportaal, HiX Mobile, and Zorgplatform taken offline. 2026-04-10 — Belgian hospital impact reported. 2026-04-11 — Brockton Hospital still on downtime procedures; Anubis attempts media spin.

### Emerging Patterns

- **Healthcare as primary ransomware target:** Healthcare organizations appear in five of eight articles this week — as direct victims (Brockton Hospital, ChipSoft, Belgian hospitals) and as the most-impacted sector in Storm-1175's campaigns. The sector's combination of operational criticality, legacy systems, and time-sensitive patient data creates high ransom leverage.

- **BYOVD as cross-group EDR evasion standard:** Qilin and Warlock use kernel-mode vulnerable drivers (rwdrv.sys/hlpdrv.sys and NSecKrnl.sys respectively) to kill 300+ EDR products; Storm-1175 tampers with Microsoft Defender registry settings to achieve similar outcomes. Three distinct ransomware groups using defense-impairment as a pre-deployment prerequisite suggests this is now a normalized ransomware tradecraft step, not an advanced capability.

- **RMM tool abuse as covert C2/lateral movement infrastructure:** Storm-1175 used 7+ commercial RMM tools (Atera, Level, N-able, MeshAgent, ConnectWise, AnyDesk, SimpleHelp) across campaigns. Warlock used TightVNC and Visual Studio Code tunnels. Encrypting C2 within trusted remote management traffic significantly degrades network-based detection.

- **N-day/zero-day exploitation window weaponization:** Storm-1175 has demonstrated exploitation of CVEs within 1 day of disclosure (CVE-2025-31324 for SAP NetWeaver) and zero-days 1 week before public disclosure. This compresses the organizational patch window to near-zero and demands threat-led patching prioritization based on exploit market signals, not just CVSS scores.

---

## Article Analysis

---

### [1] Brockton Hospital still dealing with aftermath of ransomware attack

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Sat, 11 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [databreaches.net](https://databreaches.net/2026/04/11/brockton-hospital-still-dealing-with-aftermath-of-ransomware-attack/) |

**Summary:** Anubis ransomware, operating as a RaaS, attacked Brockton Hospital (Signature Healthcare) beginning approximately April 7, 2026, encrypting systems and triggering ambulance diversions, chemotherapy cancellation, and the inability to fill new prescriptions. The hospital has been running on paper-based downtime procedures for over a week with two more weeks expected. Anubis attempted to publicly spin the attack as "professional" and non-harmful to patients, a claim directly contradicted by documented patient care disruptions.

**Severity Rationale:** Active ransomware encryption of a live hospital with confirmed patient care impact (ambulance diversions, chemotherapy cancellations, prescription failures) warrants Critical severity.

**Threat Actors:** Anubis

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [2] Healthcare IT solutions provider ChipSoft hit by ransomware attack

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | Thu, 09 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [bleepingcomputer.com](https://www.bleepingcomputer.com/news/security/healthcare-it-solutions-provider-chipsoft-hit-by-ransomware-attack/) |

**Summary:** Dutch healthcare EHR vendor ChipSoft suffered a ransomware attack that forced offline its Zorgportaal, HiX Mobile, and Zorgplatform digital health platforms, cascading outages to at least four Dutch hospitals (Sint Jans Gasthuis, Laurentius, VieCuri, Flevo Hospital) and multiple Belgian facilities. ChipSoft's HiX platform is used by many Dutch hospitals, making this a de facto supply-chain impact event affecting healthcare delivery across two countries. Z-CERT, the Dutch healthcare cybersecurity CERT, is actively supporting remediation.

**Severity Rationale:** Ransomware against a healthcare IT hub serving multiple hospitals across two countries constitutes Critical severity due to the systemic cascading impact on patient-facing systems.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [3] Storm-1175 Deploys Medusa Ransomware at 'High Velocity'

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Tue, 07 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com](https://www.darkreading.com/threat-intelligence/storm-1175-medusa-ransomware-high-velocity) |

**Summary:** Dark Reading reports on Microsoft Threat Intelligence's profile of Storm-1175, a financially motivated cybercrime group conducting high-velocity Medusa ransomware campaigns that exploit N-day and zero-day vulnerabilities in the window between disclosure and widespread patch adoption. The group can move from exploitation to ransomware deployment in as little as 24 hours, with healthcare, education, professional services, and finance sectors in Australia, UK, and US suffering significant recent intrusions. Notable CVEs exploited include CVE-2026-1731 (BeyondTrust), CVE-2025-31161 (CrushFTP), and zero-days CVE-2026-23760 (SmarterMail) and CVE-2025-10035 (GoAnywhere MFT).

**Severity Rationale:** An active ransomware actor with confirmed zero-day capability, sub-24-hour attack chains, and multi-sector impact across three countries warrants Critical severity.

**Threat Actors:** Storm-1175, Medusa

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-1731, CVE-2025-31161, CVE-2024-27198, CVE-2023-21529, CVE-2026-23760, CVE-2025-10035
- **URLs:** _none_

---

### [4] China-Linked Storm-1175 Exploits Zero-Days to Rapidly Deploy Medusa Ransomware

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Tue, 07 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [thehackernews.com](https://thehackernews.com/2026/04/china-linked-storm-1175-exploits-zero.html) |

**Summary:** The Hacker News provides an expanded technical breakdown of Storm-1175's Medusa ransomware campaigns, documenting exploitation of 16+ CVEs across Microsoft Exchange, PaperCut, Ivanti Connect Secure, ConnectWise ScreenConnect, JetBrains TeamCity, SimpleHelp, CrushFTP, GoAnywhere MFT, SmarterMail, and BeyondTrust since 2023. Post-compromise tooling includes LOLBins (PowerShell, PsExec), Impacket, Mimikatz, PDQ Deployer for mass ransomware deployment, and multiple RMM platforms (AnyDesk, Atera, MeshAgent, ConnectWise ScreenConnect, SimpleHelp). Rclone is used for data exfiltration, while Microsoft Defender exclusions are configured to allow Medusa payloads to execute undetected.

**Severity Rationale:** Comprehensive documentation of an active ransomware group with zero-day capability, 16+ exploited CVEs, and confirmed deployments across healthcare, education, finance, and professional services sectors.

**Threat Actors:** Storm-1175, Medusa

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1059](https://attack.mitre.org/techniques/T1059/) | Command and Scripting Interpreter | Execution |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Web Shell | Persistence |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Persistence |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2023-21529, CVE-2023-27350, CVE-2023-27351, CVE-2023-46805, CVE-2024-1708, CVE-2024-1709, CVE-2024-21887, CVE-2024-27198, CVE-2024-27199, CVE-2024-57726, CVE-2024-57727, CVE-2024-57728, CVE-2025-10035, CVE-2025-31161, CVE-2025-52691, CVE-2026-1731, CVE-2026-23760
- **URLs:** _none_

---

### [5] Storm-1175 focuses gaze on vulnerable web-facing assets in high-tempo Medusa ransomware operations

| Field | Value |
|---|---|
| **Source** | Microsoft Security Blog |
| **Published** | Mon, 06 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [microsoft.com](https://www.microsoft.com/en-us/security/blog/2026/04/06/storm-1175-focuses-gaze-on-vulnerable-web-facing-assets-in-high-tempo-medusa-ransomware-operations/) |

**Summary:** Microsoft Threat Intelligence published the primary profile of Storm-1175, documenting the group's systematic exploitation of 16+ web-facing vulnerabilities since 2023 with attack-to-deployment timelines as short as one day. Post-compromise, Storm-1175 deploys web shells or Cloudflare tunnels (renamed as conhost.exe) for persistence, uses PDQ Deployer for network-wide Medusa deployment, and tampers with Windows Defender registry settings to suppress antivirus scanning of the C:\ drive. The group's RMM arsenal spans Atera, Level, N-able DWAgent, MeshAgent, ConnectWise ScreenConnect, AnyDesk, and SimpleHelp — all used as covert C2 channels.

**Severity Rationale:** Primary source intelligence on an active, high-tempo ransomware actor with documented zero-day exploitation capability and confirmed critical-sector impact.

**Threat Actors:** Storm-1175, Medusa

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Web Shell | Persistence |
| [T1136.001](https://attack.mitre.org/techniques/T1136/001/) | Create Local Account | Persistence |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion |
| [T1090.001](https://attack.mitre.org/techniques/T1090/001/) | Internal Proxy (Cloudflare tunnel) | Command and Control |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2023-21529, CVE-2023-27350, CVE-2023-27351, CVE-2023-46805, CVE-2024-1708, CVE-2024-1709, CVE-2024-21887, CVE-2024-27198, CVE-2024-27199, CVE-2024-57726, CVE-2024-57727, CVE-2024-57728, CVE-2025-10035, CVE-2025-31161, CVE-2025-52691, CVE-2026-1731, CVE-2026-23760
- **URLs:** _none_

---

### [6] Qilin and Warlock Ransomware Use Vulnerable Drivers to Disable 300+ EDR Tools

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Mon, 06 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com](https://thehackernews.com/2026/04/qilin-and-warlock-ransomware-use.html) |

**Summary:** Qilin and Warlock ransomware groups are independently deploying BYOVD (Bring Your Own Vulnerable Driver) attacks to disable over 300 EDR solutions before ransomware deployment. Qilin uses DLL side-loading via msimg32.dll to chain two kernel-mode drivers — rwdrv.sys (ThrottleStop.sys renamed) and hlpdrv.sys — that terminate EDR processes while suppressing ETW logging and neutralizing user-mode hooks. Warlock (Water Manaul) exploits unpatched SharePoint servers and uses a vulnerable NSec driver (NSecKrnl.sys, previously googleApiUtil64.sys) for the same EDR-killing purpose, alongside TightVNC, Cloudflare tunnels, and Rclone. Both rwdrv.sys and hlpdrv.sys have been previously observed in Akira and Makop ransomware attacks.

**Severity Rationale:** Sophisticated BYOVD technique capable of silencing virtually all endpoint security products across two active ransomware groups, with shared tooling suggesting an ecosystem-level capability distribution.

**Threat Actors:** Qilin, Warlock (Water Manaul)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion |
| [T1054](https://attack.mitre.org/techniques/T1054/) | Indicator Blocking (ETW suppression) | Defense Evasion |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

> **Note:** Key artifact names (not hash IOCs): `msimg32.dll` (malicious DLL), `rwdrv.sys` (renamed ThrottleStop.sys), `hlpdrv.sys`, `NSecKrnl.sys` (Warlock NSec driver), `googleApiUtil64.sys` (prior Warlock driver).

---

### [7] BKA Identifies REvil Leaders Behind 130 German Ransomware Attacks

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Mon, 06 Apr 2026 |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com](https://thehackernews.com/2026/04/bka-identifies-revil-leaders-behind-130.html) |

**Summary:** Germany's Federal Criminal Police Office (BKA) has identified Daniil Maksimovich Shchukin (31, Russian national, alias UNKN/Oneillk2) as the public-facing representative of REvil/GandCrab, and Anatoly Sergeevitsch Kravchuk (43, Russian-born) as the group's developer. The pair are suspected of conducting 130 ransomware attacks across Germany with collective damages exceeding €35.4 million ($40.8M), 25 of which resulted in ransom payments totaling €1.9 million. REvil, also tracked as Sodinokibi, Water Mare, and Gold Southfield, was active from 2019 until 2021 and counted JBS and Kaseya among its high-profile victims.

**Severity Rationale:** Law enforcement attribution of a now-defunct RaaS operation is valuable for intelligence context but represents historical investigative development rather than an active exploitation threat.

**Threat Actors:** REvil, Sodinokibi, GandCrab

**MITRE ATT&CK Techniques:**

_No techniques mapped — attribution/law enforcement article without behavioral TTPs._

**IOCs Extracted:**

_No IOCs extracted._

---

### [8] What's New in Rapid7 Products and Services: Q1 2026 in Review

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | Thu, 09 Apr 2026 |
| **Severity** | 🟢 Low |
| **URL** | [rapid7.com](https://www.rapid7.com/blog/post/pt-whats-new-rapid7-products-services-q1-2026) |

**Summary:** Rapid7's Q1 2026 product review highlights new security capabilities including MDR for Microsoft (correlating Microsoft, Rapid7, and third-party telemetry), acquisition of Kenzo Security for AI-driven autonomous SOC investigation (94% reduction in investigation time claimed), cloud runtime security via ARMO partnership, and DSPM through a Symmetry Systems partnership. While not a threat intelligence report, the product directions reflect industry defensive responses to the current threat landscape including ransomware and identity-based attacks.

**Severity Rationale:** Informational vendor product announcement with no direct threat content; included due to ransomware keyword match in article body.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2023-21529` | 4, 5 |
| CVE | `CVE-2023-27350` | 4, 5 |
| CVE | `CVE-2023-27351` | 4, 5 |
| CVE | `CVE-2023-46805` | 4, 5 |
| CVE | `CVE-2024-1708` | 4, 5 |
| CVE | `CVE-2024-1709` | 4, 5 |
| CVE | `CVE-2024-21887` | 4, 5 |
| CVE | `CVE-2024-27198` | 3, 4, 5 |
| CVE | `CVE-2024-27199` | 4, 5 |
| CVE | `CVE-2024-57726` | 4, 5 |
| CVE | `CVE-2024-57727` | 4, 5 |
| CVE | `CVE-2024-57728` | 4, 5 |
| CVE | `CVE-2025-10035` | 3, 4, 5 |
| CVE | `CVE-2025-31161` | 3, 4, 5 |
| CVE | `CVE-2025-52691` | 4, 5 |
| CVE | `CVE-2026-1731` | 3, 4, 5 |
| CVE | `CVE-2026-23760` | 3, 4, 5 |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 3, 4, 5 |
| [T1059](https://attack.mitre.org/techniques/T1059/) | Command and Scripting Interpreter | Execution | 4 |
| [T1136.001](https://attack.mitre.org/techniques/T1136/001/) | Create Local Account | Persistence | 5 |
| [T1505.003](https://attack.mitre.org/techniques/T1505/003/) | Web Shell | Persistence | 4, 5 |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Persistence | 4 |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation | 6 |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | 3, 4, 5 |
| [T1054](https://attack.mitre.org/techniques/T1054/) | Indicator Blocking | Defense Evasion | 6 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion | 3, 4, 5, 6 |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | DLL Side-Loading | Defense Evasion | 6 |
| [T1090.001](https://attack.mitre.org/techniques/T1090/001/) | Internal Proxy | Command and Control | 5 |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Desktop Protocol | Lateral Movement | 3, 4, 5, 6 |
| [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Exfiltration | 3, 4, 5, 6 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 1, 2, 3, 4, 5, 6 |
| [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Impact | 2 |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact | 1 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 8 |
| **Articles Analyzed** | 8 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-04-13 11:00:34 UTC |
