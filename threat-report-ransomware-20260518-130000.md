# Threat Intelligence Report: Ransomware

**Generated:** 2026-05-18 13:00:00 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-05-12 → 2026-05-18
**Articles Analyzed:** 13
**Sources:** SecurityWeek, Rapid7 Cybersecurity Blog, darkreading, Cybersecurity Dive, DataBreaches.Net, Check Point Research, Securelist, BankInfoSecurity

---

## Executive Summary

The May 12–18, 2026 ransomware landscape reveals a sector in the midst of both tactical maturation and structural escalation. Nitrogen ransomware's attack on Foxconn—the world's largest electronics manufacturer—marks a deliberate upmarket shift from the group's typical mid-market supply chain targeting, creating double-extortion leverage over Apple, Nvidia, Google, and other Fortune 500 customers via 8TB of stolen engineering schematics. Simultaneously, The Gentlemen RaaS operation—currently the second most active group globally with 332 published victims in just five months—suffered an internal database breach that provides rare public visibility into their full operational stack, including CVE exploitation priorities (CVE-2024-55591, CVE-2025-32433, CVE-2025-33073), affiliate TOX IDs, and live negotiation transcripts. A structural shift continues to gather momentum: encryptionless extortion, exemplified by ShinyHunters' 275-million-user Canvas breach and Kaspersky's state-of-ransomware analysis, renders backup-based recovery strategies largely ineffective against a growing share of attacks. Identity compromise remains the dominant ransomware entry point—two-thirds of attacks now begin with an identity-related breach—while BYOVD-based EDR killers have become a normalized pre-deployment step across multiple tracked groups including Nitrogen and The Gentlemen. Security teams should treat edge device patching (Fortinet, Cisco SD-WAN), identity credential hygiene, and BYOVD detection as immediate priorities.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 3 |
| 🟠 High | 7 |
| 🟡 Medium | 1 |
| 🟢 Low | 2 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| CVE | `CVE-2023-52271` | Articles 0, 2 | Topaz Antifraud BYOVD driver exploited by Nitrogen in Foxconn attack; confirmed across both independent sources covering same incident |
| CVE | `CVE-2024-55591` | Article 1 | Fortinet edge appliance CVE actively tracked by The Gentlemen for initial access—leaked internal chats confirm operational prioritization |
| CVE | `CVE-2025-32433` | Article 1 | Listed in The Gentlemen's internal CVE watchlist for exploitation; suggests near-term weaponization |
| CVE | `CVE-2025-33073` | Article 1 | Listed in The Gentlemen's internal CVE watchlist alongside CVE-2025-32433; active evaluation underway |
| CVE | `CVE-2026-20182` | Article 4 | CVSS 10.0 Cisco SD-WAN auth bypass explicitly flagged as ransomware pivot vector; actively exploited variant CVE-2026-20127 also in the wild |

### Shared Threat Actors

#### Nitrogen
- **Seen in:** Articles 0, 2
- **Activity:** Two independent sources (Dark Reading and Cybersecurity Dive) confirm Nitrogen's attack on Foxconn North American facilities, with 11 million files (8TB) stolen including schematics tied to Apple, Google, Intel, and Nvidia. Nitrogen uses SEO poisoning and fake software installers for initial access, and BYOVD via CVE-2023-52271 for EDR bypass. The group's compromise of a globally critical supply chain hub represents an escalation beyond their documented mid-market targeting pattern.

#### The Gentlemen
- **Seen in:** Articles 1, 6
- **Activity:** Check Point Research and Dark Reading both analyze the May 4, 2026 breach of The Gentlemen's internal Rocket database. The 16GB leak includes affiliate communications, tooling, CVE watchlists, ransom negotiation transcripts (including a confirmed $190K payment), and 8 unique affiliate TOX IDs. The group is confirmed as the second most active RaaS operation in 2026 with 332+ published victims, using a 90/10 payout model to attract experienced affiliates.

