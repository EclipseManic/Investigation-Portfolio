# SOC Investigation Portfolio

Seven end-to-end SOC investigations written as incident reports: what the telemetry showed, what I pivoted on, what the evidence supported, and what it could not prove.

Each case is a self-contained report built from packet captures, Windows event logs and host artefacts, following the same triage → pivot → timeline → IOCs → ATT&CK → report workflow a Tier-1/Tier-2 analyst runs.

## Start here

| # | Case | Scenario | Primary evidence |
|:--:|---|---|---|
| 1 | [Phishing Email Incident — PhishNet](Phishing%20Email%20Investigation/report.md) | Vendor-impersonation email delivering a malicious attachment | Mail headers, attachment analysis |
| 2 | [Backup Server Compromise — Telly](Linux%20Server%20Investigation/report.md) | Telnet-vulnerable backup server → root → customer database exfiltration | PCAP, Linux logs, command history |
| 3 | [LLMNR Poisoning — Noxious](LLMNR%20Poisoning%20Investigation/report.md) | Rogue host poisoning LLMNR in Active Directory to capture NTLM authentication | PCAP, NTLM challenge/response |
| 4 | [Web Exploitation & Privilege Escalation — Packet Puzzle](Network%20Intrusion%20Investigation/report.md) | PHP RCE, payload staging, GodPotato privilege escalation | PCAP, payload analysis |
| 5 | [BonitaSoft Exploitation — Meerkat](Bonitasoft%20Compromise%20Investigation/report.md) | Credential stuffing plus CVE-2022-25237 auth bypass → RCE, SSH key persistence | Web logs, host artefacts |
| 6 | [Web Shell & Java Exploitation — JustSomePages](Web%20Shell%20%26%20Java%20Exploitation%20Investigation/report.md) | JSP web shell deployment with WAF evasion and PowerShell lateral movement | PCAP, WAF/EDR telemetry |
| 7 | [Zorvyn FinTech Internship Campaign — Evasive PDF Analysis](Zorvyn%20FinTech%20Remote%20Internship%20Campaign%20%E2%80%94%20Evasive%20PDF%20Analysis/report.md) | Live fraud campaign aimed at Indian students; offer-letter PDF with evasive behaviour | OSINT, sandbox output, PDF internals |

## Report structure

Every folder holds a single `report.md` with the same sequence:

- Case overview and scoping
- Investigation steps, including the queries and filters actually used
- Findings with the supporting evidence
- Reconstructed timeline
- Indicators of compromise
- MITRE ATT&CK mapping
- Conclusion, including what the telemetry did not show

## Tools

Wireshark, tcpdump, Windows Event Viewer, Sysmon (case dependent), VirusTotal and public threat-intelligence sources.

## Scope and limits

- These are reconstructions from provided captures and lab telemetry, not live enterprise incidents. Where a capture is ambiguous, the report says so instead of asserting a verdict.
- Timestamps appear as they do in the source evidence and are not normalised across cases.
- Case 7 covers a real, publicly reported campaign. It contains only what the actors published themselves; no victim identities are included.
- Screenshots appear where they carry evidential value. Some steps are described in text only.

Reports written by Manichand Gupta. AI assistants were used for editing and formatting; the analysis, pivots and conclusions are my own.

Part of my [SOC and detection portfolio](https://github.com/EclipseManic) — the profile README maps the lab, investigation, OSINT and tooling work.
