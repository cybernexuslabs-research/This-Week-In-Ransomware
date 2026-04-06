# Threat Intelligence Report: Ransomware

**Generated:** 2026-04-06 13:00:00 UTC
**Search Term:** `ransomware`
**Date Range:** 2026-03-30 → 2026-04-06
**Articles Analyzed:** 14
**Sources:** The Hacker News, DataBreaches.Net, Krebs on Security, BleepingComputer, SecurityWeek, Threat Intelligence (Google/Mandiant), darkreading, SANS Internet Storm Center, Unit 42, Rapid7 Cybersecurity Blog

---

## Executive Summary

The ransomware threat landscape for the week of March 30–April 6, 2026 is defined by three converging trends of high strategic significance. First, BYOVD (Bring Your Own Vulnerable Driver) attacks have matured into a standard pre-ransomware tactic: Qilin and Warlock are both using shared vulnerable drivers to silently kill 300+ EDR tools before encrypting targets, with the same drivers also observed in Akira and Makop campaigns — signaling broad ecosystem adoption. Second, the TeamPCP supply chain campaign has structurally shifted how ransomware groups acquire initial access at scale: by compromising developer security tooling embedded in CI/CD pipelines (Trivy, KICS, LiteLLM), TeamPCP harvested 500K+ credentials and is now explicitly partnering with Vect ransomware to monetize victims — a first-known supply-chain-to-ransomware pipeline. Third, nation-state actors are deliberately blurring the line between geopolitical destruction and ransomware: Iran has revived Pay2Key with criminal affiliates targeting US organizations using pseudo-ransomware wiper techniques, while North Korea's UNC1069 compromised the axios npm package (100M+ weekly downloads) and deployed a sophisticated cross-platform backdoor. For defenders, the immediate priorities are rotating credentials in LiteLLM-adjacent environments, enforcing kernel driver allowlisting to counter BYOVD, and ensuring offline backup and IR readiness for healthcare and critical infrastructure — sectors under intensified targeting this week.

---

## Severity Distribution

| Severity | Count |
|---|---|
| 🔴 Critical | 4 |
| 🟠 High | 4 |
| 🟡 Medium | 4 |
| 🟢 Low | 2 |

---

## Cross-Article Connections

### Shared IOCs

| IOC Type | Value | Seen In | Significance |
|---|---|---|---|
| Domain | `sfrclak[.]com` | Articles 2, 3 | C2 domain used by UNC1069 in both the TeamPCP-adjacent axios attack and the GTIG full attribution report — confirms same North Korean infrastructure across both articles |
| IP | `142.11.206[.]73` | Articles 2, 3 | Resolved IP for sfrclak[.]com; GTIG linked this ASN to prior UNC1069 operations via AstrillVPN node — cross-corroborated by SANS ISC TeamPCP update |

### Shared Threat Actors

#### Qilin
- **Seen in:** Articles 1, 5
- **Activity:** Qilin is simultaneously advancing technically (BYOVD driver kill chain disabling 300+ EDR products, per Cisco Talos) and operationally (active breach of German political party Die Linke with politically charged data theft). CYFIRMA/Cynet data places Qilin as the most active ransomware group in recent months — the Die Linke incident demonstrates they are willing to target sensitive political targets with hybrid-warfare framing.

#### TeamPCP (PCPcat / ShellForce / DeadCatx3)
- **Seen in:** Articles 2, 4
- **Activity:** Unit 42 and SANS ISC together document the full scope of the TeamPCP supply chain campaign — from initial Trivy GitHub compromise through CanisterWorm worm/wiper evolution to confirmed ransomware partnerships with Vect and CipherForce. The SANS update adds the first confirmed victim disclosure (Mercor AI) and documents Wiz's findings on post-compromise AWS cloud enumeration patterns.

#### REvil / GandCrab
- **Seen in:** Articles 9, 10, 14
- **Activity:** Germany's BKA has doxed and issued arrest warrants for two core REvil/GandCrab operators — Daniil Shchukin (UNKN) and Anatoly Kravchuk — in the most significant ransomware attribution action of 2026. Multiple outlets confirmed the identities, with Krebs providing the most detailed historical analysis connecting UNKN to prior criminal identities (Ger0in botnet operator) and Shchukin's physical location in Krasnodar, Russia.