#### ShinyHunters
- **Seen in:** Articles 8, 9
- **Activity:** ShinyHunters breached Instructure's Canvas LMS twice within two weeks (April 29 and May 7), stealing 3.65TB covering 275 million users across 9,000 schools. Kaspersky's state-of-ransomware report cites ShinyHunters as a leading example of the emerging encryptionless extortion model—data theft without encryption is increasingly the primary leverage mechanism, bypassing the defensive value of backups entirely.

### Campaign Threads

#### Foxconn / Nitrogen North American Manufacturing Breach
- **Articles:** 0, 2
- **Description:** Nitrogen ransomware claimed responsibility for a major breach of Foxconn's North American facilities, exfiltrating more than 11 million files (8TB) containing confidential engineering schematics, manufacturing process documents, and financial records tied to Apple, Google, Intel, Nvidia, AMD, JPMorgan Chase, and others. Foxconn confirmed the attack and activated containment procedures; as of May 14 the company was listed on Nitrogen's onion leak site, indicating negotiations were ongoing or payment had been refused. Nitrogen's typical SEO poisoning / fake installer initial access vector was cited, combined with BYOVD via CVE-2023-52271 for EDR bypass.
- **Timeline:** Mid-May 2026: Nitrogen claims breach → Foxconn confirms cyberattack (May 13) → Foxconn listed on Nitrogen leak site → Operations at affected facilities resuming (May 14)

#### The Gentlemen Internal Database Breach and Exposure
- **Articles:** 1, 6
- **Description:** On or just before May 4, 2026, an anonymous group breached The Gentlemen's internal backend (Rocket database), leaking 44MB of a 16GB trove of internal communications, tooling, affiliate IDs, and negotiation transcripts. Two distinct intelligence teams—Check Point Research and Dark Reading/Eli Smadja—independently analyzed the leak, revealing the group's CVE watchlist (Fortinet/Cisco edge devices), NTLM relay tactics, M365 credential harvesting, and a rare successful negotiation transcript showing a $190K ransom paid. The leak also exposed a dual-pressure tactic: data stolen from a UK consultancy was reused to coerce a Turkish victim.
- **Timeline:** May 4: Leak announced → Check Point Research obtains sample → Internal chats published → Dark Reading reports operational structure (May 13)

#### Instructure / Canvas Ransomware Payment
- **Articles:** 8, 11
- **Description:** ShinyHunters twice infiltrated Instructure's Canvas LMS platform (April 29 and May 7), stealing 3.65TB of data across 275 million users and 9,000 schools worldwide. Instructure reached an "agreement" with the unnamed threat actor on May 13—widely characterized by cybersecurity experts as a ransom payment—and received digital confirmation of data destruction via "shred logs." The FBI, which strongly discourages ransom payment, was not cited as involved in the decision. The ISMG editorial panel further examined the impossibility of verifying criminal data deletion commitments.

### Emerging Patterns

- **Manufacturing as the top ransomware target sector:** The Foxconn breach, West Pharmaceutical attack, and Kaspersky's report jointly document manufacturing as the most heavily targeted sector—accounting for nearly 70% more ransomware victims than the next most targeted industry and over $18B in losses in 2025 Q1–Q3 alone. Low tolerance for downtime, high-profile supply chain interdependencies, and data valuable to multiple downstream clients create multiple ransom leverage points simultaneously. *(Articles 0, 2, 5, 9)*

- **BYOVD (Bring Your Own Vulnerable Driver) normalized as pre-deployment EDR kill step:** Nitrogen's use of CVE-2023-52271, The Gentlemen's documented EDR-kill tooling, and Kaspersky's confirmation that EDR killers are now a "standard component of attack playbooks" collectively signal that BYOVD has crossed from advanced technique to commodity method. Defenders cannot rely on EDR alone as a late-stage detection control. *(Articles 0, 1, 2, 6, 9)*

