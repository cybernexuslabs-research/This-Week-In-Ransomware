# This Week In Ransomware

> A curated weekly digest of ransomware news, incidents, threat actor activity, newly discovered variants, vulnerabilities exploited in the wild, and defensive resources — tracking the evolving ransomware landscape.

---

## Overview

**This Week In Ransomware** is an automated threat intelligence repository that publishes weekly Markdown reports on the ransomware ecosystem. Each report is AI-generated from live threat intelligence feeds, synthesizing articles from leading cybersecurity sources into a structured, analyst-ready digest.

Reports cover:

- **Incidents & Campaigns** — Active ransomware operations, victim disclosures, and attack chain breakdowns
- **Threat Actors** — Group activity, infrastructure exposures, and TTP evolution
- **New Variants** — Emerging ransomware families and notable tooling updates
- **Exploited Vulnerabilities** — CVEs being actively weaponized in ransomware intrusions, including zero-days
- **Cross-Article Connections** — Shared IOCs, overlapping actors, and corroborated campaign threads across multiple sources
- **Defensive Resources** — CISA advisories, patch guidance, and detection opportunities

---

## Report Structure

Each weekly report follows a consistent format:

| Section | Description |
|---|---|
| Executive Summary | High-signal narrative of the week's dominant themes |
| Severity Distribution | Count of critical / high / medium / low findings |
| Cross-Article Connections | Shared IOCs, threat actors, and campaign threads across sources |
| Article Summaries | Per-article analysis with IOCs, MITRE ATT&CK techniques, and severity scores |
| Full IOC List | Consolidated indicators of compromise (IPs, domains, hashes, CVEs) |
| MITRE ATT&CK Coverage | Techniques observed across all analyzed articles |
| Threat Actor Index | All actors mentioned, with cross-article context |

---

## Sources

Reports aggregate and analyze content from the following RSS feeds, spanning news outlets, vendor research blogs, and vulnerability intelligence sources:

**News & Analysis**
- [Bleeping Computer](https://www.bleepingcomputer.com/)
- [The Hacker News](https://thehackernews.com/)
- [Dark Reading](https://www.darkreading.com/)
- [SecurityWeek](https://www.securityweek.com/)
- [Cybersecurity Dive](https://www.cybersecuritydive.com/)
- [Krebs on Security](https://krebsonsecurity.com/)
- [BankInfoSecurity](https://www.bankinfosecurity.com/)
- [DataBreaches.Net](https://databreaches.net/)
- [SANS Internet Storm Center](https://isc.sans.edu/)

**Vendor & Threat Research**
- [Kaspersky Securelist](https://securelist.com/)
- [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/)
- [Palo Alto Unit 42](https://unit42.paloaltonetworks.com/)
- [Mandiant (Google)](https://www.mandiant.com/resources/blog)
- [CrowdStrike Blog](https://www.crowdstrike.com/blog/)
- [SentinelOne Blog](https://www.sentinelone.com/blog/)
- [Malwarebytes Labs](https://blog.malwarebytes.com/)
- [Check Point Research](https://research.checkpoint.com/)
- [Elastic Security Labs](https://www.elastic.co/security-labs/)
- [Rapid7 Blog](https://blog.rapid7.com/)
- [Bishop Fox Blog](https://bishopfox.com/blog/)
- [Google Threat Intelligence](https://feeds.feedburner.com/threatintelligence/pvexyqv7v0v)

**Vulnerability Intelligence**
- [Zero Day Initiative (Advisories)](https://www.zerodayinitiative.com/rss/published/)
- [Zero Day Initiative (Blog)](https://www.zerodayinitiative.com/blog/)
- [Google Project Zero](https://googleprojectzero.blogspot.com/)
- [Exploit Database](https://www.exploit-db.com/)
- [PortSwigger Research](https://portswigger.net/research/)

---

## Methodology

Reports are produced by an automated pipeline that:

1. Queries RSS feeds from tracked threat intelligence sources for the prior 7-day window
2. Fetches and parses full article content
3. Analyzes each article with an LLM to extract IOCs, MITRE ATT&CK techniques, threat actors, and a severity score
4. Identifies cross-article connections — shared IOCs, corroborated actors, and campaign threads
5. Synthesizes findings into an executive summary and structured Markdown report

Severity scores are AI-assigned on a four-tier scale (Critical / High / Medium / Low) based on factors including: active exploitation in the wild, CVSS score, breadth of impact, and novelty of technique.

---

## Intended Audience

- Security operations and threat intelligence teams
- Incident responders tracking active ransomware groups
- Vulnerability management teams prioritizing patch efforts
- Researchers studying the ransomware ecosystem

---

## Disclaimer

This repository contains threat intelligence for **defensive and research purposes only**. IOCs, TTPs, and actor information are sourced from public reporting and are intended to support detection, hunting, and defense. Nothing in these reports should be used to facilitate unauthorized access or malicious activity.

Content is AI-generated from public sources and may contain errors or omissions. Always validate IOCs and findings against your own telemetry and authoritative sources before acting on them.

---

## License

Reports and content in this repository are published under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution appreciated but not required.