#### UNC1069 (North Korea nexus)
- **Seen in:** Articles 2, 3
- **Activity:** UNC1069 compromised the axios npm package maintainer account and injected WAVESHAPER.V2 backdoor affecting potentially 100M+ weekly downloads. The SANS ISC TeamPCP update confirms attribution and notes the stolen npm token exploited is exactly the credential type that TeamPCP's CanisterWorm harvests — raising the possibility that TeamPCP credential dumps enabled UNC1069's initial access.

### Campaign Threads

#### TeamPCP Supply Chain → Ransomware Pipeline
- **Articles:** 2, 3, 4
- **Description:** TeamPCP conducted a multi-stage supply chain compromise of widely deployed security tools (Trivy, KICS, LiteLLM) and developer infrastructure (Telnyx SDK), harvesting over 500,000 credentials from 500,000 machines. The campaign has now explicitly partnered with Vect and CipherForce ransomware groups to convert stolen credentials into ransomware deployments, with Mercor AI confirmed as the first identified downstream victim (4TB exfiltrated via LiteLLM compromise). Separately, UNC1069 (North Korea) may have leveraged TeamPCP-seeded credential markets to compromise the axios npm package maintainer's long-lived npm token.
- **Timeline:** Late Feb 2026 — Initial Trivy breach/credential rotation failure → March 19 — Trivy GitHub tags backdoored → March 25 — LiteLLM v1.82.7-v1.82.8 compromised → March 30-31 — axios npm attack by UNC1069 → March 31 — Mercor AI confirms breach → April 1 — LiteLLM forensic audit complete, release freeze lifted

#### German Ransomware Nexus
- **Articles:** 5, 9, 10, 14
- **Description:** Germany featured prominently this week as both a ransomware victim and enforcement actor. Qilin attacked Die Linke political party (described by the party as potential hybrid warfare), while the BKA simultaneously doxed two Russian nationals behind GandCrab/REvil for 130+ attacks causing €35.4M in German damages. Three separate sources (THN, Krebs, DataBreaches) covered the REvil unmasking, highlighting its investigative significance.
- **Timeline:** 2019-2021 — REvil/GandCrab attacks in Germany → March 26, 2026 — Die Linke network compromised by Qilin → April 1 — Qilin claims Die Linke on leak site → April 6 — BKA publishes arrest warrants for Shchukin (UNKN) and Kravchuk

### Emerging Patterns

- **BYOVD as Mainstream Pre-Ransomware Tactic:** Multiple ransomware groups (Qilin, Warlock, Akira, Makop) are now sharing the same vulnerable driver pairs (rwdrv.sys/ThrottleStop.sys + hlpdrv.sys; NSecKrnl.sys) to kill EDR products at the kernel level before deploying ransomware. The convergence on shared drivers across unrelated groups suggests a commoditized BYOVD-as-a-service offering in the criminal underground — defenders cannot rely on blocking individual driver hashes alone.

- **Supply Chain as Ransomware Initial Access Vector:** TeamPCP's explicit partnership with Vect and CipherForce ransomware groups following their CI/CD supply chain compromise represents a novel operational model: compromise developer tooling to harvest cloud credentials at scale, then hand off access to ransomware affiliates. This decoupling of access acquisition from ransomware deployment is structurally similar to IAB economics — but operating at CI/CD supply chain scale.

- **Nation-State Pseudo-Ransomware for Geopolitical Cover:** Both Iran (Agrius/Apostle, Pay2Key) and North Korea (UNC1069/WAVESHAPER.V2) are using ransomware-like techniques — either disguising wipers as ransomware or financially motivating criminal affiliates — to obscure geopolitical intent and complicate attribution. Incident responders and legal teams now face sanctions exposure risk if they pay ransoms that may be routed to OFAC-designated entities.

- **IABs Pricing Up, Targeting Government and Critical Infrastructure:** Rapid7's H2 2025 analysis shows average IAB access prices increased ~4,055% YoY to $113K, with government, retail, and IT as top targeted sectors. This premium-pricing shift directly feeds ransomware operators with high-value domain admin access — correlating with the surge in high-impact attacks on political parties, healthcare, and water treatment facilities seen this week.

---

## Article Analysis

---