- **Encryptionless extortion supplanting encryption as primary leverage:** ShinyHunters' Canvas breach and Kaspersky's analysis confirm that a growing share of ransomware operators are dropping file encryption entirely, relying on data theft and public disclosure threats. This fundamentally undermines backup-centric resilience strategies and reframes ransomware as a data-governance and regulatory liability problem, not merely a business-continuity one. *(Articles 8, 9)*

- **Identity compromise as the dominant ransomware initial access vector:** Sophos' survey of 5,000 organizations found two-thirds of ransomware attacks originate from identity-related breaches—credentials, API keys, service accounts, and OAuth tokens. The Gentlemen's confirmed use of M365/OWA credential logs and Kaspersky's documentation of IAB-supplied RDP/VPN/RDWeb access corroborate this trend at the infrastructure level. *(Articles 9, 10)*

- **RaaS operational professionalization:** The Gentlemen's exposed structure—defined C-suite-like roles, 90/10 payout splits, LLM-assisted development, and systematic CVE tracking—reflects a broader professionalization of the RaaS model that drives higher attack volume and consistency. Combined with Access-as-a-Service IAB markets, the barrier to launching sophisticated ransomware campaigns continues to fall. *(Articles 1, 6)*

---

## Article Analysis

---

### [0] Foxconn Attack Highlights Manufacturing's Cyber Crisis

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Thu, 14 May 2026 12:00:00 GMT |
| **Severity** | 🔴 Critical |
| **URL** | [darkreading.com/cyberattacks-data-breaches/foxconn-attack...](https://www.darkreading.com/cyberattacks-data-breaches/foxconn-attack-manufacturing-cyber-crisis) |

**Summary:** Nitrogen ransomware claimed responsibility for a breach of multiple Foxconn North American facilities, exfiltrating more than 11 million files (8TB) including confidential engineering schematics, manufacturing documents, and financial records tied to Apple, Intel, Google, Nvidia, AMD, JPMorgan Chase, and others. The attack is one of approximately 600 ransomware incidents targeting manufacturers in 2026 so far, with Arctic Wolf confirming manufacturing is the most heavily targeted sector—nearly 70% more victims than the next industry. Median ransomware payments in the manufacturing sector hover at $400K, with Foxconn's status on Nitrogen's active leak site suggesting negotiations remain unresolved or payment was refused.

**Severity Rationale:** Active ransomware deployment against the world's largest electronics manufacturer with confirmed 8TB exfiltration creating leverage over multiple Fortune 500 companies and sensitive engineering IP.

**Threat Actors:** Nitrogen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing / SEO Poisoning | Initial Access |
| [T1036](https://attack.mitre.org/techniques/T1036/) | Masquerading (fake software installers) | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (BYOVD) | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2023-52271
- **URLs:** _none_

---

### [1] Thus Spoke…The Gentlemen

| Field | Value |
|---|---|
| **Source** | Check Point Research |
| **Published** | Wed, 13 May 2026 13:01:01 +0000 |
| **Severity** | 🔴 Critical |
| **URL** | [research.checkpoint.com/2026/thus-spoke-the-gentlemen/](https://research.checkpoint.com/2026/thus-spoke-the-gentlemen/) |

**Summary:** Check Point Research obtained and analyzed a partial leak of The Gentlemen RaaS group's internal Rocket database, breached on May 4, 2026. The 44MB sample reveals the full operational structure: administrator zeta88 (alias hastalamuerte) builds the locker, manages infrastructure, and runs negotiations; specialists qbit and quant handle edge-device scanning and credential access respectively. Internal chats expose CVE watchlists targeting Fortinet and Cisco edge appliances (CVE-2024-55591, CVE-2025-32433, CVE-2025-33073), NTLM relay and OWA/M365 credential logging for initial access, 8 unique affiliate TOX IDs, a confirmed $190K ransom receipt (down from a $250K anchor), and a dual-pressure tactic where data from one victim was weaponized against a second. With 412 victims on the DLS and 29 confirmed campaigns in public sources, The Gentlemen is the second most productive RaaS operation in 2026.

**Severity Rationale:** Detailed real-world operational intelligence on the second most active RaaS group globally, including live CVE targets and affiliate infrastructure, creates immediate risk of copycat tactics and informs adversary emulation.

**Threat Actors:** The Gentlemen, zeta88 (hastalamuerte)

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (Fortinet/Cisco edge) | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (OWA/M365 credential logs) | Initial Access |
| [T1557](https://attack.mitre.org/techniques/T1557/) | Adversary-in-the-Middle (NTLM relay) | Credential Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (EDR killers/BYOVD) | Defense Evasion |
| [T1071](https://attack.mitre.org/techniques/T1071/) | Application Layer Protocol (SystemBC C2) | Command and Control |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** 15CE8D5DB0BAC3BCBB1FA69F2E672CC54EFBEC7684DA792F3CBF8B007A9FEA1D16374560DFA5, 2F1A9C8B8AA163BBB84FF799A0954B232C279C5E9EE42505955288EAAD28685A2BC0713C7745, 88984846080D639C9A4EC394E53BA616D550B2B3AD691942EA2CCD33AA5B9340FD1A8FF40E9A, 98C132E2B20B531BE6604397D97040C1E9EB42FCE12EDF119BCE8B4031CA5C70DAF5E65FA3C3, D2CBA43A1AF6D965432AE11487726DB84D2945CF2CD975D7774B76B54AF052418AC2E59ADA69, D527959A7BC728CB272A0DB683B547F079C98012201A48DD2792B84604E8BC29F6E6BDB8003F, F8E24C7F5B12CD69C44C73F438F65E9BF560ADF35EBBDF92CF9A9B84079F8F04060FF98D098E, F96C481CBB0D6E7BDA49C6D68CFDB1D284354961534EDEEDA854C672B48A8D6B7146F90BDACB
- **CVEs:** CVE-2024-55591, CVE-2025-32433, CVE-2025-33073
- **URLs:** _none_

---

### [2] Foxconn confirms cyberattack affecting some North American facilities

| Field | Value |
|---|---|
| **Source** | Cybersecurity Dive - Latest News |
| **Published** | Wed, 13 May 2026 11:13:44 -0400 |
| **Severity** | 🔴 Critical |
| **URL** | [cybersecuritydive.com/news/foxconn-confirms-cyberattack.../820120/](https://www.cybersecuritydive.com/news/foxconn-confirms-cyberattack-affecting-some-north-american-facilities/820120/) |

**Summary:** Foxconn confirmed a cyberattack by Nitrogen ransomware against its North American facilities, with threat researchers from Arctic Wolf confirming claims of 11 million stolen files (8TB) including schematics from third-party technology clients. Nitrogen is described as a double-extortion group that emerged in September 2024, typically targeting mid-sized supply chain companies—making the Foxconn attack an unusually high-profile escalation. A specific BYOVD technique leveraging CVE-2023-52271 (Topaz Antifraud vulnerable driver) was used to disable antivirus tools. Nitrogen is noted to have originally used AlphV ransomware in 2023 before establishing its own operation.

**Severity Rationale:** Confirmed ransomware breach of the world's largest electronics manufacturer, with verified exfiltration of supply chain partner IP and confirmed BYOVD exploitation for AV bypass.

**Threat Actors:** Nitrogen

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (BYOVD via CVE-2023-52271) | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2023-52271
- **URLs:** _none_

---

### [3] American Lending Center Data Breach Affects 123,000 Individuals

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Fri, 15 May 2026 11:06:55 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/american-lending-center-data-breach...](https://www.securityweek.com/american-lending-center-data-breach-affects-123000-individuals/) |

**Summary:** American Lending Center (ALC), a California non-bank lender managing a $3B portfolio, disclosed that a ransomware attack detected in July 2025 has affected 123,000 individuals, with names, dates of birth, and SSNs potentially stolen. The investigation concluded April 8, 2026—nearly nine months after discovery. No known ransomware group has claimed credit, which may indicate a ransom was paid or the attacker does not operate a public leak site. ALC found no evidence of data misuse at time of notification.

**Severity Rationale:** Confirmed ransomware with PII exfiltration affecting 123,000 individuals at a financial institution, including sensitive identity data (SSN, DOB) sufficient for identity fraud.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |

**IOCs Extracted:**
_No IOCs extracted._

---

### [4] The Dark Side of Efficiency: When Network Controllers Become "God Mode" for Attackers

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | Thu, 14 May 2026 16:00:00 GMT |
| **Severity** | 🟠 High |
| **URL** | [rapid7.com/blog/post/tr-efficiencys-dark-side-network-controllers...](https://www.rapid7.com/blog/post/tr-efficiencys-dark-side-network-controllers-in-god-mode-attackers-sd-wan) |

**Summary:** Rapid7 researchers disclosed CVE-2026-20182 (CVSS 10.0), a maximum-severity authentication bypass in the Cisco Catalyst SD-WAN Controller that allows an unauthenticated attacker to present as a trusted network router and obtain full administrative access to the control plane. The article explicitly flags this class of vulnerability as highly attractive to ransomware groups, who can use SD-WAN controller compromise to eliminate per-host lateral movement and directly disrupt the entire enterprise network. A related CVE-2026-20127 is noted as already actively exploited in the wild. Rapid7 recommends immediate patching and network segmentation of administrative control planes.

**Severity Rationale:** CVSS 10.0 vulnerability in widely deployed enterprise networking infrastructure with an actively exploited predecessor (CVE-2026-20127), providing ransomware operators unauthenticated control-plane access.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (impersonating trusted router) | Defense Evasion |
| [T1570](https://attack.mitre.org/techniques/T1570/) | Lateral Tool Transfer (via compromised controller) | Lateral Movement |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-20182, CVE-2026-20127
- **URLs:** _none_

---

### [5] West Pharmaceutical starts restoring operations after ransomware attack

| Field | Value |
|---|---|
| **Source** | Cybersecurity Dive - Latest News |
| **Published** | Thu, 14 May 2026 10:46:36 -0400 |
| **Severity** | 🟠 High |
| **URL** | [cybersecuritydive.com/news/west-pharmaceutical-restoring.../820250/](https://www.cybersecuritydive.com/news/west-pharmaceutical-restoring-operations-ransomware-attack/820250/) |

**Summary:** West Pharmaceutical Services, a leading drug-delivery device manufacturer with annual revenues of $3.3B, disclosed a ransomware attack detected May 4 that resulted in confirmed data theft and encryption. The company took systems offline as a precaution, temporarily disrupting global operations including manufacturing, receiving, and shipping. Palo Alto Networks Unit 42 handled incident response and confirmed containment, including neutralization of malicious binaries and unauthorized persistence mechanisms. No ransomware group has been publicly identified as responsible, and full financial impact is not yet determined.

**Severity Rationale:** Confirmed ransomware with data exfiltration and encryption against a critical pharmaceutical supply chain manufacturer, causing global operational disruption and requiring enterprise-level incident response.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account (unauthorized persistence) | Persistence |

**IOCs Extracted:**
_No IOCs extracted._

---

### [6] Tables Turn on 'The Gentlemen' RaaS Gang With Data Leak

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | Wed, 13 May 2026 20:47:46 GMT |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/threat-intelligence/gentlemen-raas-gang-data-leak](https://www.darkreading.com/threat-intelligence/gentlemen-raas-gang-data-leak) |

**Summary:** An anonymous group breached The Gentlemen RaaS gang's internal backend database and is selling 16GB of stolen operational data for $10,000 in Bitcoin, with 44MB published as proof-of-life. Dark Reading's analysis of the leaked sample reveals a tight 10-person organizational structure led by "zeta88," a generous 90/10 affiliate payout model, exploitation of known edge-device CVEs, BYOVD for EDR bypass, and LLM-assisted development. With 332 published victims in the first five months of 2026, The Gentlemen is the second most productive RaaS operation globally. Analysts at Check Point assess the breach as a reputational hit but unlikely to significantly disrupt operations.

**Severity Rationale:** Operational exposure of the second most active RaaS operation globally, including TTPs, CVE watchlists, affiliate relationships, and negotiation outcomes—high intelligence value with limited operational disruption expected.

**Threat Actors:** The Gentlemen, zeta88

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (edge devices) | Initial Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (BYOVD/EDR killers) | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [7] NL: Dutch watchdog says healthcare lab failed data security rules before cyberattack affecting 850,000

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Wed, 13 May 2026 13:13:05 +0000 |
| **Severity** | 🟠 High |
| **URL** | [databreaches.net/2026/05/13/nl-dutch-watchdog...](https://databreaches.net/2026/05/13/nl-dutch-watchdog-says-healthcare-lab-failed-data-security-rules-before-cyberattack-affecting-850000/) |

**Summary:** (*RSS summary fallback — site Cloudflare-protected.*) The Dutch data protection authority found that Bevolkingsonderzoek Nederland, a public cancer screening agency, failed to meet data security requirements prior to an August 2025 attack by the Nova ransomware gang that resulted in the theft of data belonging to approximately 500,000 women who had undergone cervical cancer screening. The agency paid Nova's initial ransom demand, which Nova confirmed, but the gang subsequently demanded additional payment—reportedly because the victim had spoken with police—extending the extortion in violation of the original agreement.

**Severity Rationale:** Ransomware with double extortion against a healthcare screening agency handling highly sensitive medical data for 850,000 individuals, with confirmed ransom payment that failed to terminate the threat.

**Threat Actors:** Nova

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (double extortion) | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [8] Canvas owner reaches 'agreement' with threat actors after data breach

| Field | Value |
|---|---|
| **Source** | Cybersecurity Dive - Latest News |
| **Published** | Wed, 13 May 2026 09:41:52 -0400 |
| **Severity** | 🟠 High |
| **URL** | [cybersecuritydive.com/news/canvas-agreement-threat-actors.../820084/](https://www.cybersecuritydive.com/news/canvas-agreement-threat-actors--ransomware/820084/) |

**Summary:** Instructure, owner of the Canvas LMS used by 275 million users at 9,000 schools worldwide, confirmed it reached an "agreement" with ShinyHunters after two breaches (April 29 and May 7) resulting in 3.65TB of stolen data including usernames, email addresses, course names, and enrollment information. Cybersecurity experts characterize the agreement as a ransom payment based on the structure of the deal, where Instructure received digital "shred logs" as confirmation of data destruction—a guarantee experts note is unverifiable. Multiple class-action lawsuits have been filed, and federal cyber-coordination infrastructure that previously assisted school districts during the 2024 PowerSchool incident no longer exists, leaving states to respond independently.

**Severity Rationale:** Massive education-sector data breach affecting 275 million users with confirmed ransom payment to ShinyHunters, compounded by weakened federal incident response capacity for K-12 institutions.

**Threat Actors:** ShinyHunters

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (Free for Teachers platform) | Initial Access |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (ransom payment confirmed) | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [9] State of ransomware in 2026

| Field | Value |
|---|---|
| **Source** | Securelist |
| **Published** | Tue, 12 May 2026 07:00:04 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securelist.com/state-of-ransomware-in-2026/119761/](https://securelist.com/state-of-ransomware-in-2026/119761/) |

**Summary:** Kaspersky's International Anti-Ransomware Day report documents four major trends defining the 2026 ransomware landscape: (1) EDR killers via BYOVD are now a standard pre-deployment phase; (2) post-quantum cryptography adoption, exemplified by the PE32 ransomware family using ML-KEM/Kyber1024, is making decryption without payment infeasible even against future quantum computing; (3) encryptionless extortion (data theft only) is growing rapidly as ransom payment rates drop to 28%; and (4) Access-as-a-Service IABs are industrializing initial access, with RDWeb portals replacing RDP as the preferred point of sale. Manufacturing alone suffered over $18B in ransomware losses in the first three quarters of 2025.

**Severity Rationale:** Annual threat landscape report documenting novel post-quantum encryption techniques and structural ecosystem shifts that have direct near-term defensive implications, including the obsolescence of backup-centric recovery strategies.

**Threat Actors:** ShinyHunters

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application (RDWeb) | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts (IAB-supplied credentials) | Initial Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (EDR killers/BYOVD) | Defense Evasion |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (encryptionless extortion) | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [10] Identity takes center stage as a leading factor in enterprise cyberattacks

| Field | Value |
|---|---|
| **Source** | Cybersecurity Dive - Latest News |
| **Published** | Tue, 12 May 2026 10:43:59 -0400 |
| **Severity** | 🟡 Medium |
| **URL** | [cybersecuritydive.com/news/identity-enterprise-cyberattacks.../819977/](https://www.cybersecuritydive.com/news/identity-enterprise-cyberattacks-ai-ransomware/819977/) |

**Summary:** A Sophos survey of 5,000 IT and cybersecurity leaders across 17 countries found that 70% suffered at least one identity-related breach in the past year, and two-thirds of ransomware victims traced the attack origin to an identity compromise. Mean ransomware recovery cost was $1.64M, with median at $750K. Only 24% of organizations regularly monitor for unusual logins, and fewer than one-third rotate non-human credentials regularly. Oil and gas, utilities, and government agencies reported the highest breach rates by sector.

**Severity Rationale:** Threat intelligence survey report without active exploitation disclosure; high analytical value for understanding the dominant ransomware initial access vector but no immediate incident to contain.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
| ID | Technique | Tactic |
|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1550](https://attack.mitre.org/techniques/T1550/) | Use Alternate Authentication Material | Defense Evasion |
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access |

**IOCs Extracted:**
_No IOCs extracted._

---

### [11] ISMG Editors: Should We Trust Ransomware Gangs?

| Field | Value |
|---|---|
| **Source** | BankInfoSecurity.com RSS Syndication |
| **Published** | 2026-05-15 (date within date range; exact time unknown) |
| **Severity** | 🟢 Low |
| **URL** | [bankinfosecurity.com/ismg-editors-should-we-trust-ransomware-gangs-a-31704](https://www.bankinfosecurity.com/ismg-editors-should-we-trust-ransomware-gangs-a-31704) |

**Summary:** ISMG's editorial panel discusses the Instructure/Canvas ransomware payment and whether organizations can trust criminal promises to delete stolen data—concluding that verification is impossible. The panel also addresses AI-accelerated attack timelines outpacing human defenders and real-time payment fraud implications. No new technical intelligence is disclosed; the discussion centers on the ethical and policy dimensions of ransom payment decisions and the structural limitations of post-payment assurances.

**Severity Rationale:** Informational editorial discussion without novel threat intelligence; analysis focuses on policy implications of an existing incident already documented in Article 8.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

### [12] How Rapid7 is bringing Cyber GRC closer to security operations

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | Tue, 12 May 2026 13:17:51 GMT |
| **Severity** | 🟢 Low |
| **URL** | [rapid7.com/blog/post/cds-rapid7-cyber-grc-secops-compliance](https://www.rapid7.com/blog/post/cds-rapid7-cyber-grc-secops-compliance) |

**Summary:** Rapid7 announced the launch of Cyber GRC, a governance, risk, and compliance product that integrates with its Command Platform. The article references contextual ransomware statistics (44% of breaches involve ransomware, up 37% year-over-year; supply chain breaches doubled to 30% of incidents; median zero days to mass exploitation for critical CVEs), but these are cited to support a product announcement rather than document a new incident. No new threat intelligence is disclosed.

**Severity Rationale:** Vendor product launch blog with supporting industry statistics; informational only, no active threat or incident disclosed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2023-52271` | 0, 2 |
| CVE | `CVE-2024-55591` | 1 |
| CVE | `CVE-2025-32433` | 1 |
| CVE | `CVE-2025-33073` | 1 |
| CVE | `CVE-2026-20127` | 4 |
| CVE | `CVE-2026-20182` | 4 |
| Hash (TOX ID) | `15CE8D5DB0BAC3BCBB1FA69F2E672CC54EFBEC7684DA792F3CBF8B007A9FEA1D16374560DFA5` | 1 |
| Hash (TOX ID) | `2F1A9C8B8AA163BBB84FF799A0954B232C279C5E9EE42505955288EAAD28685A2BC0713C7745` | 1 |
| Hash (TOX ID) | `88984846080D639C9A4EC394E53BA616D550B2B3AD691942EA2CCD33AA5B9340FD1A8FF40E9A` | 1 |
| Hash (TOX ID) | `98C132E2B20B531BE6604397D97040C1E9EB42FCE12EDF119BCE8B4031CA5C70DAF5E65FA3C3` | 1 |
| Hash (TOX ID) | `D2CBA43A1AF6D965432AE11487726DB84D2945CF2CD975D7774B76B54AF052418AC2E59ADA69` | 1 |
| Hash (TOX ID) | `D527959A7BC728CB272A0DB683B547F079C98012201A48DD2792B84604E8BC29F6E6BDB8003F` | 1 |
| Hash (TOX ID) | `F8E24C7F5B12CD69C44C73F438F65E9BF560ADF35EBBDF92CF9A9B84079F8F04060FF98D098E` | 1 |
| Hash (TOX ID) | `F96C481CBB0D6E7BDA49C6D68CFDB1D284354961534EDEEDA854C672B48A8D6B7146F90BDACB` | 1 |

> **Note:** Hashes listed are TOX IDs (cryptographic identifiers for the TOX messaging protocol) for The Gentlemen affiliate accounts, not file hashes. Treat as infrastructure identifiers, not malware signatures.

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Credential Access / Initial Access | 1, 4, 9, 10 |
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access | 10 |
| [T1550](https://attack.mitre.org/techniques/T1550/) | Use Alternate Authentication Material | Defense Evasion | 10 |
| [T1557](https://attack.mitre.org/techniques/T1557/) | Adversary-in-the-Middle (NTLM relay) | Defense Evasion | 1 |
| [T1036](https://attack.mitre.org/techniques/T1036/) | Masquerading | Defense Evasion | 0 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools (BYOVD/EDR killers) | Defense Evasion | 0, 1, 2, 6, 9 |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration | 0, 1, 2, 3, 5, 8 |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 1, 4, 6, 8, 9 |
| [T1195](https://attack.mitre.org/techniques/T1195/) | Supply Chain Compromise | Initial Access | 0, 2 |
| [T1566](https://attack.mitre.org/techniques/T1566/) | Phishing / SEO Poisoning | Initial Access | 0 |
| [T1071](https://attack.mitre.org/techniques/T1071/) | Application Layer Protocol (C2) | Command and Control | 1 |
| [T1136](https://attack.mitre.org/techniques/T1136/) | Create Account | Persistence | 5 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 0, 1, 2, 3, 5, 6, 7, 9 |
| [T1570](https://attack.mitre.org/techniques/T1570/) | Lateral Tool Transfer | Lateral Movement | 4 |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft (extortion) | Impact | 7, 8, 9 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 13 |
| **Articles Analyzed** | 13 |
| **Articles Skipped** | 1 (DataBreaches.Net — Cloudflare-protected; RSS summary used) |
| **Report Generated** | 2026-05-18 13:00:00 UTC |
