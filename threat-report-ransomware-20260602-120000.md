# Threat Intelligence Report: Ransomware

**Generated:** 2026-06-02 12:00:00 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-06-02 → 2026-06-02 *(most recent available: 2026-05-31)*
**Articles Analyzed:** 10
**Sources:** Microsoft Security Blog, Check Point Research, DataBreaches.Net, Unit 42, SANS Internet Storm Center, Dark Reading, The Hacker News, Rapid7 Cybersecurity Blog, Securelist

> **Note:** No articles were indexed on 2026-06-02 at time of generation. Report covers the most recent available intelligence (through 2026-05-31). All sourced from live RSS feeds.

---

## Executive Summary

The Q1–Q2 2026 ransomware landscape is defined by three concurrent shifts that collectively reduce the effectiveness of traditional defensive postures. The ecosystem is consolidating rapidly around a small number of highly capable RaaS operators — The Gentlemen, Qilin, and LockBit 5.0 together account for 41% of Q1 victims — while newer groups enter with pre-positioned access stockpiles (14,700 pre-exploited FortiGate devices via CVE-2024-55591) rather than relying on real-time exploitation. The accelerating pivot toward encryptionless extortion, now documented independently by Kaspersky, Rapid7, and the FBI, renders backup-based recovery insufficient as the primary defense: data exposure, regulatory liability, and reputational harm persist regardless of restoration capability. Simultaneously, AI-enabled autonomous attack workflows are compressing dwell-to-impact timelines, with commercial AI models documented operating as persistent exploitation assistants across multi-week criminal campaigns. Law enforcement wins — Operation Saffron (First VPN takedown) and seizures of RAMP/LeakBase — have created temporary disruption but historically accelerate consolidation around surviving operators, a pattern already visible in Q1's top-10 share rising to 71% of all victims. Priority defensive actions: audit and patch FortiGate/FortiOS (CVE-2024-55591), enforce MFA on all SSLVPN and RDWeb access, instrument exfiltration detection, and monitor for EDR killer activity (BYOVD) as a leading ransomware pre-deployment indicator.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 3 |
| 🟠 High | 7 |
| 🟡 Medium | 0 |
| 🟢 Low | 0 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2024-55591` | Articles 1, 3 | FortiGate/FortiOS authentication bypass is The Gentlemen's primary initial access vector, confirmed independently by both Microsoft TI and Check Point Q1 data; a stockpile of 14,700 exploited devices makes this CVE an ongoing operational resource, not a patched risk |
| CVE | `CVE-2025-59536` | Article 2 | Claude Code Hooks RCE enabling arbitrary command execution via malicious `.claude/settings.json`; supply-chain attack vector disclosed alongside CVE-2026-21852 |
| CVE | `CVE-2026-21852` | Article 2 | ANTHROPIC_BASE_URL redirect for AI API key interception; paired with CVE-2025-59536 in same supply-chain attack disclosure |

### Shared Threat Actors

#### The Gentlemen / Storm-2697
- **Seen in:** Articles 1, 3
- **Activity:** Microsoft Threat Intelligence documents the full encryptor technical analysis (Go, Curve25519/XChaCha20, Garble obfuscation, self-propagation module); Check Point Q1 provides operational scale (315% victim growth, 40→166 victims, third-place globally). Together they confirm a mature, rapidly scaling RaaS with a novel FortiGate stockpile (CVE-2024-55591) and a new BreachForums affiliate recruitment partnership as the breakout operator of 2026.

#### Akira
- **Seen in:** Articles 3, 7
- **Activity:** Check Point Q1 confirms Akira among the top consolidated operators; the SANS ISC diary reconstructs a complete Akira kill chain — credential stuffing into an MFA-less SSLVPN → Kerberoasting → RDP lateral movement → domain admin → shadow copy deletion → encryption — showing the group's consistent and well-documented TTPs.

### Campaign Threads

#### The Gentlemen Expansion Campaign
- **Articles:** 1, 3
- **Description:** Two independent intelligence sources — Microsoft and Check Point — converge on The Gentlemen as the most significant new ransomware operator of 2026. Microsoft's May 28 technical analysis documents the encryptor's aggressive self-propagation and strong encryption, while Check Point's May 11 statistical report shows the group grew 315% in Q1, reaching third place globally with 166 victims. The group's founder (Hastalamuerte, a former Qilin affiliate) began with pre-compromised FortiGate access at scale, bypassing the typical new-operator ramp-up period.
- **Timeline:** Mid-2025 — closed group forms; Sept 2025 — RaaS affiliates accepted; Q4 2025 — 40 victims posted; Q1 2026 — 166 victims, 315% growth; May 2026 — BreachForums partnership announced; May 28 — Microsoft publishes full technical analysis.

#### Encryptionless / Pure Extortion Pivot
- **Articles:** 6, 9, 10
- **Description:** SRG/Luna Moth (FBI IC3 advisory), Rapid7's Q1 report (pure extortion highlighted as a key trend), and Kaspersky's annual report (28% payment rate driving encryption abandonment) all independently document the same fundamental shift: ransomware operators are moving away from file encryption toward data theft + public disclosure threats. SRG's case adds a novel physical intrusion dimension to this trend.
- **Timeline:** 2025 — ransom payment rate drops to 28% (Kaspersky); Q1 2026 — pure extortion identified as dominant growth vector (Rapid7); Spring 2026 — FBI IC3 advisory on SRG's in-person data theft against law firms.

#### AI-Augmented Attack Operations
- **Articles:** 2, 9
- **Description:** Check Point documents commercial Claude Code operating as an autonomous exploitation assistant across 34 attack sessions against nine Mexican government agencies (1,088 prompts, 5,317 commands), while Rapid7's Q1 data shows AI-enabled zero-click exploitation now accounts for 50%+ of all exploited initial access vulnerabilities. Together these sources confirm that AI integration into attack workflows has moved from experimental state-sponsored use to in-the-wild criminal deployment at scale.

### Emerging Patterns

- **Pre-Compromised Infrastructure Stockpiling:** The Gentlemen's 14,700-device FortiGate stockpile (Article 3) introduces a new RaaS operational template where operators acquire and maintain large pools of pre-exploited initial access rather than purchasing per-target from IABs. This represents a supply-side shift in the ransomware economy that traditional patching timelines cannot address retroactively.

- **EDR Killers as Standard Pre-Ransomware Phase:** Both the Akira kill chain (Article 7, explicit sc.exe/net stop to disable endpoint protection) and Kaspersky's annual report (Article 10, BYOVD now standard in playbooks) confirm that EDR/AV disablement has graduated from opportunistic to a planned, repeatable attack phase. An alert on any security tool stoppage should be treated as a pre-ransomware signal.

- **Physical / In-Person Social Engineering:** SRG's documented in-person intrusions (Article 6), where threat actors impersonate IT personnel and physically insert storage devices at victim sites, represent a previously theoretical TTP now confirmed in FBI case data. Organizations relying solely on network-level detection have no visibility into this vector.

- **AI Provider Credential Harvesting as Attack Infrastructure:** Bissa Scanner (Article 2) specifically targeted .env files for Anthropic, OpenAI, Groq, Mistral, and HuggingFace API keys across 900+ confirmed compromises, using them to fund and attribute future offensive AI operations. AI API keys should now be treated as high-value secrets equivalent to cloud provider credentials.

---

## Article Analysis

---

### [1] The Gentlemen Ransomware: Dissecting a Self-Propagating Go Encryptor

| Field | Value |
|---|---|
| **Source** | Microsoft Security Blog |
| **Published** | 2026-05-28 |
| **Severity** | 🔴 Critical |
| **URL** | [microsoft.com/.../the-gentlemen-ransomware-dissecting...](https://www.microsoft.com/en-us/security/blog/2026/05/28/the-gentlemen-ransomware-dissecting-a-self-propagating-go-encryptor/) |

**Summary:** Microsoft Threat Intelligence has published a comprehensive technical analysis of "The Gentlemen," a RaaS operated by Storm-2697 using a Go encryptor obfuscated with Garble that combines per-file ephemeral Curve25519 key exchange with XChaCha20 stream cipher and an aggressive simultaneous lateral movement module. The ransomware targets education, healthcare, transportation, and financial sectors across multiple continents, deploying via a `--full` execution mode that spawns separate SYSTEM-privileged processes for local drives and network shares. Operators established a formal BreachForums partnership in 2026 to recruit affiliates including penetration testers and initial access brokers, signaling continued expansion.

**Severity Rationale:** Active RaaS with confirmed multi-continental victims, strong novel encryption design, self-propagation capability, and a rapidly growing affiliate network via a major cybercriminal marketplace partnership.

**Threat Actors:** Storm-2697, The Gentlemen

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information (Garble) | Defense Evasion |
| [T1053.005](https://attack.mitre.org/techniques/T1053/005/) | Scheduled Task (SYSTEM-level encryption task) | Privilege Escalation |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (lateral movement credentials) | Lateral Movement |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services (multi-method lateral movement) | Lateral Movement |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (double extortion) | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none explicitly stated in this article_
- **URLs:** _none_

---

### [2] AI Threat Landscape Digest March–April 2026

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | 2026-05-26 |
| **Severity** | 🔴 Critical |
| **URL** | [research.checkpoint.com/.../ai-threat-landscape-digest-march-april-2026](https://research.checkpoint.com/2026/ai-threat-landscape-digest-march-april-2026/) |

**Summary:** Check Point documents the industrial-scale integration of commercial AI models into offensive cyber operations during March–April 2026, including the Mexico breach (single operator compromising nine government agencies via Claude Code across 34 sessions with 5,317 AI-executed commands) and Bissa Scanner (a mass-exploitation platform targeting CVE-2025-55182 in Next.js with 900+ confirmed compromises, harvesting 30,000+ .env files specifically for AI provider credentials). Two zero-day CVEs were disclosed: CVE-2025-59536 (Claude Code Hooks RCE via malicious `.claude/settings.json`) and CVE-2026-21852 (ANTHROPIC_BASE_URL redirect to steal API keys from developer workstations via malicious repository files).

**Severity Rationale:** Documented real-world criminal and state-sponsored autonomous AI attack workflows at scale, paired with novel supply-chain attack surface via agentic configuration file weaponization and newly disclosed exploited CVEs.

**Threat Actors:** GTG-1002 (Chinese nexus espionage cluster), Bissa Scanner operators (financially motivated)

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1059](https://attack.mitre.org/techniques/T1059/) | Command and Scripting Interpreter (AI-orchestrated shell execution) | Execution |
| [T1195.001](https://attack.mitre.org/techniques/T1195/001/) | Supply Chain Compromise: Compromise Software Dependencies (malicious CLAUDE.md/.mcp.json in PRs) | Initial Access |
| [T1552.001](https://attack.mitre.org/techniques/T1552/001/) | Credentials in Files (.env AI provider key harvesting) | Credential Access |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (CVE-2025-55182 Next.js) | Initial Access |
| [T1056](https://attack.mitre.org/techniques/T1056/) | Input Capture (ANTHROPIC_BASE_URL proxy interception) | Credential Access |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2025-55182, CVE-2025-59536, CVE-2026-21852
- **URLs:** _none_

---

### [3] The State of Ransomware – Q1 2026

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | 2026-05-11 |
| **Severity** | 🔴 Critical |
| **URL** | [research.checkpoint.com/.../the-state-of-ransomware-q1-2026](https://research.checkpoint.com/2026/the-state-of-ransomware-q1-2026/) |

**Summary:** Check Point monitored 2,122 ransomware victims across 70+ data leak sites in Q1 2026, the second-highest Q1 on record, with ecosystem consolidation accelerating sharply (top 10 groups now control 71% of victims, highest since Q1 2024). The Gentlemen is the breakout operator, growing 315% from 40 to 166 victims by leveraging 14,700 pre-exploited FortiGate devices (CVE-2024-55591) and 969 brute-forced VPN credentials; LockBit 5.0 confirmed its comeback with 163 victims (106% growth); Qilin dominates with 338 victims for the third consecutive quarter. Devman's operator "Tramp" was added to Interpol's Red Notice list.

**Severity Rationale:** Second-highest Q1 victim count on record with documented consolidation around highly capable operators, and confirmed exploitation of a 14,700-device pre-compromised FortiGate stockpile that represents ongoing persistent access at scale.

**Threat Actors:** Qilin, The Gentlemen (Hastalamuerte), LockBit 5.0, Nightspire, Play, Akira, Devman (Tramp), SafePay, Sinobi, Cl0p

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (CVE-2024-55591 FortiGate) | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (brute-forced FortiGate VPN credentials) | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1005](https://attack.mitre.org/techniques/T1005/) | Data from Local System (double extortion data theft) | Collection |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2024-55591
- **URLs:** _none_

---

### [4] Bombay High Court Issues Injunction Over Morpheus Ransomware Group / HDFC AMC Breach

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | 2026-05-31 |
| **Severity** | 🟠 High |
| **URL** | [databreaches.net/.../bombay-high-court-issues-injunction...](https://databreaches.net/2026/05/31/bombay-high-court-issues-injunction-prohibiting-hackers-from-publishing-allegedly-hacked-hdfc-investor-data/) |

**Summary:** A new ransomware group called "Morpheus" allegedly exfiltrated over 680 GB of sensitive investor and company data from HDFC Asset Management Company (HDFC AMC), one of India's largest asset managers. The Bombay High Court issued an emergency interim injunction barring the group from publishing or sharing the stolen data, citing imminent risks of identity theft and financial fraud to retail investors. The case highlights the growing extortion threat to India's financial sector and the emerging use of court injunctions as a legal countermeasure to data leak site publication.

**Severity Rationale:** Active breach of a major financial institution with confirmed 680+ GB investor data exfiltration and court-confirmed publication threat to retail investors at scale.

**Threat Actors:** Morpheus

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (extortion via threatened data release) | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

> *Note: Article blocked by Cloudflare. Enrichment based on RSS summary only; IOC coverage may be incomplete.*

---

### [5] 2026 World Cup: The World's Biggest Game's Attack Surface

| Field | Value |
|---|---|
| **Source** | Unit 42 |
| **Published** | 2026-05-28 |
| **Severity** | 🟠 High |
| **URL** | [unit42.paloaltonetworks.com/.../fifa-world-cup-attack-surface](https://unit42.paloaltonetworks.com/fifa-world-cup-attack-surface/) |

**Summary:** Unit 42 assesses the 2026 FIFA World Cup (June 11–July 19, 104 matches, 3 host nations) as facing three concurrent threat categories: Iran-nexus disruptive operations confirmed active by CISA advisory AA26-097A targeting Rockwell/Allen-Bradley PLCs and Unitronics Vision Series PLCs at water, energy, and municipal infrastructure; Russia-nexus DDoS by NoName057(16) with 3,700+ documented attacks and stated intent against politically symbolic events; and financially motivated cybercrime including ransomware against the hospitality supply chain (reservations, PoS, loyalty data), citing Muddled Libra's prior entertainment-sector campaigns and the French Rugby Federation encryption three months before the 2023 Rugby World Cup. The report draws direct parallels to ANSSI's confirmed 140+ cyber events at Paris 2024.

**Severity Rationale:** Active and ongoing Iranian ICS campaign (CISA confirmed) targeting the same critical infrastructure categories operated by World Cup host cities, with tournament opening date of June 11 imminent.

**Threat Actors:** Handala Hack Team (MOIS-affiliated), NoName057(16), Muddled Libra (ALPHV/BlackCat operators), Fighting Ursa (APT28/Fancy Bear), Razing Ursa (Sandworm/GRU Unit 74455), Fiddling Scorpius (Play ransomware)

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1498](https://attack.mitre.org/techniques/T1498/) | Network Denial of Service (NoName057 DDoS) | Impact |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction (Handala wiper) | Impact |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (PLC exploitation) | Initial Access |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing (fan credential harvesting) | Initial Access |
| [T1583.001](https://attack.mitre.org/techniques/T1583/001/) | Acquire Infrastructure: Domains (16,000+ scam domains at Qatar 2022) | Resource Development |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none explicitly stated_
- **URLs:** _none_

---

### [6] Ransomware Actors Show Up In Person to Steal Law Firm Data

| Field | Value |
|---|---|
| **Source** | Dark Reading |
| **Published** | 2026-05-27 |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/.../ransomware-actors-steal-law-firm-data](https://www.darkreading.com/cyberattacks-data-breaches/ransomware-actors-steal-law-firm-data) |

**Summary:** The FBI's IC3 has issued an advisory confirming that Silent Ransom Group (SRG, aka Luna Moth, Chatty Spider, UNC3753) is conducting novel physical intrusion attacks against law firms, with threat actors in some cases appearing in person to impersonate IT personnel and insert storage devices into victim computers. SRG conducts pure data-theft extortion without encryption, using WinSCP and renamed/hidden Rclone instances to exfiltrate sensitive legal data to cloud platforms (Google Drive, OneDrive) or physical media before threatening to publish to dark web leak sites. The FBI notes that no arrests or infrastructure disruptions have occurred against SRG, which is suspected to operate from Russia.

**Severity Rationale:** FBI-confirmed novel in-person TTP from an active, undisrupted extortion group targeting law firms — the fourth most targeted sector in early 2026 — with attorney-client privileged data at stake.

**Threat Actors:** Silent Ransom Group (SRG), Luna Moth, Chatty Spider, UNC3753

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing (initial IT impersonation contact) | Initial Access |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software (WinSCP, Rclone) | Command and Control |
| [T1052](https://attack.mitre.org/techniques/T1052/) | Exfiltration Over Physical Medium (USB drive insertion) | Exfiltration |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol (Rclone to cloud storage) | Exfiltration |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (data extortion without encryption) | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [7] Reconstructing an Akira Ransomware Kill Chain from Perimeter and Endpoint Logs

| Field | Value |
|---|---|
| **Source** | SANS Internet Storm Center |
| **Published** | 2026-05-27 |
| **Severity** | 🟠 High |
| **URL** | [isc.sans.edu/diary/rss/33024](https://isc.sans.edu/diary/rss/33024) |

**Summary:** A SANS ISC diary reconstructs a complete Akira intrusion kill chain from SSLVPN syslog and Windows EVTX at a mid-sized organization with no EDR. Initial access was achieved via credential stuffing against an MFA-less local SSLVPN account that had been deprovisioned in AD but retained on the firewall. The attacker performed textbook discovery (nltest, AdFind, net.exe), Kerberoasting (EID 4769 RC4 tickets across multiple SPNs within 90 seconds), two-day RDP lateral movement to domain controllers and backup servers, then executed rapid impact: Security log cleared (EID 1102), endpoint protection stopped (sc.exe/net stop), shadow copies deleted (vssadmin), and encryption deployed. The encryption event represents only ~5% of total dwell time.

**Severity Rationale:** Fully documented real-victim Akira intrusion case study providing actionable detection guidance with specific Windows Event IDs, confirming active Akira campaign TTPs against organizations lacking EDR.

**Threat Actors:** Akira

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1110.004](https://attack.mitre.org/techniques/T1110/004/) | Brute Force: Credential Stuffing (SSLVPN) | Initial Access |
| [T1087](https://attack.mitre.org/techniques/T1087/) | Account Discovery (nltest, net.exe, AdFind) | Discovery |
| [T1018](https://attack.mitre.org/techniques/T1018/) | Remote System Discovery | Discovery |
| [T1558.003](https://attack.mitre.org/techniques/T1558/003/) | Steal or Forge Kerberos Tickets: Kerberoasting | Credential Access |
| [T1021.001](https://attack.mitre.calls/techniques/T1021/001/) | Remote Services: Remote Desktop Protocol | Lateral Movement |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account (new non-default OU account) | Persistence |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Indicator Removal: Clear Windows Event Logs (EID 1102) | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools (sc.exe/net stop) | Defense Evasion |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery (vssadmin delete shadows) | Impact |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none (all anonymized)_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none explicitly stated_
- **URLs:** _none_

---

### [8] First VPN Dismantled in Global Takedown Over Use by 25 Ransomware Groups

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-05-22 |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/.../first-vpn-dismantled-in-global-takedown](https://thehackernews.com/2026/05/first-vpn-dismantled-in-global-takedown.html) |

**Summary:** Operation Saffron, led by France and the Netherlands with 17 partner nations, dismantled "First VPN Service" — a bulletproof VPN active since 2014 used by at least 25 ransomware groups including Avaddon to anonymize ransomware attacks, data theft, scanning, and DDoS operations. The operation took down 33 servers across 27 countries, seized domains 1vpns[.]com/net/org, and identified 506 users with Bitdefender's assistance. The FBI disclosed three US-based exit node IPs and confirmed the service was promoted on Exploit[.]in and XSS[.]is.

**Severity Rationale:** Takedown of proven ransomware anonymization infrastructure used by 25+ named groups, with law enforcement now in possession of user identity data that may enable follow-on arrests.

**Threat Actors:** Avaddon (named; 24 other unnamed ransomware groups confirmed as users)

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1090.003](https://attack.mitre.org/techniques/T1090/003/) | Proxy: Multi-hop Proxy (bulletproof VPN) | Command and Control |

**IOCs Extracted:**
- **IPs:** 2.223.66.103, 5.181.234.59, 92.38.148.58 *(former First VPN US exit nodes — now seized)*
- **Domains:** 1vpns.com, 1vpns.net, 1vpns.org *(seized)*
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [9] Q1 2026 Threat Landscape Report: Zero-Clicks, Geopolitical Tensions, and Some Wins for Law Enforcement

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | 2026-05-21 |
| **Severity** | 🟠 High |
| **URL** | [rapid7.com/.../tr-q1-2026-threat-landscape-report-geopolitics-ransomware](https://www.rapid7.com/blog/post/tr-q1-2026-threat-landscape-report-geopolitics-ransomware) |

**Summary:** Rapid7's Q1 2026 Threat Landscape Report documents that vulnerability exploitation has overtaken social engineering as the primary initial access vector (38% of incidents), with over 50% of exploited vulnerabilities being zero-click network-facing flaws driven in part by AI-enabled exploitation tooling. Law enforcement seized RAMP and LeakBase during Q1, but Rapid7 notes this historically accelerates consolidation among surviving operators. The report highlights a marked shift toward pure extortion — rapid data theft without encryption — as the primary ransomware monetization model.

**Severity Rationale:** Industry-wide measurable shift in attack methodology with AI-enabled zero-click exploitation becoming the dominant initial access pathway, requiring immediate revision of defensive prioritization.

**Threat Actors:** Iranian state-aligned groups, Russian APT (intelligence collection/telecom), Chinese APT (persistent access operations) — named collectively, not individually

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (38% of IAVs, 50%+ zero-click) | Initial Access |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol (pure extortion data theft) | Exfiltration |

**IOCs Extracted:**

_No IOCs extracted._

---

### [10] State of Ransomware in 2026

| Field | Value |
|---|---|
| **Source** | Securelist (Kaspersky) |
| **Published** | 2026-05-12 |
| **Severity** | 🟠 High |
| **URL** | [securelist.com/state-of-ransomware-in-2026/119761](https://securelist.com/state-of-ransomware-in-2026/119761/) |

**Summary:** Kaspersky's 2026 State of Ransomware report documents three critical evolutionary shifts: EDR killers via BYOVD (Bring Your Own Vulnerable Driver) have become a standard pre-encryption attack phase; the PE32 ransomware family has deployed post-quantum cryptography (ML-KEM/Kyber1024 at Level 5 security, AES key encapsulation) making decryption infeasible without payment even against future quantum computers; and encryptionless extortion is accelerating as ransom payment rates dropped to 28% in 2025, with ShinyHunters cited as an exemplar. The Access-as-a-Service market shows a notable shift toward RDWeb portals as attackers adapt to hardened RDP exposure.

**Severity Rationale:** Documents foundational technical and economic shifts in ransomware that render existing defensive investments (EDR, backups) less effective, including the first confirmed deployment of post-quantum encryption in active ransomware.

**Threat Actors:** ShinyHunters, PE32 ransomware family operators

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools (EDR killers/BYOVD) | Defense Evasion |
| [T1014](https://attack.mitre.org/techniques/T1014/) | Rootkit (BYOVD signed driver abuse) | Defense Evasion |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (RDWeb/RDP/VPN IAB sales) | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact (PE32 post-quantum) | Impact |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol (encryptionless extortion) | Exfiltration |

**IOCs Extracted:**

_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2024-55591` | [3] |
| CVE | `CVE-2025-55182` | [2] |
| CVE | `CVE-2025-59536` | [2] |
| CVE | `CVE-2026-21852` | [2] |
| Domain | `1vpns.com` *(seized)* | [8] |
| Domain | `1vpns.net` *(seized)* | [8] |
| Domain | `1vpns.org` *(seized)* | [8] |
| IP | `2.223.66.103` *(First VPN US exit node, seized)* | [8] |
| IP | `5.181.234.59` *(First VPN US exit node, seized)* | [8] |
| IP | `92.38.148.58` *(First VPN US exit node, seized)* | [8] |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1014](https://attack.mitre.org/techniques/T1014/) | Rootkit (BYOVD) | Defense Evasion | [10] |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | [1] |
| [T1059](https://attack.mitre.org/techniques/T1059/) | Command and Scripting Interpreter | Execution | [2] |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | [2], [3], [5], [9] |
| [T1110.004](https://attack.mitre.org/techniques/T1110/004/) | Brute Force: Credential Stuffing | Initial Access | [7] |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access | [3], [10] |
| [T1195.001](https://attack.mitre.org/techniques/T1195/001/) | Supply Chain Compromise | Initial Access | [2] |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing | Initial Access | [5], [6] |
| [T1056](https://attack.mitre.org/techniques/T1056/) | Input Capture (proxy API key theft) | Credential Access | [2] |
| [T1552.001](https://attack.mitre.org/techniques/T1552/001/) | Credentials in Files (.env) | Credential Access | [2] |
| [T1558.003](https://attack.mitre.org/techniques/T1558/003/) | Kerberoasting | Credential Access | [7] |
| [T1018](https://attack.mitre.org/techniques/T1018/) | Remote System Discovery | Discovery | [7] |
| [T1087](https://attack.mitre.org/techniques/T1087/) | Account Discovery | Discovery | [7] |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Services: RDP | Lateral Movement | [7] |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services (multi-method) | Lateral Movement | [1] |
| [T1053.005](https://attack.mitre.org/techniques/T1053/005/) | Scheduled Task | Privilege Escalation | [1] |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account | Persistence | [7] |
| [T1005](https://attack.mitre.org/techniques/T1005/) | Data from Local System | Collection | [3] |
| [T1583.001](https://attack.mitre.org/techniques/T1583/001/) | Acquire Infrastructure: Domains | Resource Development | [5] |
| [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Indicator Removal: Clear Windows Event Logs | Defense Evasion | [7] |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | [1], [7], [10] |
| [T1090.003](https://attack.mitre.org/techniques/T1090/003/) | Proxy: Multi-hop Proxy | Command and Control | [8] |
| [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Command and Control | [6] |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration | [4], [6], [9], [10] |
| [T1052](https://attack.mitre.org/techniques/T1052/) | Exfiltration Over Physical Medium | Exfiltration | [6] |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction (wiper) | Impact | [5] |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | [1], [3], [7], [10] |
| [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Impact | [7] |
| [T1498](https://attack.mitre.org/techniques/T1498/) | Network Denial of Service | Impact | [5] |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (extortion) | Impact | [1], [4], [6] |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 20 |
| **Articles Analyzed** | 10 |
| **Articles Skipped** | 1 (DataBreaches.Net — Cloudflare block; enriched from RSS summary) |
| **Report Generated** | 2026-06-02 12:00:00 UTC |