### [1] Qilin and Warlock Ransomware Use Vulnerable Drivers to Disable 300+ EDR Tools

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-04-06 |
| **Severity** | 🔴 Critical |
| **URL** | [thehackernews.com/2026/04/qilin-and-warlock-ransomware-use.html](https://thehackernews.com/2026/04/qilin-and-warlock-ransomware-use.html) |

**Summary:** Qilin and Warlock (Water Manaul) ransomware groups are independently deploying BYOVD attacks to disable over 300 EDR drivers from nearly every security vendor before executing ransomware. Qilin uses a DLL side-loaded msimg32.dll that drops two vulnerable drivers — rwdrv.sys (renamed ThrottleStop.sys) for kernel memory access and hlpdrv.sys for EDR termination — while unregistering monitoring callbacks to suppress interference. Warlock exploits unpatched SharePoint servers for initial access, uses NSecKrnl.sys in a BYOVD attack to kill security tools, and pairs the kill chain with PsExec, RDP Patcher, Velociraptor C2, Cloudflare Tunnel, and Rclone for lateral movement and exfiltration, with ransomware deploying on average six days after initial access.

**Severity Rationale:** Active ransomware deployment by the most prolific current ransomware group (Qilin) combined with novel kernel-level EDR evasion targeting essentially all endpoint security vendors simultaneously.

**Threat Actors:** Qilin, Warlock (Water Manaul)

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | Hijack Execution Flow: DLL Side-Loading | Defense Evasion |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1070.004](https://attack.mitre.org/techniques/T1070/004/) | Indicator Removal: File Deletion | Defense Evasion |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Services: Remote Desktop Protocol | Lateral Movement |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

> **Note:** Specific driver file names mentioned: `msimg32.dll` (loader DLL), `rwdrv.sys` (renamed ThrottleStop.sys), `hlpdrv.sys`, `NSecKrnl.sys` (Warlock), `googleApiUtil64.sys` (prior Warlock driver). No network IOCs disclosed.

---

### [2] TeamPCP Supply Chain Campaign: Update 005 — First Confirmed Victim Disclosure

| Field | Value |
|---|---|
| **Source** | SANS Internet Storm Center |
| **Published** | 2026-04-01 |
| **Severity** | 🔴 Critical |
| **URL** | [isc.sans.edu/diary/rss/32856](https://isc.sans.edu/diary/rss/32856) |

**Summary:** SANS ISC published the fifth update to the TeamPCP supply chain campaign, documenting the first confirmed victim (Mercor AI, ~4TB exfiltrated via LiteLLM compromise including biometric identity verification data), post-compromise AWS cloud enumeration patterns documented by Wiz (TruffleHog-based credential validation, 24-hour operational tempo, AWS IAM/EC2/ECS/Lambda/S3 discovery, use of conspicuous resource names "pawn" and "massive-exfil"), and the narrowing of attribution for the axios npm compromise to UNC1069 (North Korea) using WAVESHAPER backdoor — though the npm token's origin in TeamPCP credential dumps remains possible. LiteLLM's Mandiant-led forensic audit is complete and the release freeze has been lifted after verifying only v1.82.7 and v1.82.8 were compromised.

**Severity Rationale:** First confirmed downstream victim of a massive supply chain campaign combined with active nation-state credential exploitation confirms the campaign has transitioned from theoretical to realized harm at scale.

**Threat Actors:** TeamPCP (PCPcat, ShellForce, DeadCatx3), UNC1069, LAPSUS$

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Supply Chain Compromise: Compromise Software Supply Chain | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1552](https://attack.mitre.org/techniques/T1552/) | Unsecured Credentials | Credential Access |
| [T1580](https://attack.mitre.org/techniques/T1580/) | Cloud Infrastructure Discovery | Discovery |
| [T1619](https://attack.mitre.org/techniques/T1619/) | Cloud Storage Object Discovery | Discovery |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** `142.11.206[.]73`
- **Domains:** `sfrclak[.]com`
- **Hashes:** _none_
- **CVEs:** _none_
- **URLs:** _none_

> **Additional file-based IOCs:** macOS: `/Library/Caches/com.apple.act.mond` | Windows: `%PROGRAMDATA%\wt.exe` | Linux: `/tmp/ld.py`

---

### [3] North Korea-Nexus Threat Actor Compromises Widely Used Axios NPM Package

| Field | Value |
|---|---|
| **Source** | Threat Intelligence (Google/Mandiant) |
| **Published** | 2026-03-31 |
| **Severity** | 🔴 Critical |
| **URL** | [cloud.google.com/blog/topics/threat-intelligence/north-korea-threat-actor-targets-axios-npm-package](https://cloud.google.com/blog/topics/threat-intelligence/north-korea-threat-actor-targets-axios-npm-package/) |

**Summary:** Google GTIG formally attributes the axios npm supply chain attack to UNC1069, a North Korean financially motivated threat actor active since 2018, who compromised the axios maintainer account and injected WAVESHAPER.V2 across Windows, macOS, and Linux via the malicious plain-crypto-js dependency. The SILKBELL dropper (setup.js, SHA256: e10b1fa84f1d6481625f741b69892780140d4e0e7769e7491e5f4d894c2e0e09) uses a postinstall hook to silently deploy OS-specific backdoor payloads, which beacon to C2 at sfrclak[.]com:8000 every 60 seconds supporting file enumeration, in-memory PE injection, and arbitrary command execution. On Windows, persistence is achieved via registry Run key `MicrosoftUpdate`.

**Severity Rationale:** Nation-state supply chain attack on one of npm's most downloaded packages (100M+ and 83M weekly downloads for the compromised versions) with a cross-platform backdoor enabling persistent access and in-memory code execution.

**Threat Actors:** UNC1069

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Supply Chain Compromise: Compromise Software Supply Chain | Initial Access |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript | Execution |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command and Scripting Interpreter: PowerShell | Execution |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion |
| [T1036.005](https://attack.mitre.org/techniques/T1036/005/) | Masquerading: Match Legitimate Name or Location | Defense Evasion |
| [T1070.004](https://attack.mitre.org/techniques/T1070/004/) | Indicator Removal: File Deletion | Defense Evasion |
| [T1547.001](https://attack.mitre.org/techniques/T1547/001/) | Boot or Logon Autostart Execution: Registry Run Keys | Persistence |
| [T1055](https://attack.mitre.org/techniques/T1055/) | Process Injection | Defense Evasion |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control |

**IOCs Extracted:**
- **IPs:** `142.11.206[.]73`
- **Domains:** `sfrclak[.]com`
- **Hashes:** `e10b1fa84f1d6481625f741b69892780140d4e0e7769e7491e5f4d894c2e0e09` (setup.js / SILKBELL)
- **CVEs:** _none_
- **URLs:** _none_

> **Additional IOCs:** Attacker email: `ifstap@proton.me` | macOS persistence: `/Library/Caches/com.apple.act.mond` | Windows: `%PROGRAMDATA%\wt.exe`, `%PROGRAMDATA%\system.bat`, `HKCU:\Software\Microsoft\Windows\CurrentVersion\Run\MicrosoftUpdate` | Linux: `/tmp/ld.py`

---

### [4] Weaponizing the Protectors: TeamPCP's Multi-Stage Supply Chain Attack on Security Infrastructure

| Field | Value |
|---|---|
| **Source** | Unit 42 |
| **Published** | 2026-03-31 |
| **Severity** | 🔴 Critical |
| **URL** | [unit42.paloaltonetworks.com/teampcp-supply-chain-attacks](https://unit42.paloaltonetworks.com/teampcp-supply-chain-attacks/) |

**Summary:** Unit 42 provides the definitive technical account of TeamPCP's supply chain campaign against Trivy, KICS, LiteLLM, and the Telnyx Python SDK, detailing three generations of the kamikaze.sh payload evolving from monolithic credential harvester to CanisterWorm — a self-replicating worm with decentralized C2, SSH key harvesting, Docker API scanning, and targeted wiper components. The campaign exfiltrated 300+ GB of credentials from 500,000 machines and is now partnering with Vect ransomware for victim monetization, with 16 organizations publicly identified on the CipherForce leak site. The C2 used typosquatted domain scan.aquasecurtiy[.]org with ICP backup infrastructure.

**Severity Rationale:** Massive supply chain compromise of widely embedded security scanning tools with confirmed downstream extortion partnerships and a worm component capable of self-propagation across cloud environments.

**Threat Actors:** TeamPCP (PCPcat, ShellForce, DeadCatx3), Vect, CipherForce

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Supply Chain Compromise: Compromise Software Supply Chain | Initial Access |
| [T1059.004](https://attack.mitre.org/techniques/T1059/004/) | Command and Scripting Interpreter: Unix Shell | Execution |
| [T1059.006](https://attack.mitre.org/techniques/T1059/006/) | Command and Scripting Interpreter: Python | Execution |
| [T1552](https://attack.mitre.org/techniques/T1552/) | Unsecured Credentials | Credential Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |
| [T1053](https://attack.mitre.org/techniques/T1053/) | Scheduled Task/Job | Persistence |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** `scan.aquasecurtiy[.]org`, `tdtqy-oyaaa-aaaae-af2dq-cai.raw.icp0[.]io`
- **Hashes:** _none_
- **CVEs:** `CVE-2025-55182`
- **URLs:** _none_

---

### [5] Die Linke German Political Party Confirms Data Stolen by Qilin Ransomware

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | 2026-04-03 |
| **Severity** | 🟠 High |
| **URL** | [bleepingcomputer.com/news/security/die-linke-german-political-party-confirms-data-stolen-by-qilin-ransomware](https://www.bleepingcomputer.com/news/security/die-linke-german-political-party-confirms-data-stolen-by-qilin-ransomware/) |

**Summary:** The Qilin ransomware group breached German parliamentary party Die Linke on March 26, 2026, stealing internal organizational data and employee personal information, though the party's 123,000-member database was reportedly spared. The party publicly attributed the attack to Qilin and characterized it as likely part of "hybrid warfare" given the geopolitical timing, noting Russian-speaking financially and politically motivated cybercriminals were responsible. Qilin claimed the attack on April 1 on its dark web leak site without publishing data samples, applying standard double-extortion pressure.

**Severity Rationale:** Active breach of a national parliamentary political party by the current most-active ransomware group, with geopolitical dimensions and sensitive employee/organizational data at risk of public release.

**Threat Actors:** Qilin

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration |

**IOCs Extracted:**

_No IOCs extracted._

---

### [6] In Other News: ChatGPT Data Leak, Android Rootkit, Water Facility Hit by Ransomware

| Field | Value |
|---|---|
| **Source** | SecurityWeek |
| **Published** | 2026-04-03 |
| **Severity** | 🟠 High |
| **URL** | [securityweek.com/in-other-news-chatgpt-data-leak-android-rootkit-water-facility-hit-by-ransomware](https://www.securityweek.com/in-other-news-chatgpt-data-leak-android-rootkit-water-facility-hit-by-ransomware/) |

**Summary:** SecurityWeek's weekly roundup includes a ransomware attack on the Minot, North Dakota water treatment plant (March 14) that forced manual operations for 16 hours after network disconnection to contain the incident — a critical infrastructure attack with direct public safety implications. The roundup also covers Everest ransomware claiming Nissan data via a third-party supplier breach, a high-severity Symantec DLP vulnerability (CVE-2026-3991), and an Android banking trojan Mirax available for $3,000/month targeting 700+ financial apps.

**Severity Rationale:** Ransomware successfully compromising a water treatment plant represents critical infrastructure disruption with potential public health consequences, even though manual operations prevented service interruption.

**Threat Actors:** Everest

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |

**IOCs Extracted:**
- **IPs:** _none_
- **Domains:** _none_
- **Hashes:** _none_
- **CVEs:** `CVE-2026-3991`
- **URLs:** _none_

---

### [7] vSphere and BRICKSTORM Malware: A Defender's Guide

| Field | Value |
|---|---|
| **Source** | Threat Intelligence (Google/Mandiant) |
| **Published** | 2026-04-02 |
| **Severity** | 🟠 High |
| **URL** | [cloud.google.com/blog/topics/threat-intelligence/vsphere-brickstorm-defender-guide](https://cloud.google.com/blog/topics/threat-intelligence/vsphere-brickstorm-defender-guide/) |

**Summary:** Mandiant/Google published a comprehensive defender's guide to BRICKSTORM, malware targeting VMware vSphere environments that establishes persistence at the hypervisor layer below where endpoint agents operate, gaining administrative control over all vCenter-managed VMs and datastores. The attack exploits weak security architecture, misconfigured identities, and absence of visibility below the guest OS — not product vulnerabilities. Mandiant released a vCenter Hardening Script and outlines a four-phase defense framework: STIG benchmarking, identity hardening (PAWs/PAM), Zero Trust networking, and logging/forensic visibility.

**Severity Rationale:** Persistent compromise of virtualization control plane grants attackers administrative control over all workloads organization-wide, and vSphere 7's October 2025 end-of-life creates an unpatched exposure window for a large segment of enterprise infrastructure.

**Threat Actors:** BRICKSTORM (China-nexus, per prior GTIG research)

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1552](https://attack.mitre.org/techniques/T1552/) | Unsecured Credentials | Credential Access |
| [T1053](https://attack.mitre.org/techniques/T1053/) | Scheduled Task/Job | Persistence |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion |

**IOCs Extracted:**

_No IOCs extracted._

---

### [8] Iran Deploys 'Pseudo-Ransomware,' Revives Pay2Key Operations

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-03-31 |
| **Severity** | 🟠 High |
| **URL** | [darkreading.com/threat-intelligence/iran-pseudo-ransomware-pay2key-operations](https://www.darkreading.com/threat-intelligence/iran-pseudo-ransomware-pay2key-operations) |

**Summary:** Iran has revived Pay2Key ransomware by recruiting affiliates from Russian criminal forums and increasing the affiliate profit share from 70% to 80% for attacks against US and Israeli targets, using the operation as a geopolitical force multiplier following the Feb. 28 US-Israel attack on Iranian nuclear facilities. Concurrently, Iran-backed APT Agrius is deploying the Apostle malware — originally a wiper retrofitted as ransomware — as "pseudo-ransomware" to disguise destructive state objectives as financial crime. The KELA report warns that paying ransom to Iran-linked entities could trigger OFAC sanctions violations.

**Severity Rationale:** State-sponsored actors using ransomware-as-a-cover for destructive operations against US critical infrastructure, with legal sanctions exposure risk compounding the technical threat.

**Threat Actors:** Agrius, Pay2Key

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact |
| [T1583](https://attack.mitre.org/techniques/T1583/) | Acquire Infrastructure | Resource Development |

**IOCs Extracted:**

_No IOCs extracted._

---

### [9] BKA Identifies REvil Leaders Behind 130 German Ransomware Attacks

| Field | Value |
|---|---|
| **Source** | The Hacker News |
| **Published** | 2026-04-06 |
| **Severity** | 🟡 Medium |
| **URL** | [thehackernews.com/2026/04/bka-identifies-revil-leaders-behind-130.html](https://thehackernews.com/2026/04/bka-identifies-revil-leaders-behind-130.html) |

**Summary:** Germany's BKA has issued arrest warrants for two Russian nationals — Daniil Maksimovich Shchukin (alias UNKN, 31, from Krasnodar) who led GandCrab and REvil, and Anatoly Kravchuk (43, developer) — for 130 ransomware attacks in Germany between 2019 and 2021 causing over €35.4M in damages and extracting €1.9M in ransom payments from 25 victims. REvil, an evolution of GandCrab, was responsible for major attacks against Kaseya and JBS before being disrupted by a multi-agency law enforcement operation in late 2021. Russia's FSB arrested some members in 2022 with four sentenced to prison in October 2024.

**Severity Rationale:** Historical attribution and law enforcement action against now-defunct group; significant for intelligence and deterrence value but no active threat from these specific actors.

**Threat Actors:** REvil (Sodinokibi, Water Mare, Gold Southfield), GandCrab, UNKN

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

### [10] Germany Doxes "UNKN," Head of RU Ransomware Gangs REvil, GandCrab

| Field | Value |
|---|---|
| **Source** | Krebs on Security |
| **Published** | 2026-04-06 |
| **Severity** | 🟡 Medium |
| **URL** | [krebsonsecurity.com/2026/04/germany-doxes-unkn-head-of-ru-ransomware-gangs-revil-gandcrab](https://krebsonsecurity.com/2026/04/germany-doxes-unkn-head-of-ru-ransomware-gangs-revil-gandcrab/) |

**Summary:** Brian Krebs provides the most detailed account of the BKA doxing of UNKN (Daniil Shchukin), tracing his criminal evolution from botnet operator "Ger0in" (2010–2011) through GandCrab ($2B extorted before May 2019 shutdown) to REvil leadership. Krebs connects Shchukin to the U.S. DOJ's Feb. 2023 cryptocurrency seizure filing, a $317K digital wallet, and photo corroboration via birthday party images from Krasnodar. The article provides important historical context on how REvil pioneered double extortion and big-game hunting of organizations with cyber insurance.

**Severity Rationale:** Detailed historical intelligence on now-defunct threat actors; significant for attribution research and understanding ransomware-as-a-service evolution but no current operational threat.

**Threat Actors:** REvil, GandCrab, UNKN (Daniil Shchukin)

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

### [11] Evolution of Ransomware: Multi-Extortion Ransomware Attacks

| Field | Value |
|---|---|
| **Source** | BleepingComputer |
| **Published** | 2026-04-03 |
| **Severity** | 🟡 Medium |
| **URL** | [bleepingcomputer.com/news/security/evolution-of-ransomware-multi-extortion-ransomware-attacks](https://www.bleepingcomputer.com/news/security/evolution-of-ransomware-multi-extortion-ransomware-attacks/) |

**Summary:** Penta Security-sponsored analysis documents the evolution from single to triple extortion ransomware, noting 124 active ransomware groups (73 newly emerged), a 49% YoY surge in confirmed attacks in 2025 (1,174 incidents), and high-impact cases at the University of Mississippi Medical Center (Epic EHR offline across 35 clinics) and payment processor BridgePay in February 2026. AI-powered tools are lowering the barrier to entry, enabling less sophisticated actors to deploy ransomware. Backups alone are no longer sufficient defense as stolen-data extortion continues independently of encryption payment.

**Severity Rationale:** Informational/vendor-sponsored analysis with statistical framing; valuable for threat landscape awareness but no new active campaign or novel technique disclosed.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

### [12] Initial Access Brokers Have Shifted to High-Value Targets and Premium Pricing

| Field | Value |
|---|---|
| **Source** | Rapid7 Cybersecurity Blog |
| **Published** | 2026-03-31 |
| **Severity** | 🟡 Medium |
| **URL** | [rapid7.com/blog/post/tr-initial-access-broker-shift-high-value-targets-premium-pricing](https://www.rapid7.com/blog/post/tr-initial-access-broker-shift-high-value-targets-premium-pricing) |

**Summary:** Rapid7's H2 2025 analysis of five underground forums (Exploit, XSS, BreachForums, DarkForums, RAMP) shows IABs have dramatically increased targeting of government, retail, and IT sectors, with average victim revenue at $3.24B and average access listing price at $113K — a ~4,055% price increase YoY. DarkForums (221 threads) and RAMP (208 threads) now dominate, accounting for 81% of observed IAB threads. Domain Admin access (32% of listings) has grown while lower-privilege access declined, and RDP remains the leading access vector (21.2%) followed by VPN and RDWeb.

**Severity Rationale:** Threat intelligence report providing structural insight into IAB market evolution; no active exploitation but directly enables ransomware targeting of high-value organizations.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**

| ID | Technique | Tactic |
|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access |

**IOCs Extracted:**

_No IOCs extracted._

---

### [13] Ransomware Will Hit Hospitals. Rehearsals Are Key to Defense

| Field | Value |
|---|---|
| **Source** | darkreading |
| **Published** | 2026-04-01 |
| **Severity** | 🟢 Low |
| **URL** | [darkreading.com/cybersecurity-operations/ransomware-hospitals-preparation-key-defense](https://www.darkreading.com/cybersecurity-operations/ransomware-hospitals-preparation-key-defense) |

**Summary:** RSAC 2026 presentation by CMIO Joseph Izzo of San Joaquin General Hospital describes the operational reality of healthcare ransomware response — standard downtime playbooks fail during extended outages, "gray zone" partial failures are underexercised, and analog fallback workflows require rehearsal under realistic pressure. Key recommendations include redundant identity verification, prevalidated paper MAR processes, two-person high-risk confirmation workflows, tabletop exercises involving frontline staff, and careful management of shadow AI tools as an additional attack surface.

**Severity Rationale:** Informational/educational content from a conference presentation; no new threat intelligence but relevant operational guidance for healthcare security teams.

**Threat Actors:** _None identified_

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

### [14] Germany Doxes "UNKN," Head of RU Ransomware Gangs REvil, GandCrab

| Field | Value |
|---|---|
| **Source** | DataBreaches.Net |
| **Published** | 2026-04-06 |
| **Severity** | 🟢 Low |
| **URL** | [databreaches.net/2026/04/06/germany-doxes-unkn-head-of-ru-ransomware-gangs-revil-gandcrab](https://databreaches.net/2026/04/06/germany-doxes-unkn-head-of-ru-ransomware-gangs-revil-gandcrab/) |

**Summary:** DataBreaches.Net aggregated brief covering the BKA advisory doxing UNKN (Daniil Shchukin) and Anatoly Kravchuk of GandCrab/REvil, referencing Krebs for full details. The BKA confirms 130 attacks and ~$2M in ransom payments extracted across 24 cyberattacks causing €35M in total economic damage across Germany.

**Severity Rationale:** Short aggregation post duplicating content from the Krebs article with no additional intelligence value.

**Threat Actors:** REvil, GandCrab, UNKN

**MITRE ATT&CK Techniques:**

_No techniques mapped._

**IOCs Extracted:**

_No IOCs extracted._

---

## Consolidated IOC Table

| IOC Type | Value | Source Articles |
|---|---|---|
| CVE | `CVE-2025-55182` | 4 |
| CVE | `CVE-2026-3991` | 6 |
| Domain | `scan.aquasecurtiy[.]org` | 4 |
| Domain | `sfrclak[.]com` | 2, 3 |
| Domain | `tdtqy-oyaaa-aaaae-af2dq-cai.raw.icp0[.]io` | 4 |
| Hash (SHA256) | `e10b1fa84f1d6481625f741b69892780140d4e0e7769e7491e5f4d894c2e0e09` | 3 |
| IP | `142.11.206[.]73` | 2, 3 |

> **File-based IOCs (not network-routable):**
> - macOS: `/Library/Caches/com.apple.act.mond` (Articles 2, 3)
> - Windows: `%PROGRAMDATA%\wt.exe`, `%PROGRAMDATA%\system.bat` (Articles 2, 3)
> - Windows Registry: `HKCU:\Software\Microsoft\Windows\CurrentVersion\Run\MicrosoftUpdate` (Article 3)
> - Linux: `/tmp/ld.py` (Articles 2, 3)
> - Driver files: `rwdrv.sys`, `hlpdrv.sys`, `NSecKrnl.sys`, `msimg32.dll` (Article 1)

---

## MITRE ATT&CK Coverage

| ID | Technique | Tactic | Articles |
|---|---|---|---|
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Initial Access | 1, 2, 4, 5, 7, 12 |
| [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Initial Access | 1, 7, 12 |
| [T1195.002](https://attack.mitre.org/techniques/T1195/002/) | Supply Chain Compromise: Compromise Software Supply Chain | Initial Access | 2, 3, 4 |
| [T1053](https://attack.mitre.org/techniques/T1053/) | Scheduled Task/Job | Persistence | 4, 7 |
| [T1547.001](https://attack.mitre.org/techniques/T1547/001/) | Boot or Logon Autostart Execution: Registry Run Keys | Persistence | 3 |
| [T1583](https://attack.mitre.org/techniques/T1583/) | Acquire Infrastructure | Resource Development | 8 |
| [T1552](https://attack.mitre.org/techniques/T1552/) | Unsecured Credentials | Credential Access | 2, 4, 7 |
| [T1580](https://attack.mitre.org/techniques/T1580/) | Cloud Infrastructure Discovery | Discovery | 2 |
| [T1619](https://attack.mitre.org/techniques/T1619/) | Cloud Storage Object Discovery | Discovery | 2 |
| [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Defense Evasion | 3 |
| [T1036.005](https://attack.mitre.org/techniques/T1036/005/) | Masquerading: Match Legitimate Name or Location | Defense Evasion | 3 |
| [T1055](https://attack.mitre.org/techniques/T1055/) | Process Injection | Defense Evasion | 3 |
| [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Privilege Escalation | 1 |
| [T1070.004](https://attack.mitre.org/techniques/T1070/004/) | Indicator Removal: File Deletion | Defense Evasion | 1, 3 |
| [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Impair Defenses: Disable or Modify Tools | Defense Evasion | 1, 4, 7 |
| [T1574.002](https://attack.mitre.org/techniques/T1574/002/) | Hijack Execution Flow: DLL Side-Loading | Defense Evasion | 1 |
| [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | Command and Scripting Interpreter: PowerShell | Execution | 3 |
| [T1059.004](https://attack.mitre.org/techniques/T1059/004/) | Command and Scripting Interpreter: Unix Shell | Execution | 4 |
| [T1059.006](https://attack.mitre.org/techniques/T1059/006/) | Command and Scripting Interpreter: Python | Execution | 4 |
| [T1059.007](https://attack.mitre.org/techniques/T1059/007/) | Command and Scripting Interpreter: JavaScript | Execution | 3 |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Services: Remote Desktop Protocol | Lateral Movement | 1 |
| [T1567](https://attack.mitre.org/techniques/T1567/) | Exfiltration Over Web Service | Exfiltration | 5 |
| [T1041](https://attack.mitre.org/techniques/T1041/) | Exfiltration Over C2 Channel | Exfiltration | 4 |
| [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Exfiltration | 1 |
| [T1071.001](https://attack.mitre.org/techniques/T1071/001/) | Application Layer Protocol: Web Protocols | Command and Control | 1, 3 |
| [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Impact | 8 |
| [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | Impact | 1, 2, 4, 5, 6, 8 |

---

## Report Metadata

| Field | Value |
|---|---|
| **Skill Version** | threat-analysis v1.0 |
| **Feeds Searched** | 26 |
| **Articles Retrieved** | 14 |
| **Articles Analyzed** | 14 |
| **Articles Skipped** | 0 |
| **Report Generated** | 2026-04-06 13:00:00 UTC |
