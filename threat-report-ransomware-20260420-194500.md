# Threat Intelligence Report: Ransomware

**Generated:** 2026-04-20 19:45:00 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-04-13 → 2026-04-20
**Articles Analyzed:** 9
**Sources:** BleepingComputer, Check Point Research, SecurityWeek, DataBreaches.Net, Malwarebytes, Google Cloud / Mandiant, Dark Reading, Google Cloud / GTIG

---

## Executive Summary

This week's collection reveals a ransomware ecosystem that has matured from opportunistic encryption to disciplined, infrastructure-backed big-game hunting: the Gentlemen RaaS operation's use of a 1,570-node SystemBC proxy botnet is operationally equivalent to a nation-state C2 architecture, signaling RaaS groups are now investing in persistent, reusable infrastructure between campaigns. Europe — and Germany specifically — is under disproportionate pressure, with the 92% DLS posting surge, active Mittelstand phishing campaigns, and Qilin/SAFEPAY/Sarcoma all operating concurrently; security teams supporting European manufacturing, legal, or construction clients should treat their environments as actively contested. The QEMU virtualization evasion technique represents a critical defensive gap: if ransomware payloads execute inside QEMU virtual machines on compromised hosts, most deployed EDR agents have no visibility, making the technique a force-multiplier for any operator who adopts it — prioritize QEMU binary execution and unusual VM disk image writes as hunt analytics. The Mandiant AI advisory is not hypothetical context: CVE-2025-26399 and CVE-2025-5777 appearing in live ransomware delivery chains within weeks of disclosure validates the compressed weaponization timeline thesis, and patch prioritization models based on 30-day windows are no longer operationally sound for internet-facing applications. Finally, the Synnovis/NHS case is a critical reminder for risk modeling: ransomware against a single pathology vendor has produced documented patient mortality two years post-incident, which means vendor dependency mapping and supply chain resilience must be treated as ransomware defense priorities, not just IT continuity concerns.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 4 |
| 🟠 High | 3 |
| 🟡 Medium | 1 |
| 🟢 Low | 1 |

---

## Cross-Article Connections

### Shared IOCs

_No shared IOCs identified across articles._

### Shared Threat Actors

#### Qilin
- **Seen in:** Articles [4], [8]
- **Activity:** Qilin is simultaneously responsible for long-tail critical infrastructure damage (the 2024 Synnovis/NHS attack still causing patient harm and delayed pathology reports in 2026) and is one of the primary drivers of Germany's 92% DLS growth surge in 2025, targeting Mittelstand SMBs. This dual presence across healthcare and European manufacturing/SMB sectors confirms Qilin as a high-tempo, indiscriminate RaaS operator with no sector exclusions.

#### The Gentlemen
- **Seen in:** Articles [0], [1]
- **Activity:** Articles 0 and 1 are complementary coverage of the same Gentlemen RaaS campaign — Article 0 provides strategic overview (1,570+ compromised SystemBC hosts, multi-platform lockers, named victims Oltenia Energy Complex and Adaptavist Group), while Article 1 provides DFIR-level technical detail (Domain Admin compromise chain, Cobalt Strike C2 at 91.107.247.163, SystemBC C2 at 45.86.230.112, PowerShell delivery of grand.exe). Together they reveal a mature RaaS affiliate with enterprise-grade proxy infrastructure and disciplined operational security.

### Campaign Threads

#### Gentlemen RaaS / SystemBC Proxy Infrastructure Campaign
- **Articles:** [0], [1]
- **Description:** The Gentlemen RaaS group has operationalized a botnet of 1,570+ compromised corporate hosts running SystemBC to provide covert, resilient proxy infrastructure. Affiliates use Cobalt Strike for lateral movement via ADMIN$ shares, Mimikatz/LSASS dumping for credential access, and GPO modification for simultaneous domain-wide encryption — a hallmark of sophisticated big-game hunting. Confirmed victims include Oltenia Energy Complex (critical infrastructure) and Adaptavist Group.
- **Timeline:** Domain Admin compromised → Cobalt Strike deployed via ADMIN$ shares (C2: 91.107.247.163) → Mimikatz credential dumping → SystemBC staged to 45.86.230.112 (blocked by EDR) → GPO modified for simultaneous encryption → grand.exe ransomware deployed via PowerShell. Both articles published 2026-04-20, indicating concurrent coordinated disclosure.

