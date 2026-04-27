# Threat Intelligence Report: Ransomware

**Generated:** 2026-04-27 07:29:33 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-04-21 → 2026-04-27
**Articles Analyzed:** 11
**Sources:** DataBreaches.Net, BleepingComputer, Dark Reading, The Hacker News, Rapid7 Cybersecurity Blog, BankInfoSecurity.com

---

## Executive Summary

The week of April 21–27, 2026 saw ransomware activity concentrated around three major threads: the explosive rise of The Gentlemen RaaS, active exploitation of a critical Bomgar/BeyondTrust RCE vulnerability, and the resurgence of Trigona with purpose-built evasion tooling. The Gentlemen — a mid-2025 entrant paying affiliates 90% of ransom proceeds — has claimed over 320 public victims and its SystemBC C2 infrastructure exposes a botnet of 1,570+ compromised corporate networks not yet in public reporting, making the true operational scale significantly larger than disclosed. CVE-2026-1731 in Bomgar Remote Support is under active exploitation with LockBit ransomware confirmed deployed against MSP supply chains, with one incident cascading to 78 downstream businesses. Trigona re-emerged after a 2023 disruption with a custom `uploader_client.exe` exfiltration tool and a multi-stage BYOVD EDR-killing playbook, signalling the group has rebuilt with improved operational security. On the legal front, the final of three cybersecurity professionals who colluded with BlackCat/ALPHV pled guilty, closing the case and reinforcing the need for structural separation of negotiation, payment, and forensic roles. Healthcare continues to bear disproportionate regulatory pressure, with HHS OCR levying $1.7M in HIPAA fines against four entities that failed to conduct adequate risk analyses before ransomware breaches.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 4 |
| 🟠 High | 2 |
| 🟡 Medium | 3 |
| 🟢 Low | 2 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2026-1731` | Article 0 | Critical Bomgar RCE under active exploitation for LockBit ransomware deployment; actively targeted in MSP environments with confirmed supply-chain impact |
| IP | `45.86.230[.]112` | Article 2 | SystemBC C2 server linked to The Gentlemen affiliate operation; single-source confirmation — corroborating DFIR reporting falls outside this date window |
| IP | `91.107.247[.]163` | Article 2 | Cobalt Strike C2 used in The Gentlemen lateral movement; same caveat as above |

### Shared Threat Actors

#### The Gentlemen
- **Seen in:** Articles 2, 3
- **Activity:** Two independent research publications (The Hacker News and Dark Reading) confirm The Gentlemen as the fastest-scaling RaaS in 2026, with 192 Q1 incidents and a botnet of 1,570+ unreported corporate victims visible from their SystemBC C2. The group pays affiliates 90%, provides multi-OS lockers and EDR killers, and uses GPO-based domain-wide ransomware detonation.

#### BlackCat / ALPHV
- **Seen in:** Articles 6, 7
- **Activity:** Dual coverage confirms Angelo Martino's guilty plea, closing the three-person insider collusion case. All defendants (Martino, Goldberg, Martin) have now pled guilty. Martino sentenced July 9, 2026; others sentenced April 30, 2026. DOJ seized $10M in assets from Martino alone.

#### Trigona
- **Seen in:** Articles 4, 5
- **Activity:** Symantec's report, covered by both BleepingComputer and DataBreaches.Net, confirms Trigona's March 2026 resurgence with a custom exfiltration tool and BYOVD EDR-disruption toolkit. The group had been dormant since a 2023 disruption by Ukrainian cyber activists who stole their source code and database.

### Campaign Threads

#### The Gentlemen RaaS Expansion
- **Articles:** 2, 3
- **Description:** The Hacker News and Dark Reading provide complementary coverage of The Gentlemen's scale and attack methodology. Together they establish a 1,570+ victim botnet, 90% affiliate payout model, Go-based multi-OS lockers with a separate ESXi C variant, and Group Policy-based mass deployment. The ESXi variant evades most AV engines on VirusTotal.
- **Timeline:** July 2025: group emerges → September 2025: Trend Micro first analysis → Q4 2025: victim count accelerates → Q1 2026: 192 incidents, ranks third globally behind Qilin and Akira → April 21–22, 2026: dual publication confirms 1,570+ hidden victims.

#### BlackCat Insider Threat Prosecution
- **Articles:** 6, 7
- **Description:** Dark Reading and The Hacker News cover the same DOJ announcement confirming the final guilty plea in a case where three cybersecurity incident-response professionals systematically fed victim insurance limits and negotiation positions to BlackCat between April–November 2023, enabling inflated ransoms. One victim paid $1.2M in Bitcoin; the proceeds were split and laundered.
- **Timeline:** April 2023: collusion begins → November 2023: final BlackCat deployment → December 2025: Goldberg and Martin plead guilty → April 21, 2026: Martino pleads guilty → July 9, 2026: Martino sentencing.

#### Trigona Resurgence with Custom Tooling
- **Articles:** 4, 5
- **Description:** BleepingComputer and DataBreaches.Net both report on Symantec's findings documenting Trigona's return in March 2026 with purpose-built tooling. The custom `uploader_client.exe` avoids flagging of public utilities like Rclone and MegaSync, and multiple BYOVD tools are chained to systematically disable endpoint protection before encryption.
- **Timeline:** October 2022: Trigona launches → October 2023: Ukrainian activists hack Trigona servers, steal source code → March 2026: Trigona resurfaces with custom tooling → April 23, 2026: Symantec/BleepingComputer publish IOCs.

### Emerging Patterns

- **Cross-platform ESXi + Windows ransomware as standard practice:** Both The Gentlemen (articles 2, 3) and Kyber (article 1) deploy separate ESXi and Windows encryptors within the same operation. Targeting VMware ESXi alongside Windows is now a baseline capability for mature RaaS operations, maximising disruption potential in virtualised enterprise environments.

- **BYOVD / EDR killer tooling as affiliate-tier standard:** Trigona affiliates (articles 4, 5) deployed six distinct BYOVD tools to kill endpoint protection. The Gentlemen (articles 2, 3) provides affiliates with EDR-killing capability as part of its RaaS package. This is no longer an advanced-group differentiator — it is a commodity offered at the affiliate level.

- **RMM platforms as ransomware deployment highways:** CVE-2026-1731 in Bomgar (article 0) is being exploited to reach MSP downstream customers at scale. The Gentlemen independently leverage AnyDesk and RDP for persistence (articles 2, 3). Legitimate RMM tool traffic is increasingly the cover under which ransomware staging occurs, complicating detection.

- **Ransomware ecosystem professionalisation creates insider threat surface:** The RAMP leak (article 8) reveals a structured criminal marketplace with commercial deal mechanics. The BlackCat prosecution (articles 6, 7) shows the downstream consequence: professionalised ransomware operations create monetisable roles for insiders in victim organisations and their service providers.

---

## Article Analysis

---

### [0] Surge in Bomgar RMM Exploitation Demonstrates Supply Chain Risk

| Field | Value |
|---|---|
| **Source** | Dark Reading |
| **Published** | Tue, 21 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com/cyberattacks-data-breaches/surge-bomgar-rmm-exploitation...](https://www.darkreading.com/cyberattacks-data-breaches/surge-bomgar-rmm-exploitation-demonstrates-supply-chain-risk) |

**Summary:** Huntress SOC documented five exploitation incidents in two weeks targeting CVE-2026-1731, a critical unauthenticated RCE in Bomgar/BeyondTrust Remote Support. An April 15 attack against an MSP led to the mass isolation of 78 businesses and exploitation across four downstream customers; two other incidents confirmed LockBit ransomware deployment using the leaked LockBit 3.0 builder. Attackers systematically added rogue admin accounts, deployed additional RMMs (AnyDesk, Atera) for persistence, and pivoted from compromised MSP servers into all managed client networks.

**Severity Rationale:** Active exploitation of a critical unauthenticated RCE in widely deployed MSP tooling with confirmed ransomware deployment and documented supply-chain lateral spread to dozens of downstream organisations.

**Threat Actors:** LockBit

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Persistence |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | SMB/Windows Admin Shares | Lateral Movement |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-1731
- **URLs:** _none_

---

### [1] Kyber Ransomware Double Trouble: Windows and ESXi Attacks Explained

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | Tue, 21 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [rapid7.com/blog/post/tr-kyber-ransomware-double-trouble...](https://www.rapid7.com/blog/post/tr-kyber-ransomware-double-trouble-windows-esxi-attacks-explained) |

**Summary:** Rapid7 analysed a March 2026 incident response engagement recovering both Windows (Rust, AES-256-CTR + Kyber1024 + X25519) and ESXi (C++, actual ChaCha8 + RSA-4096 — despite ransom note claiming post-quantum encryption) Kyber variants from the same environment. The ESXi variant targets `/vmfs/volumes` datastores, gracefully terminates VMs via `esxcli` before encryption, and forks into a background process to survive SSH session termination. The Windows variant includes an experimental Hyper-V targeting module. Both share Tor-based negotiation infrastructure and a campaign ID, confirming coordinated cross-platform deployment.

**Severity Rationale:** Cross-platform ransomware actively deployed against enterprise VMware ESXi and Windows infrastructure in a confirmed March 2026 incident, with anti-recovery measures and ESXi-specific virtualisation disruption capabilities.

**Threat Actors:** Kyber

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | Execution |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** `Mlnmlnnrdhcaddwll4zqvfd2vyqsgtgj473gjoehwna2v4sizdukheyd[.]onion` (Kyber Tor chat), `Kyblogtz6k3jtxnjjvluee5ec4g3zcnvyvbgsnq5thumphmqidkt7xid[.]onion` (Kyber Tor blog/leak site)
- **Hashes:** `6ccacb7567b6c0bd2ca8e68ff59d5ef21e8f47fc1af70d4d88a421f1fc5280fc` (ESXi ELF SHA-256)
- **CVEs:** _none_
- **URLs:** _none_

---

### [2] SystemBC C2 Server Reveals 1,570+ Victims in The Gentlemen Ransomware Operation

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Tue, 21 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [thehackernews.com/2026/04/systembc-c2-server-reveals-1570-victims.html](https://thehackernews.com/2026/04/systembc-c2-server-reveals-1570-victims.html) |

**Summary:** Check Point Research gained visibility into a SystemBC C2 server used by a The Gentlemen affiliate, revealing over 1,570 compromised corporate networks globally — the majority in the US, UK, and Germany — not yet in public breach disclosures. SystemBC establishes RC4-encrypted SOCKS5 tunnels and can download payloads directly into memory. The group uses GPO-based domain-wide ransomware detonation, Cobalt Strike (C2 on ports 443/80) for lateral movement, and fields both Windows and ESXi encryptors. Industry-wide ransomware dwell times are collapsing, with Akira achieving foothold-to-encryption in under one hour in some incidents.

**Severity Rationale:** Confirmed botnet of 1,570+ unreported corporate victims with active RaaS cross-platform capability and direct C2 infrastructure visibility including actionable IPs.

**Threat Actors:** The Gentlemen, Akira, Qilin, Cl0p

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1090](https://attack.mitre.org/techniques/T1090/) | Proxy | Command and Control |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Group Policy Modification | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control |

**IOCs Extracted:**
- **IPs:** `45.86.230[.]112` (SystemBC C2), `91.107.247[.]163` (Cobalt Strike C2)
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [3] 'The Gentlemen' Rapidly Rises to Ransomware Prominence

| Field | Value |
|---|---|
| **Source** | Dark Reading |
| **Published** | Wed, 22 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com/threat-intelligence/gentlemen-rapidly-rise-ransomware](https://www.darkreading.com/threat-intelligence/gentlemen-rapidly-rise-ransomware) |

**Summary:** Dark Reading's profile, drawing on NCC Group, Comparitech, GuidePoint Security, and Check Point analysts, establishes The Gentlemen as the fastest-scaling ransomware operation in recent history — surpassing 150 victims in nine months compared to DragonForce's two years. Affiliates receive 90% of ransom proceeds, EDR-killing tools, and Group Policy-based mass deployment capability. An observed attack chain shows DC foothold → Cobalt Strike staging via admin shares → SystemBC SOCKS5 tunnelling → PowerShell Defender disablement → simultaneous ESXi and Windows encryption. The ESXi variant evades most VirusTotal AV engines.

**Severity Rationale:** Active, prolific RaaS with 320+ public victims and 1,570+ C2-visible unreported compromises; multi-platform capability and high affiliate payout signal sustained high-tempo operations.

**Threat Actors:** The Gentlemen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Group Policy Modification | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1090](https://attack.mitre.org/techniques/T1090/) | Proxy | Command and Control |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | Execution |

**IOCs Extracted:**
- _No IOCs extracted._

---

### [4] Trigona Ransomware Attacks Use Custom Exfiltration Tool to Steal Data

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | Thu, 23 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [bleepingcomputer.com/news/security/trigona-ransomware-attacks-use-custom-exfiltration-tool...](https://www.bleepingcomputer.com/news/security/trigona-ransomware-attacks-use-custom-exfiltration-tool-to-steal-data/) |

**Summary:** Symantec researchers documented a March 2026 Trigona affiliate attack using a custom exfiltration tool `uploader_client.exe` that supports five parallel upload connections per file, rotates TCP connections after 2GB of traffic, and uses an authentication key to restrict data access. The affiliate additionally deployed the Huorong kernel driver and six BYOVD tools (PCHunter, Gmer, YDark, WKTools, DumpGuard, StpProcessMonitorByovd) to disable endpoint protection, used AnyDesk for remote access, and executed Mimikatz and Nirsoft utilities for credential harvesting. Symantec published IOCs to assist defenders.

**Severity Rationale:** Active ransomware campaign with custom-built exfiltration tooling and a multi-stage EDR disruption chain, indicating a well-resourced affiliate deliberately investing in detection evasion.

**Threat Actors:** Trigona

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation (BYOVD) | Privilege Escalation |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |

**IOCs Extracted:**
- _No IOCs extracted (tool names identified but no hashes, IPs, or domains explicitly listed in available content)._

---

### [5] Trigona Affiliates Deploy Custom Exfiltration Tool to Streamline Data Theft

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Thu, 23 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [databreaches.net/2026/04/23/trigona-affiliates-deploy-custom-exfiltration...](https://databreaches.net/2026/04/23/trigona-affiliates-deploy-custom-exfiltration-tool-to-streamline-data-theft/) |

**Summary:** DataBreaches.Net coverage of the same Symantec/BleepingComputer Trigona report, contextualising the group's resurgence after a 2023 Ukrainian activist disruption. The article highlights that the custom exfiltration tool is a deliberate choice to avoid triggering security tools that detect public utilities like Rclone and MegaSync, indicating conscious OPSEC investment by the threat actor.

**Severity Rationale:** Corroborating coverage of an active Trigona campaign confirming the group's operational resurgence after a multi-year disruption.

**Threat Actors:** Trigona

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |

**IOCs Extracted:**
- _No IOCs extracted (RSS summary fallback)._

---

### [6] Ransomware Negotiator Pleads Guilty to BlackCat Scheme

| Field | Value |
|---|---|
| **Source** | Dark Reading |
| **Published** | Tue, 21 Apr 2026 |
| **Severity** | 🟡 Medium |
| **URL** | [darkreading.com/insider-threats/ransomware-negotiator-pleads-guilty-blackcat-scheme](https://www.darkreading.com/insider-threats/ransomware-negotiator-pleads-guilty-blackcat-scheme) |

**Summary:** Angelo Martino (41, DigitalMint) pled guilty to conspiring with BlackCat/ALPHV between April–November 2023, feeding victim insurance limits and negotiation strategies to attackers while posing as a trusted negotiator for five victims. He co-deployed BlackCat ransomware with Ryan Goldberg (Sygnia) and Kevin Martin (DigitalMint), extracting $1.2M in Bitcoin from one victim. DOJ seized $10M in total assets from Martino. Security experts recommend structurally separating negotiation, payment, and forensic roles to prevent future insider collusion.

**Severity Rationale:** Criminal prosecution confirming insider threat within the incident-response industry; significant structural implication for ransomware response governance but no active threat vector.

**Threat Actors:** BlackCat, ALPHV

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
- _No IOCs extracted._

---

### [7] Ransomware Negotiator Pleads Guilty to Aiding BlackCat Attacks in 2023

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | Tue, 21 Apr 2026 |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com/2026/04/ransomware-negotiator-pleads-guilty-to.html](https://thehackernews.com/2026/04/ransomware-negotiator-pleads-guilty-to.html) |

**Summary:** The Hacker News coverage of the Martino/BlackCat guilty plea, adding that Martin and Goldberg are scheduled for sentencing April 30, 2026, while Martino faces sentencing July 9, 2026 — all facing up to 20 years. The DOJ framed the case as a betrayal of the incident-response industry's foundational trust. Also surfaces a UK-based Scattered Spider affiliate who separately pled guilty to wire fraud and theft of $8M in virtual currency.

**Severity Rationale:** Companion coverage corroborating the BlackCat prosecution; medium severity as the threat actor has largely disbanded but the insider threat archetype remains live risk.

**Threat Actors:** BlackCat, ALPHV, Scattered Spider

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
- _No IOCs extracted._

---

### [8] RAMP Uncovered: Anatomy of Russia's Ransomware Marketplace

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Thu, 23 Apr 2026 |
| **Severity** | 🟡 Medium |
| **URL** | [databreaches.net/2026/04/23/ramp-uncovered-anatomy-of-russias-ransomware-marketplace...](https://databreaches.net/2026/04/23/ramp-uncovered-anatomy-of-russias-ransomware-marketplace/) |

**Summary:** A leaked RAMP database reveals the internal mechanics of Russia's primary ransomware affiliate marketplace — a structured commercial platform where criminals sell network access, recruit affiliates, advertise ransomware services, and negotiate deals in private channels. RAMP operates with business-grade deal structures, providing rare visibility into the financial and operational infrastructure underpinning RaaS at scale. The leak is a significant intelligence opportunity for understanding how ransomware groups source affiliates and initial access.

**Severity Rationale:** Threat intelligence report from a significant leaked database; provides strategic ecosystem context but does not describe an active exploitation campaign.

**Threat Actors:** RAMP forum operators

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
- _No IOCs extracted (RSS summary fallback)._

---

### [9] OCR Announces Settlements of Four Ransomware Investigations that Affected Over 427,000 Individuals

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Fri, 24 Apr 2026 |
| **Severity** | 🟢 Low |
| **URL** | [databreaches.net/2026/04/24/ocr-announces-settlements-of-four-ransomware-investigations...](https://databreaches.net/2026/04/24/ocr-announces-settlements-of-four-ransomware-investigations-that-affected-over-427000-individuals/) |

**Summary:** HHS OCR announced HIPAA settlements with four regulated entities following ransomware breach investigations, marking the 19th completed ransomware investigation under the Risk Analysis Initiative. The four organisations collectively affected approximately 427,000 individuals and all failed to conduct compliant HIPAA security risk analyses. All settlements include corrective action plans with two years of OCR monitoring.

**Severity Rationale:** Regulatory enforcement announcement covering historical breaches; informational for compliance teams with no active threat intelligence value.

**Threat Actors:** PYSA (referenced in related reporting)

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
- _No IOCs extracted (RSS summary fallback)._

---

### [10] Poor Risk Analysis Cost 4 Firms $1.7 Million in HIPAA Fines

| Field | Value |
|---|---|
| **Source** | BankInfoSecurity.com |
| **Published** | Apr 24, 2026 |
| **Severity** | 🟢 Low |
| **URL** | [bankinfosecurity.com/poor-risk-analysis-cost-4-firms-17-million-in-hipaa-fines-a-31506](https://www.bankinfosecurity.com/poor-risk-analysis-cost-4-firms-17-million-in-hipaa-fines-a-31506) |

**Summary:** Detailed breakdown of the HHS OCR settlements: Assured Imaging ($375K; PYSA ransomware 2020, ~245,000 victims), Regional Women's Health Group/Axia ($320K), Star Group SG Health Plan ($245K), and Consociate Health ($225K). A recurring failure pattern is organisations conducting gap assessments instead of full risk analyses — a distinction OCR does not accept. All four corrective action plans require full ePHI system inventories and documented risk scoring with remediation tracking.

**Severity Rationale:** Detailed regulatory and compliance reporting on historical ransomware breaches; actionable for healthcare security and compliance teams.

**Threat Actors:** PYSA

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
- _No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2026-1731` | 0 |
| Domain | `Kyblogtz6k3jtxnjjvluee5ec4g3zcnvyvbgsnq5thumphmqidkt7xid[.]onion` | 1 |
| Domain | `Mlnmlnnrdhcaddwll4zqvfd2vyqsgtgj473gjoehwna2v4sizdukheyd[.]onion` | 1 |
| Hash | `6ccacb7567b6c0bd2ca8e68ff59d5ef21e8f47fc1af70d4d88a421f1fc5280fc` | 1 |
| IP | `45.86.230[.]112` | 2 |
| IP | `91.107.247[.]163` | 2 |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | 4 |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | SMB/Windows Admin Shares | Lateral Movement | 0 |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | 1 |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration | 4, 5 |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | Execution | 1, 3 |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation (BYOVD) | Privilege Escalation | 4 |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control | 2 |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Persistence | 0 |
| [T1090](https://attack.mitre.org/techniques/T1090/) | Proxy | Command and Control | 2, 3 |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 0 |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control | 0, 3, 4 |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Group Policy Modification | Defense Evasion | 2, 3 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 0, 1, 2, 3, 4, 5 |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact | 1 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | 2, 3, 4, 5 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 11 |
| **Articles Analyzed** | 11 |
| **Articles Skipped** | 0 (3 used RSS summary fallback: DataBreaches.Net articles behind WAF) |
| **Date Filter Applied** | `--since 2026-04-21` (explicit, non-overlapping) |
| **Report Generated** | 2026-04-27 07:29:33 UTC |
