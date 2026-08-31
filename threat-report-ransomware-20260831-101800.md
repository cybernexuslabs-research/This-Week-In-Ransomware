# Threat Intelligence Report: ransomware

**Generated:** 2026-08-31 10:18:00 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-08-25 → 2026-08-31
**Articles Analyzed:** 6
**Sources:** SecurityWeek, DataBreaches.Net, Rapid7 Cybersecurity Blog, Securelist

---

## Executive Summary

The past week's ransomware activity is dominated by data-extortion pressure rather than confirmed mass encryption events, with Rhysida, Qilin, PEAR, LockBit, and Akira all leveraging leak-site shaming against victims spanning government (Berlin, U.S. ATF), healthcare (South Plains Rural Health Services), financial services (U.S. Bancorp via a fourth-party provider), benefits administration (Paylogix), and critical infrastructure (Manchester Airports Group). Notably, two government/law-enforcement entities — Berlin's city government and the U.S. ATF — were both added to ransomware leak sites within days of each other, and both Berlin and Manchester Airports Group publicly refused ransom demands, reinforcing a broader public-sector non-payment trend despite large-scale exfiltration claims. Separately, the actively exploited PaperCut NG/MF authentication-bypass-to-RCE chain (CVE-2026-81578 / CVE-2026-82078) is a high-priority initial-access vector to monitor, given ransomware operators' documented history of weaponizing the prior PaperCut flaw (CVE-2023-27350) within weeks of disclosure. No shared IOCs or confirmed campaign links were found across this week's articles, suggesting these are independent, opportunistic operations by distinct actors rather than one coordinated campaign.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 1 |
| 🟠 High | 4 |
| 🟡 Medium | 0 |
| 🟢 Low | 1 |

---

## Cross-Article Connections

### Shared IOCs
_No shared IOCs identified across articles._

### Shared Threat Actors
_No shared threat actors identified — Rhysida, PEAR, LockBit, Akira, and Qilin each appear in only one article this cycle._

### Campaign Threads
_No multi-article campaign threads identified; each incident involves a distinct actor and victim._

### Emerging Patterns

- **Government/law-enforcement targeting:** Berlin's city government (Rhysida) and the U.S. ATF (Qilin) were both added to ransomware leak sites within the same week, suggesting public-sector entities remain attractive, high-visibility targets for extortion groups seeking leverage.
- **Extortion-only leak-site pressure over confirmed encryption:** Across Rhysida, Qilin, PEAR, LockBit, and Akira, the reporting emphasizes data theft and leak-site listings rather than confirmed ransomware deployment/encryption, consistent with the broader industry shift toward exfiltration-based extortion.
- **Public-sector non-payment stance:** Both Berlin and Manchester Airports Group explicitly refused ransom demands despite claims of large-scale data theft (5.7TB and 8.7M customer records, respectively), reinforcing a "don't pay" posture among large public/quasi-public organizations.
- **Healthcare and benefits-administration data at risk:** PEAR's claimed breach of South Plains Rural Health Services and Akira's breach of benefits administrator Paylogix both exposed large volumes of health and personally identifiable information, continuing ransomware's focus on data-rich, compliance-sensitive sectors.
- **PaperCut as a recurring ransomware initial-access vector:** The newly disclosed PaperCut NG/MF authentication-bypass-to-RCE chain (CVE-2026-81578/CVE-2026-82078) echoes the 2023 PaperCut flaw (CVE-2023-27350), which was broadly exploited by ransomware affiliates — this new chain warrants close monitoring for similar adoption.

---

## Article Analysis

---