#### European SMB Ransomware Targeting Surge
- **Articles:** [5], [8]
- **Description:** Two articles independently document intensifying ransomware pressure on European SMBs, with Germany as the epicenter. Article 8 reports a 92% YoY growth in German DLS postings driven by SAFEPAY, Qilin, and Sarcoma targeting Mittelstand firms in manufacturing, legal, and construction sectors. Article 5 documents a concurrent DHL-themed phishing campaign targeting a German industrial supplier, delivering trojanized SimpleHelp RMM as a ransomware staging backdoor — a ground-level tactic consistent with the strategic surge documented in Article 8.
- **Timeline:** 2025: Germany DLS postings surge 92% (3x European average); SAFEPAY accumulates 76 German victims. 2026-04-17: Active DHL-phishing campaign targeting German industrial sector detected, delivering SimpleHelp RMM for ransomware staging. Ongoing: SAFEPAY, Qilin, Sarcoma continue targeting Mittelstand SMBs.

### Emerging Patterns

- **Legitimate and Dual-Use Tool Abuse for Covert C2 and Proxy Infrastructure:** Across the Gentlemen campaign (SystemBC as proxy botnet) and the German phishing campaign (trojanized SimpleHelp RMM as persistent backdoor), ransomware operators are systematically replacing custom C2 infrastructure with legitimate or dual-use tools. This significantly degrades detection efficacy for signature-based controls and makes network traffic analysis harder, as C2 blends with expected enterprise remote-access patterns. TI teams should treat RMM tool installations and proxy relay traffic as high-priority ransomware precursor signals. *(Articles [0], [1], [5])*

- **Credential Dumping as Universal Ransomware Prerequisite:** Articles covering Gentlemen (LSASS dump via Mimikatz) and the QEMU campaigns (SAM and NTDS dumps) all feature multi-stage credential harvesting before encryption. Detection of LSASS access, ntds.dit reads, or SAM registry hive exports should be treated as imminent ransomware precursors, not generic credential threats. *(Articles [0], [1], [2])*

- **Virtualization and Proxy Layers for Defense Evasion:** Both the Gentlemen campaign (SystemBC internal proxy, T1090.001) and the QEMU abuse campaigns (T1564.006 — running virtual instances) demonstrate adversaries inserting an abstraction layer between their tooling and host defenses. QEMU virtualization evades EDR by running malicious payloads inside a virtual machine the host OS cannot inspect; SystemBC routes C2 traffic through compromised corporate hosts to mask true C2 endpoints. This convergence of evasion-by-abstraction across unrelated threat actors signals the technique is becoming standard RaaS tradecraft. *(Articles [0], [1], [2])*

- **AI-Accelerated CVE Weaponization Compressing Patch Windows:** Mandiant/GTIG warns that LLM-assisted vulnerability discovery is being sold underground, with PRC-nexus operators distributing exploits rapidly across groups. This directly contextualizes Article 2, where two separate campaigns exploit CVE-2025-26399 and CVE-2025-5777 — relatively recent CVEs already weaponized into active ransomware delivery chains. TI teams must assume near-zero patch windows for critical internet-facing application CVEs. *(Articles [2], [6])*

- **Long-Tail Critical Infrastructure Impact from Ransomware:** The Qilin/Synnovis attack (Article 4) — executed in 2024 — is still producing measurable patient harm in 2026: 161,560 delayed pathology reports, documented patient death, 10,000+ cancelled appointments. Ransomware against healthcare supply chain vendors creates cascading, multi-year operational failures that are systematically under-attributed in short-cycle threat reporting. *(Articles [4], [8])*

---

## Article Analysis

---

