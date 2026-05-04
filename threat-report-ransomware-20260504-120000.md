# Threat Intelligence Report: Ransomware

**Generated:** 2026-05-04 12:00:00 UTC  
**Search Term:** `ransomware`  
**Date Range:** 2026-04-28 → 2026-05-04  
**Articles Analyzed:** 8  
**Sources:** BleepingComputer, The Hacker News, DataBreaches.Net, darkreading, Check Point Research

---

## Executive Summary

The ransomware landscape between April 28 and May 4, 2026 is dominated by two distinct but equally significant storylines. First, VECT 2.0 — a new multi-platform RaaS — contains a catastrophic cryptographic design flaw that renders it a data wiper rather than recoverable ransomware for any file above 131KB, while simultaneously scaling its affiliate distribution through an unprecedented supply-chain and dark-web-forum alliance with TeamPCP and BreachForums. Second, a critical authentication bypass in cPanel/WHM (CVE-2026-41940) is being mass-exploited to deploy "Sorry" ransomware against Linux web servers, with 44,000+ hosts already compromised in what began as a zero-day in late February. On the law enforcement front, the DOJ secured four-year prison sentences for two cybersecurity insiders who facilitated ALPHV/BlackCat attacks, while a German national behind the Versus Project dark web marketplace was extradited from Colombia. A separate internecine conflict between RaaS groups 0APT and KryBit exposed both operators' infrastructure, providing defenders with actionable intelligence on RaaS operational models. Across all articles, the defining pattern is the industrialization of ransomware delivery: supply chains, open affiliate programs, and dark web forum partnerships are lowering the barrier to entry while simultaneously amplifying reach.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 1 |
| 🟠 High | 3 |
| 🟡 Medium | 2 |
| 🟢 Low | 2 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2026-41940` | Articles 1 | Critical auth bypass enabling mass ransomware deployment against cPanel/WHM infrastructure |

### Shared Threat Actors

#### VECT / TeamPCP
- **Seen in:** Articles 5, 7, 8
- **Activity:** VECT 2.0 RaaS partnered with TeamPCP supply-chain attackers to target downstream victims of the Trivy, Checkmarx KICS, LiteLLM, and Telnyx compromises. All three articles confirm the same wiper-behavior flaw and affiliate distribution model, with Check Point providing the deepest technical analysis. VECT is assessed as a novice operation with ambitious reach but severe technical deficiencies.

#### ALPHV / BlackCat
- **Seen in:** Articles 2, 3
- **Activity:** Two U.S.-based cybersecurity professionals (Goldberg/Martin) were sentenced for deploying ALPHV/BlackCat in 2023, confirming the group's RaaS infrastructure enabled insider-threat-class affiliates. While BlackCat itself no longer operates, the sentencing signals ongoing DOJ prioritization of RaaS affiliate prosecution.

### Campaign Threads

#### VECT 2.0 Wiper-Ransomware: Multi-Platform RaaS with Supply-Chain Delivery
- **Articles:** 5, 7, 8
- **Description:** Three independent sources (Dark Reading, The Hacker News, Check Point Research) report on the same VECT 2.0 campaign, confirming the group's catastrophic nonce-handling flaw across Windows, Linux, and ESXi. The Check Point deep-dive provides the technical root cause; Dark Reading and THN provide context on the TeamPCP partnership and sectoral targeting. Organizations in manufacturing, healthcare, education, and technology are at elevated risk, particularly those running third-party tools compromised in the TeamPCP supply-chain attacks (Trivy, Checkmarx KICS, LiteLLM, Telnyx).
- **Timeline:** Dec 2025: VECT launches on Russian-language forum → Jan 2026: First two victims claimed → Feb 2026: VECT 2.0 released with multi-platform support → Mar 2026: TeamPCP supply-chain attacks inject malware into Trivy/KICS/LiteLLM/Telnyx → Apr 2026: VECT announces TeamPCP and BreachForums partnerships → Apr 28, 2026: Check Point/THN/Dark Reading publish wiper-flaw analysis

#### DOJ Cybercrime Enforcement Day (April 30, 2026)
- **Articles:** 2, 3, 4
- **Description:** On April 30, 2026, the DOJ announced three simultaneous cybercrime enforcement actions: sentencing of Goldberg and Martin for BlackCat attacks, confirmation of Martino's guilty plea for the same conspiracy, and extradition of the Versus Project operator from Colombia. This coordinated enforcement day represents a deliberate public signal against ransomware operators and dark web marketplace operators alike.
- **Timeline:** Apr–Dec 2023: BlackCat attacks by Goldberg/Martin/Martino → Dec 2025: Guilty pleas entered → Apr 30, 2026: Goldberg and Martin sentenced; Versus Project operator extradited

### Emerging Patterns

- **Supply-Chain-to-Ransomware Delivery Pipeline:** VECT's formal partnership with TeamPCP represents the first confirmed case of a RaaS group structurally integrating a supply-chain attack actor as a primary distribution channel. TeamPCP's compromise of widely used developer tools (Trivy, Checkmarx KICS, LiteLLM, Telnyx) created a pre-seeded victim pool for VECT affiliates. Defenders should treat any organization using these tools as potentially pre-compromised.

- **Open-Affiliate RaaS Democratization:** VECT's BreachForums partnership — extending affiliate access to every registered forum user — marks an escalation in affiliate recruitment beyond reputation-gating or fee models. Combined with a $250 Monero entry fee (waived for CIS countries), this model dramatically lowers barriers and increases the pool of potential operators. KryBit's 80/20 affiliate model reflects the same trend toward commoditizing ransomware deployment.

- **Ransomware-as-Wiper Convergence:** Both VECT 2.0 (by design flaw) and the Sorry ransomware (RSA-2048 key non-recovery) represent cases where paying the ransom does not guarantee file recovery. Defenders should operationally treat any ransomware incident as a potential data-destruction event and prioritize immutable offline backup testing over negotiation readiness.

- **Cybersecurity Insider Threat Vector:** The BlackCat sentencing reveals that ransomware affiliates include credentialed cybersecurity professionals with deep institutional knowledge — IR managers and crypto brokers who used victim engagement access to maximize extortion. Martino's sharing of insurance policy limits represents a previously under-documented RaaS enrichment tactic.

- **Inter-Gang Intelligence Windfall:** The 0APT vs. KryBit feud exposed full operational data including admin counts, affiliate rosters, ransom demand ranges, and PHP source code for both groups. This represents a rare, actionable intelligence opportunity for defenders to build detection logic around KryBit's confirmed TTPs before the group reconstitutes.

---

## Article Analysis

---

### [1] Critrical cPanel Flaw Mass-Exploited in "Sorry" Ransomware Attacks

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | 2026-05-02 17:54 UTC |
| **Severity** | 🔴 Critical |
| **URL** | [bleepingcomputer.com/news/security/critrical-cpanel-flaw…](https://www.bleepingcomputer.com/news/security/critrical-cpanel-flaw-mass-exploited-in-sorry-ransomware-attacks/) |

**Summary:** CVE-2026-41940, a critical authentication bypass in cPanel/WHM, is being mass-exploited to deploy 'Sorry' ransomware against Linux web servers. The Go-based encryptor uses ChaCha20 with RSA-2048 key protection and appends the `.sorry` extension; at least 44,000 servers have been compromised. Decryption is mathematically impossible without the attacker's RSA-2048 private key, making recovery contingent solely on backups.

**Severity Rationale:** Active mass exploitation of a critical zero-day with confirmed ransomware deployment across 44,000+ hosts and no viable decryption path.

**Threat Actors:** Sorry

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1491](https://attack.mitre.org/techniques/T1491/) | Defacement | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-41940
- **URLs:** _none_

---

### [2] VECT 2.0 Ransomware Irreversibly Destroys Files Over 131KB on Windows, Linux, ESXi

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-04-28 14:01 UTC |
| **Severity** | 🟠 High |
| **URL** | [thehackernews.com/2026/04/vect-20-ransomware-irreversibly…](https://thehackernews.com/2026/04/vect-20-ransomware-irreversibly.html) |

**Summary:** Check Point Research confirms VECT 2.0 permanently destroys files over 131KB due to a nonce-handling flaw in its ChaCha20-IETF implementation across Windows, Linux, and ESXi variants. The group partnered with TeamPCP (supply-chain attacks on Trivy, KICS, LiteLLM, Telnyx) and BreachForums (open-affiliate model) to amplify distribution. The Windows variant uses safe-mode persistence via registry modification and anti-analysis targeting 44 security tools; the ESXi variant applies CIS-country geofencing and SSH lateral movement.

**Severity Rationale:** Active multi-platform RaaS with supply-chain distribution, confirmed data-destruction behavior, and a broad affiliate program, though technical immaturity limits current scale.

**Threat Actors:** VECT, TeamPCP

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact |
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access |
| [T1112](https://attack.mitre.org/techniques/T1112/) | Modify Registry | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

---

### [3] VECT: Ransomware by Design, Wiper by Accident

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | 2026-04-28 13:03 UTC |
| **Severity** | 🟠 High |
| **URL** | [research.checkpoint.com/2026/vect-ransomware-by-design-wiper-by-accident/](https://research.checkpoint.com/2026/vect-ransomware-by-design-wiper-by-accident/) |

**Summary:** Check Point Research's deep technical analysis confirms a fundamental nonce-discard bug in libsodium-based ChaCha20-IETF across all three VECT 2.0 platform variants, rendering 75% of every large file permanently unrecoverable by anyone including the attacker. Additional bugs include self-cancelling string obfuscation, unreachable anti-analysis code, and silently ignored encryption mode flags, pointing to amateur developers possibly using AI-generated code. The VECT–TeamPCP–BreachForums alliance creates a supply-chain-fed, mass-affiliate ransomware delivery model unprecedented in scope.

**Severity Rationale:** Deep technical validation of wiper-level impact with multi-platform coverage, confirmed supply-chain delivery, and broad affiliate distribution via BreachForums.

**Threat Actors:** VECT, TeamPCP

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact |
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Compromise Software Supply Chain | Initial Access |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion |
| [T1021.004](https://attack.mitre.org/techniques/T1021/004/) | Remote Services: SSH | Lateral Movement |
| [T1112](https://attack.mitre.org/techniques/T1112/) | Modify Registry | Defense Evasion |

**IOCs Extracted:**
_No IOCs extracted._

---

### [4] Vect 2.0 Ransomware Acts as Wiper, Thanks to Design Error

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-04-29 15:23 UTC |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/threat-intelligence/vect-ransomware-wiper-design-error](https://www.darkreading.com/threat-intelligence/vect-ransomware-wiper-design-error) |

**Summary:** Dark Reading's coverage of VECT 2.0 emphasizes the real-world impact for targeted sectors — manufacturing, education, healthcare, and technology — and the compounding risk from the TeamPCP supply-chain partnership. Check Point's Eli Smadja is cited confirming that paying the ransom is not a recovery strategy and that victims who pay receive nothing back. The article underscores that organizations relying on compromised developer tools (Trivy, KICS, LiteLLM, Telnyx) face a confirmed supply-chain entry vector.

**Severity Rationale:** Active RaaS with confirmed victims, supply-chain distribution vector, and a design flaw guaranteeing permanent data destruction even after ransom payment.

**Threat Actors:** VECT, TeamPCP

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact |
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access |
| [T1562](https://attack.mitre.org/techniques/T1562/) | Impair Defenses | Defense Evasion |

**IOCs Extracted:**
_No IOCs extracted._

---

### [5] Feuding Ransomware Groups Leak Each Other's Data

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-04-28 20:13 UTC |
| **Severity** | 🟡 Medium |
| **URL** | [darkreading.com/threat-intelligence/feuding-ransomware-groups-leak-data](https://www.darkreading.com/threat-intelligence/feuding-ransomware-groups-leak-data) |

**Summary:** 0APT and KryBit, two new RaaS operations, engaged in mutual attacks that fully exposed each other's infrastructure, affiliate data, and operational details. 0APT fabricated 190+ victims to establish false credibility before attacking rivals including KryBit, Everest, and RansomHouse; KryBit retaliated by fully compromising 0APT and confirmed the fraud via leaked access logs. The feud provided defenders with rare visibility into active RaaS infrastructure, affiliate models ($40K–$100K ransom range, 80/20 split), and TTP patterns transferable to future incarnations of both groups.

**Severity Rationale:** Threat actor intelligence windfall for defenders, but KryBit and Everest remain active operational threats with confirmed victims.

**Threat Actors:** 0APT, KryBit, Everest, RansomHouse

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1530](https://attack.mitre.org/techniques/T1530/) | Data from Cloud Storage | Collection |

**IOCs Extracted:**
_No IOCs extracted._

---

### [6] Two Cybersecurity Professionals Get 4-Year Sentences in BlackCat Ransomware Attacks

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-05-01 09:56 UTC |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com/2026/05/two-cybersecurity-professionals-get-4…](https://thehackernews.com/2026/05/two-cybersecurity-professionals-get-4.html) |

**Summary:** Ryan Goldberg (Sygnia IR manager) and Kevin Martin (DigitalMint) were sentenced to four years each for deploying ALPHV/BlackCat ransomware against multiple U.S. victims in 2023, successfully extorting one victim for $1.2M in Bitcoin. Co-conspirator Angelo Martino abused his ransomware-negotiator role to share victims' insurance policy limits with BlackCat operators, maximizing extortion payouts. The case establishes legal precedent for prosecuting cybersecurity insiders who weaponize professional access against clients.

**Severity Rationale:** Historical law enforcement action against previously concluded attacks; no active threat, with significant deterrence and insider-threat policy value.

**Threat Actors:** ALPHV, BlackCat

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [7] Two Americans Sentenced to Prison for Using BlackCat Ransomware to Attack Multiple Entities

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | 2026-04-30 22:59 UTC |
| **Severity** | 🟢 Low |
| **URL** | [databreaches.net/2026/04/30/two-americans-sentenced-to-prison…](https://databreaches.net/2026/04/30/two-americans-sentenced-to-prison-for-using-blackcat-ransomware-to-attack-multiple-entities/) |

**Summary:** DataBreaches.net covers the DOJ sentencing of Ryan Goldberg and Kevin Martin to four years each for their roles in ALPHV/BlackCat ransomware attacks targeting U.S. businesses in 2023. Both defendants agreed to pay BlackCat operators 20% of collected ransoms in exchange for access to the RaaS platform. *(Note: article content unavailable; enriched from RSS summary.)*

**Severity Rationale:** Secondary coverage of the same sentencing event as Article 6; no new threat intelligence or IOCs beyond the DOJ announcement.

**Threat Actors:** ALPHV, BlackCat

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [8] Versus Project Marketplace Creator and Operator Extradited from Colombia to the United States

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | 2026-04-30 22:57 UTC |
| **Severity** | 🟢 Low |
| **URL** | [databreaches.net/2026/04/30/versus-project-marketplace-creator…](https://databreaches.net/2026/04/30/versus-project-marketplace-creator-and-operator-extradited-from-colombia-to-the-united-states/) |

**Summary:** A German national who owned and operated 'The Versus Project' dark web marketplace has been extradited from Colombia to the United States. The marketplace facilitated the sale of drugs, stolen financial data, hacking tools, and ransomware-related transactions. The extradition occurred on the same day as the BlackCat sentencing, reflecting coordinated DOJ cybercrime enforcement. *(Note: article content unavailable; enriched from RSS summary.)*

**Severity Rationale:** Law enforcement/extradition news about a now-disrupted marketplace; no active threat indicators or ongoing campaign.

**Threat Actors:** Versus Project

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2026-41940` | [1] |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | [1] |
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access | [2], [4] |
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Compromise Software Supply Chain | Initial Access | [3] |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | [3] |
| [T1112](https://attack.mitre.org/techniques/T1112/) | Modify Registry | Defense Evasion | [2], [3] |
| [T1562](https://attack.mitre.org/techniques/T1562/) | Impair Defenses | Defense Evasion | [4] |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | Defense Evasion | [2] |
| [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | Lateral Movement | [2] |
| [T1021.004](https://attack.mitre.org/techniques/T1021/004/) | Remote Services: SSH | Lateral Movement | [3] |
| [T1530](https://attack.mitre.org/techniques/T1530/) | Data from Cloud Storage | Collection | [5] |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact | [2], [3], [4] |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | [1], [2], [3], [4], [5], [6], [7] |
| [T1491](https://attack.mitre.org/techniques/T1491/) | Defacement | Impact | [1] |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Impact | [6] |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 8 |
| **Articles Analyzed** | 8 |
| **Articles Skipped** | 2 (DataBreaches.Net — Cloudflare WAF; fell back to RSS summary) |
| **Report Generated** | 2026-05-04 12:00:00 UTC |