### [1] PaperCut NG/MF Critical Zero-Day Exploited in the Wild

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | Fri, 28 Aug 2026 10:09:12 GMT |
| **Severity** | 🔴 Critical |
| **URL** | [rapid7.com/blog/post/etr-papercut-ng-mf-critical-zero-day-exploited-in-the-wild](https://www.rapid7.com/blog/post/etr-papercut-ng-mf-critical-zero-day-exploited-in-the-wild) |

**Summary:** Rapid7 details active in-the-wild exploitation of a two-vulnerability exploit chain (CVE-2026-81578, CVE-2026-82078) in PaperCut NG/MF print management software that allows unauthenticated attackers to bypass authentication and achieve remote code execution via abuse of the external database connector and PaperCut's bundled Nashorn JavaScript engine. PaperCut has released two rounds of emergency patches after the first proved bypassable; the vendor's prior 2023 flaw (CVE-2023-27350) was widely exploited by ransomware operators, raising concern this new chain could see similar abuse.

**Severity Rationale:** Confirmed in-the-wild exploitation of an unauthenticated RCE (CVSSv4 9.4) in widely-deployed enterprise print management software, with a documented history of ransomware operators weaponizing prior PaperCut vulnerabilities.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript | Execution |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** CVE-2026-81578, CVE-2026-82078
- **URLs:** _none_

---

### [2] Berlin Won't Pay Extortion Group Claiming Data Theft

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Mon, 31 Aug 2026 08:49:36 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/berlin-wont-pay-extortion-group-claiming-data-theft](https://www.securityweek.com/berlin-wont-pay-extortion-group-claiming-data-theft/) |

**Summary:** The Rhysida ransomware group claimed responsibility for an August 2026 breach of Berlin's city government, alleging theft of over 5.7 terabytes of data — including personal information for 12,000+ people, financial records, IBANs, credentials, and HR/payroll files — from two Senate departments. City officials confirmed a 30 BTC (~$2.3 million) ransom demand but refused to pay, citing an ongoing law enforcement investigation.

**Severity Rationale:** Confirmed breach of a capital-city government with large-scale exfiltration of sensitive personal and financial data and a multimillion-dollar ransom demand, though impact was reportedly contained to two departments.

**Threat Actors:** Rhysida

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [3] PEAR leaks data allegedly exfiltrated from South Plains Rural Health Services while SPRHS remains silent

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | Sat, 29 Aug 2026 14:15:57 +0000 |
| **Severity** | 🟠 High |
| **URL** | [databreaches.net/2026/08/29/pear-leaks-data-allegedly-exfiltrated-from-south-plains-rural-health-services-while-sprhs-remains-silent](https://databreaches.net/2026/08/29/pear-leaks-data-allegedly-exfiltrated-from-south-plains-rural-health-services-while-sprhs-remains-silent/) |

**Summary:** The PEAR ransomware group claims to have exfiltrated approximately 1.4 TB of data from South Plains Rural Health Services (SPRHS), a nonprofit healthcare provider serving rural West Texas, including patient medical records and employee/administrative data. SPRHS has not publicly confirmed the incident, and no breach notification has appeared on the Texas Attorney General's breach site despite an alleged June 17 disclosure to the organization that would put the HIPAA/HITECH notification deadline around August 17.

**Severity Rationale:** Large claimed theft of protected health information from a healthcare provider poses significant patient privacy risk, tempered by the lack of independent confirmation from the victim.

**Threat Actors:** PEAR

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

### [4] In Other News: Log4j RCE Scare, Minimus Shutdown, Iranian Hacker Sanctions

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Fri, 28 Aug 2026 15:35:34 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/in-other-news-log4j-rce-scare-minimus-shutdown-iranian-hacker-sanctions](https://www.securityweek.com/in-other-news-log4j-rce-scare-minimus-shutdown-iranian-hacker-sanctions/) |

**Summary:** SecurityWeek's weekly roundup reports LockBit threatening to leak data tied to a U.S. Bancorp fourth-party vendor incident (the bank denies its own systems were compromised), the Akira ransomware group claiming credit for a breach of benefits administrator Paylogix that exposed Social Security, financial, and health insurance data for at least 67,789 people across three U.S. states, and a Manchester Airports Group breach affecting 8.7 million customers in which attackers demanded a ransom that MAG refused to pay.

**Severity Rationale:** Multiple concurrent ransomware/extortion incidents this week span financial services, benefits administration, and critical transportation infrastructure, with combined claimed victim counts in the millions.

**Threat Actors:** LockBit, Akira

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Impact |

**IOCs Extracted:**
_No IOCs extracted._

---

### [5] ATF Confirms Cyber Incident After Ransomware Group Claims Attack

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | Fri, 28 Aug 2026 13:59:14 +0000 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/atf-confirms-cyber-incident-after-ransomware-group-claims-attack](https://www.securityweek.com/atf-confirms-cyber-incident-after-ransomware-group-claims-attack/) |

**Summary:** The Qilin ransomware group added the U.S. Bureau of Alcohol, Tobacco, Firearms and Explosives (ATF) to its Tor leak site on August 26, 2026, though it has not yet published proof or specifics of stolen data. ATF confirmed a cyber incident affecting a standalone system disconnected from its enterprise network, designating it a "major incident" under federal guidelines while stating core operations, including its eForms system, were unaffected.

**Severity Rationale:** A ransomware group publicly claimed compromise of a U.S. federal law enforcement agency, triggering a formal "major incident" designation, though ATF states the affected system was isolated from its core network and no data has yet been leaked as proof.

**Threat Actors:** Qilin, Agenda

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration |

**IOCs Extracted:**
_No IOCs extracted._

---

### [6] Threat landscape for industrial automation systems. Q2 2026

| Field | Value |
|---|---|
| **Source** | Securelist |
| **Published** | Thu, 27 Aug 2026 10:05:43 +0000 |
| **Severity** | 🟢 Low |
| **URL** | [securelist.com/industrial-threat-report-q2-2026/121159](https://securelist.com/industrial-threat-report-q2-2026/121159/) |

**Summary:** Kaspersky's Q2 2026 industrial threat report shows the overall percentage of ICS computers with blocked malicious objects fell to 19.15%, the lowest level since 2022, though ransomware detections ticked up slightly to 0.16% after three consecutive quarters of decline. The biometrics sector led across most threat categories, including ransomware, reflecting its combination of internet exposure, heavy email use, and minimal cybersecurity controls.

**Severity Rationale:** Aggregate statistical trend reporting with no named incident, victim, or active campaign — informational for OT/ICS risk awareness rather than actionable on its own.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**
_No techniques mapped._

**IOCs Extracted:**
_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2026-81578` | Article 1 |
| CVE | `CVE-2026-82078` | Article 1 |

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 1, 5 |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript | Execution | 1 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 5 |
| [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Impact | 2, 4 |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration | 5 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 (3 failed to parse: BleepingComputer 403, Mandiant XML error, BankInfoSecurity 403) |
| **Articles Retrieved** | 6 |
| **Articles Analyzed** | 6 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-08-31 10:18:00 UTC |