### [1] The Gentlemen ransomware now uses SystemBC for bot-powered attacks

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | Mon, 20 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [bleepingcomputer.com/news/security/the-gentlemen-ransomware...](https://www.bleepingcomputer.com/news/security/the-gentlemen-ransomware-now-uses-systembc-for-bot-powered-attacks/) |

**Summary:** The Gentlemen ransomware-as-a-service (RaaS), active since mid-2025, has been observed leveraging SystemBC SOCKS5 proxy malware to maintain a botnet of over 1,570 predominantly corporate hosts across the US, UK, Germany, Australia, and Romania. Affiliates deploy a sophisticated attack chain involving Cobalt Strike lateral movement, Mimikatz credential harvesting, and GPO-based mass ransomware deployment, with confirmed victims including Oltenia Energy Complex and Adaptavist Group. The group operates Go-based lockers for Windows/Linux/NAS/BSD and a C-based ESXi variant, employing X25519 and XChaCha20 hybrid encryption with deliberate defense evasion via shadow copy deletion and process termination.

**Severity Rationale:** Active ransomware deployment confirmed against critical infrastructure and enterprise targets, with an operational botnet of 1,570+ hosts, ~320 claimed victims, and ongoing campaigns extending into 2026.

**Threat Actors:** The Gentlemen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | SMB/Windows Admin Shares | Lateral Movement |
| [T1078.002](https://attack.mitre.org/techniques/T1078/002/) | Domain Accounts | Privilege Escalation |
| [T1090.001](https://attack.mitre.org/techniques/T1090/001/) | Internal Proxy (SystemBC SOCKS5) | Command and Control |
| [T1003.001](https://attack.mitre.org/techniques/T1003/001/) | LSASS Memory (Mimikatz) | Credential Access |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Group Policy Modification | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:** _No IOCs extracted._

---

### [2] DFIR Report – The Gentlemen & SystemBC: A Sneak Peek Behind the Proxy

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | Mon, 20 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [research.checkpoint.com/2026/dfir-report-the-gentlemen/](https://research.checkpoint.com/2026/dfir-report-the-gentlemen/) |

**Summary:** Check Point's detailed DFIR of a Gentlemen RaaS affiliate attack documents Domain Admin compromise, Cobalt Strike lateral movement via ADMIN$ shares, PowerShell-based download and execution of grand.exe ransomware with built-in propagation, and SystemBC proxy staged to external C2. The RaaS has claimed 320+ victims with 240 attacks in the first months of 2026, operates multi-platform lockers for Windows/Linux/NAS/BSD/ESXi, and provides affiliates with EDR-killing tools. Negotiations use Tox P2P protocol, and the group maintains an X/Twitter account for victim pressure campaigns.

**Severity Rationale:** Confirmed ransomware deployment at scale with 320+ victims, active Domain Admin-level compromise, multi-platform locker capability including ESXi, and an ongoing RaaS operation with documented 2026 attacks.

**Threat Actors:** The Gentlemen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command and Scripting Interpreter: PowerShell | Execution |
| [T1569.002](https://attack.mitre.org/techniques/T1569/002/) | System Services: Service Execution | Execution |
| [T1082](https://attack.mitre.org/techniques/T1082/) | System Information Discovery | Discovery |
| [T1033](https://attack.mitre.org/techniques/T1033/) | System Owner/User Discovery | Discovery |
| [T1083](https://attack.mitre.org/techniques/T1083/) | File and Directory Discovery | Discovery |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Domain Policy Modification: Group Policy Modification | Defense Evasion |
| [T1090.001](https://attack.mitre.org/techniques/T1090/001/) | Proxy: Internal Proxy | Command and Control |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control |
| [T1573](https://attack.mitre.org/techniques/T1573/) | Encrypted Channel | Command and Control |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** `45.86.230.112` (SystemBC C2), `91.107.247.163` (Cobalt Strike C2)
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [3] Hackers Abuse QEMU for Defense Evasion

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Mon, 20 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [securityweek.com/hackers-abuse-qemu-for-defense-evasion/](https://www.securityweek.com/hackers-abuse-qemu-for-defense-evasion/) |

**Summary:** Sophos documented two distinct campaigns (STAC4713 and STAC3725) abusing QEMU virtualization to evade defenses, deploying ransomware and remote access trojans against enterprise targets. STAC4713, attributed to Gold Encounter, leveraged SonicWall VPN access and CVE-2025-26399 (SolarWinds Web Help Desk RCE) to deploy PayoutsKing ransomware and exfiltrate Active Directory credentials via QEMU-hosted reverse SSH tunnels targeting VMware/ESXi infrastructure. STAC3725 exploited CitrixBleed2 (CVE-2025-5777) for initial access, established persistence via malicious ScreenConnect, and conducted extensive post-exploitation including credential harvesting and AD reconnaissance, with access potentially brokered to multiple downstream threat actors.

**Severity Rationale:** Both campaigns involve confirmed ransomware deployment and active exploitation of remote code execution CVEs against enterprise VPN and remote access infrastructure, with credential theft and AD compromise indicating high-impact, multi-stage intrusions.

**Threat Actors:** Gold Encounter

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1133](https://attack.mitre.org/techniques/T1133/) | External Remote Services | Initial Access |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1053.005](https://attack.mitre.org/techniques/T1053/005/) | Scheduled Task/Job: Scheduled Task | Execution |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Defense Evasion |
| [T1564.006](https://attack.mitre.org/techniques/T1564/006/) | Hide Artifacts: Run Virtual Instance | Defense Evasion |
| [T1003.002](https://attack.mitre.org/techniques/T1003/002/) | OS Credential Dumping: Security Account Manager | Credential Access |
| [T1003.003](https://attack.mitre.org/techniques/T1003/003/) | OS Credential Dumping: NTDS | Credential Access |
| [T1558](https://attack.mitre.org/techniques/T1558/) | Steal or Forge Kerberos Tickets | Credential Access |
| [T1087](https://attack.mitre.org/techniques/T1087/) | Account Discovery | Discovery |
| [T1135](https://attack.mitre.org/techniques/T1135/) | Network Share Discovery | Discovery |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunneling | Command and Control |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** `CVE-2025-26399`, `CVE-2025-5777`
- **URLs:** _none_

---

### [4] Qilin's 2024 attack on NHS vendor continues to impact patient care for one NHS Trust

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Sun, 19 Apr 2026 |
| **Severity** | 🔴 Critical |
| **URL** | [databreaches.net/.../qilins-2024-attack-on-nhs-vendor...](https://databreaches.net/2026/04/19/qilins-2024-attack-on-nhs-vendor-continues-to-impact-patient-care-for-one-nhs-trust/) |

**Summary:** The Qilin ransomware group's June 2024 attack on Synnovis, an NHS pathology vendor serving South London trusts, continues to cause significant operational disruption at South London and Maudsley NHS Foundation Trust (SLaM) nearly two years after the initial incident. As of early 2026, SLaM has not restored electronic pathology systems, with over 161,560 pathology reports delayed and clinicians forced to rely on manual paper-based processes and phone communication for critical results. The attack has been attributed to causing direct patient harm to 170 individuals, more than 10,000 appointment cancellations, and at least one patient death.

**Severity Rationale:** Ransomware deployment against a critical healthcare vendor resulted in confirmed patient death, mass appointment cancellations, and nearly two years of sustained disruption to patient care infrastructure.

**Threat Actors:** Qilin

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Impact |

**IOCs Extracted:** _No IOCs extracted._

---

### [5] "Your shipment has arrived" email hides remote access software

| Field | Value |
|---|---|
| **Source** | Malwarebytes |
| **Published** | Fri, 17 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [malwarebytes.com/blog/news/2026/04/your-shipment-has-arrived...](https://www.malwarebytes.com/blog/news/2026/04/your-shipment-has-arrived-email-hides-remote-access-software) |

**Summary:** A phishing campaign impersonating DHL targets German industrial spare parts suppliers by delivering a malicious PDF attachment (AWB-Doc0921.pdf) that lures victims into downloading a trojanized SimpleHelp RMM installer (.scr) from a compromised Vietnamese logistics company domain. The payload, once executed, establishes a persistent beaconing connection enabling attacker-controlled remote access for reconnaissance, credential theft, lateral movement, and ransomware staging. The campaign leverages legitimate signed remote management tooling (LOLTech) to blend into normal enterprise traffic, targeting the German industrial sector consistent with broader European SMB extortion trends.

**Severity Rationale:** The campaign delivers a functional RMM-based backdoor enabling full remote access with explicit ransomware staging capability, against industrial sector targets — representing significant potential impact despite no confirmed ransomware deployment at time of reporting.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1566.001](https://attack.mitre.org/techniques/T1566/001/) | Phishing: Spearphishing Attachment | Initial Access |
| [T1204.002](https://attack.mitre.org/techniques/T1204/002/) | User Execution: Malicious File | Execution |
| [T1553.002](https://attack.mitre.org/techniques/T1553/002/) | Subvert Trust Controls: Code Signing | Defense Evasion |
| [T1218.011](https://attack.mitre.org/techniques/T1218/011/) | Signed Binary Proxy Execution: Rundll32 | Defense Evasion |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access |
| [T1082](https://attack.mitre.org/techniques/T1082/) | System Information Discovery | Discovery |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** `longhungphatlogistics[.]vn`
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** `longhungphatlogistics[.]vn/AWB-Doc0921.scr`

---

### [6] 6-Year Ransomware Campaign Targets Turkish Homes & SMBs

| Field | Value |
|---|---|
| **Source** | Dark Reading |
| **Published** | Thu, 16 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/.../6-year-ransomware-campaign-turkish-homes-smbs](https://www.darkreading.com/cyberattacks-data-breaches/6-year-ransomware-campaign-turkish-homes-smbs) |

**Summary:** Acronis researchers identified a financially-motivated ransomware campaign active since approximately 2020, exclusively targeting Turkish-speaking individuals and SMBs via phishing emails delivering a Java-based Adwind RAT variant. The RAT establishes C2 persistence, disables host defenses (Defender, Windows Update), and drops JanaWare ransomware with demands of $200–$400 per victim, using geofencing to restrict infections to Turkey and reduce law enforcement visibility. Threat actor identity remains unknown; total victim count is undetermined due to systematic under-reporting of small-scale attacks.

**Severity Rationale:** Active, multi-year ransomware campaign with confirmed payload deployment, involving defense evasion, C2 persistence, and file encryption — despite low per-victim demands, the sustained operational scope and SMB targeting justify a High rating.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1566.002](https://attack.mitre.org/techniques/T1566/002/) | Phishing: Spearphishing Link | Initial Access |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript/JScript | Execution |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion |
| [T1027.002](https://attack.mitre.org/techniques/T1027/002/) | Obfuscated Files or Information: Software Packing | Defense Evasion |
| [T1497.001](https://attack.mitre.org/techniques/T1497/001/) | Virtualization/Sandbox Evasion: System Checks | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1562.004](https://attack.mitre.org/techniques/T1562/004/) | Impair Defenses: Disable or Modify System Firewall | Defense Evasion |
| [T1102](https://attack.mitre.org/techniques/T1102/) | Web Service | Command and Control |
| [T1105](https://attack.mitre.org/techniques/T1105/) | Ingress Tool Transfer | Command and Control |
| [T1571](https://attack.mitre.org/techniques/T1571/) | Non-Standard Port | Command and Control |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact |

**IOCs Extracted:** _No IOCs extracted._

---

### [7] The German Cyber Criminal Überfall: Shifts in Europe's Data Leak Landscape

| Field | Value |
|---|---|
| **Source** | Google Cloud / GTIG |
| **Published** | Wed, 15 Apr 2026 |
| **Severity** | 🟠 High |
| **URL** | [cloud.google.com/.../europe-data-leak-landscape/](https://cloud.google.com/blog/topics/threat-intelligence/europe-data-leak-landscape/) |

**Summary:** GTIG reports a 92% surge in data leak site postings targeting Germany in 2025, nearly triple the European average, driven by SAFEPAY and Qilin filling the void left by LockBit and ALPHV disruptions. Ransomware operators are strategically pivoting toward German Mittelstand (SMBs under 5,000 employees), who account for 96% of victims, with manufacturing (23%), legal/professional services (14%), and construction (11%) sectors bearing the heaviest exposure. The trend is amplified by AI-enabled localization reducing language barriers and threat actor Sarcoma actively soliciting access to German company networks since November 2024.

**Severity Rationale:** Active, accelerating ransomware campaign with named threat actors claiming hundreds of confirmed victims and explicit targeting of a specific national SMB ecosystem, representing a significant ongoing large-scale threat.

**Threat Actors:** SAFEPAY, Qilin, Sarcoma, LockBit, ALPHV

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._

---

### [8] Defending Your Enterprise When AI Models Can Find Vulnerabilities Faster Than Ever

| Field | Value |
|---|---|
| **Source** | Google Cloud / Mandiant |
| **Published** | Thu, 16 Apr 2026 |
| **Severity** | 🟡 Medium |
| **URL** | [cloud.google.com/.../defending-enterprise-ai-vulnerabilities/](https://cloud.google.com/blog/topics/threat-intelligence/defending-enterprise-ai-vulnerabilities/) |

**Summary:** Google's Mandiant/GTIG has issued a strategic advisory documenting the observed use of large language models by threat actors to accelerate vulnerability discovery and exploitation, with activity including underground forum advertisement of LLM-assisted exploit services. PRC-nexus operators have been observed rapidly distributing exploits across otherwise siloed threat groups, increasing the scale and speed of potential mass exploitation campaigns. The advisory warns that AI-enabled vulnerability research will lower the barrier to entry for ransomware and extortion operations targeting enterprise environments.

**Severity Rationale:** Strategic advisory documenting an emerging trend with observed but non-specific threat actor activity; no confirmed active exploitation campaign or specific victim — warrants medium priority for strategic planning.

**Threat Actors:** PRC-nexus operators

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._

---

### [9] The backup myth that is putting businesses at risk

| Field | Value |
|---|---|
| **Source** | BleepingComputer (Sponsored) |
| **Published** | Mon, 20 Apr 2026 |
| **Severity** | 🟢 Low |
| **URL** | [bleepingcomputer.com/.../the-backup-myth-that-is-putting-businesses-at-risk/](https://www.bleepingcomputer.com/news/security/the-backup-myth-that-is-putting-businesses-at-risk/) |

**Summary:** Vendor-sponsored content by Datto arguing that backup solutions alone are insufficient to protect businesses from ransomware, as they address data recovery but not operational continuity during downtime. The piece advocates for comprehensive Business Continuity and Disaster Recovery (BCDR) strategies. No specific threat actors, incidents, or active campaigns are referenced.

**Severity Rationale:** The article contains no actionable threat intelligence, IOCs, or reports of active exploitation — it is informational vendor marketing content.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:** _No techniques mapped._

**IOCs Extracted:** _No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| IP | `45.86.230.112` | [2] Check Point Research |
| IP | `91.107.247.163` | [2] Check Point Research |
| Domain | `longhungphatlogistics[.]vn` | [5] Malwarebytes |
| CVE | `CVE-2025-26399` | [3] SecurityWeek |
| CVE | `CVE-2025-5777` | [3] SecurityWeek |
| URL | `longhungphatlogistics[.]vn/AWB-Doc0921.scr` | [5] Malwarebytes |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1133](https://attack.mitre.org/techniques/T1133/) | External Remote Services | Initial Access | [3] |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | [3] |
| [T1566.001](https://attack.mitre.org/techniques/T1566/001/) | Phishing: Spearphishing Attachment | Initial Access | [5] |
| [T1566.002](https://attack.mitre.org/techniques/T1566/002/) | Phishing: Spearphishing Link | Initial Access | [6] |
| [T1053.005](https://attack.mitre.org/techniques/T1053/005/) | Scheduled Task/Job: Scheduled Task | Execution | [3] |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command and Scripting Interpreter: PowerShell | Execution | [2] |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript/JScript | Execution | [6] |
| [T1204.002](https://attack.mitre.org/techniques/T1204/002/) | User Execution: Malicious File | Execution | [5] |
| [T1569.002](https://attack.mitre.org/techniques/T1569/002/) | System Services: Service Execution | Execution | [2] |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Defense Evasion | [3] |
| [T1078.002](https://attack.mitre.org/techniques/T1078/002/) | Valid Accounts: Domain Accounts | Privilege Escalation | [1] |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | [6] |
| [T1027.002](https://attack.mitre.org/techniques/T1027/002/) | Obfuscated Files or Information: Software Packing | Defense Evasion | [6] |
| [T1218.011](https://attack.mitre.org/techniques/T1218/011/) | Signed Binary Proxy Execution: Rundll32 | Defense Evasion | [5] |
| [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Domain Policy Modification: Group Policy Modification | Defense Evasion | [1], [2] |
| [T1497.001](https://attack.mitre.org/techniques/T1497/001/) | Virtualization/Sandbox Evasion: System Checks | Defense Evasion | [6] |
| [T1553.002](https://attack.mitre.org/techniques/T1553/002/) | Subvert Trust Controls: Code Signing | Defense Evasion | [5] |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | [6] |
| [T1562.004](https://attack.mitre.org/techniques/T1562/004/) | Impair Defenses: Disable or Modify System Firewall | Defense Evasion | [6] |
| [T1564.006](https://attack.mitre.org/techniques/T1564/006/) | Hide Artifacts: Run Virtual Instance (QEMU) | Defense Evasion | [3] |
| [T1003](https://attack.mitre.org/techniques/T1003/) | OS Credential Dumping | Credential Access | [2], [5] |
| [T1003.001](https://attack.mitre.org/techniques/T1003/001/) | OS Credential Dumping: LSASS Memory | Credential Access | [1] |
| [T1003.002](https://attack.mitre.org/techniques/T1003/002/) | OS Credential Dumping: Security Account Manager | Credential Access | [3] |
| [T1003.003](https://attack.mitre.org/techniques/T1003/003/) | OS Credential Dumping: NTDS | Credential Access | [3] |
| [T1558](https://attack.mitre.org/techniques/T1558/) | Steal or Forge Kerberos Tickets | Credential Access | [3] |
| [T1033](https://attack.mitre.org/techniques/T1033/) | System Owner/User Discovery | Discovery | [2] |
| [T1082](https://attack.mitre.org/techniques/T1082/) | System Information Discovery | Discovery | [2], [5] |
| [T1083](https://attack.mitre.org/techniques/T1083/) | File and Directory Discovery | Discovery | [2] |
| [T1087](https://attack.mitre.org/techniques/T1087/) | Account Discovery | Discovery | [3] |
| [T1135](https://attack.mitre.org/techniques/T1135/) | Network Share Discovery | Discovery | [3] |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement | [5] |
| [T1021.002](https://attack.mitre.org/techniques/T1021/002/) | Remote Services: SMB/Windows Admin Shares | Lateral Movement | [1], [2] |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control | [2], [5] |
| [T1090.001](https://attack.mitre.org/techniques/T1090/001/) | Proxy: Internal Proxy (SystemBC) | Command and Control | [1], [2] |
| [T1102](https://attack.mitre.org/techniques/T1102/) | Web Service | Command and Control | [6] |
| [T1105](https://attack.mitre.org/techniques/T1105/) | Ingress Tool Transfer | Command and Control | [6] |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control | [3], [5] |
| [T1571](https://attack.mitre.org/techniques/T1571/) | Non-Standard Port | Command and Control | [6] |
| [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunneling (QEMU SSH) | Command and Control | [3] |
| [T1573](https://attack.mitre.org/techniques/T1573/) | Encrypted Channel | Command and Control | [2] |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration | [3] |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | [1], [2], [3], [4], [5], [6] |
| [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Impact | [1], [4] |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact | [1], [6] |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 9 |
| **Articles Analyzed** | 9 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-04-20 19:45:00 UTC |
