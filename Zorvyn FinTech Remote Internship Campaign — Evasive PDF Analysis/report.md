# SOC & Fraud Investigation: Zorvyn FinTech Remote Internship Campaign
![Status](https://img.shields.io/badge/Status-Confirmed%20Scam-red)
![AV Detection](https://img.shields.io/badge/AV%20Detection-0%2F64-critical)
![MITRE Tactics](https://img.shields.io/badge/MITRE%20Tactics-9-orange)
![Severity](https://img.shields.io/badge/Severity-HIGH-red)
> **Analyst:** Manichand Gupta  
> **Date:** 12 April 2026  
> **Scope:** Technical malware analysis, fraud modus operandi, and company OSINT profile for Zorvyn FinTech “internship” offers  
> **Verdict:** High‑risk scam operation with evasive malware and financial/identity data harvesting intent
***

<img width="1762" height="789" alt="image" src="https://github.com/user-attachments/assets/d44d17bd-fb9a-4b66-bbb3-43ee5ccffaea" />


## Quick Navigation

1. [Executive Summary](#executive-summary)
2. [Case Context & Timeline](#case-context-timeline)
3. [Company & Infrastructure OSINT Profile](#company-infrastructure-osint-profile)
4. [Social Engineering & Banking / Identity Data Strategy](#social-engineering-banking-identity-data-strategy)
5. [Technical Analysis of the Offer-Letter PDF](#technical-analysis-offer-letter-pdf)
6. [Combined Threat Model](#combined-threat-model)
7. [Indicators of Compromise (IOCs)](#indicators-of-compromise)
8. [Recommended Defensive Actions](#recommended-defensive-actions)
9. [Conclusion](#conclusion)
10. [References](#references)

***

<a id="executive-summary"></a>

## 1. Executive Summary

Multiple Indian students and freshers have reported receiving highly attractive remote internship offers from an entity calling itself **“Zorvyn FinTech Pvt. Ltd.”**, typically promising **₹35–45K/month stipends and PPOs up to ₹11–14 LPA** for roles such as Cybersecurity Analyst, Data Analyst, Frontend Developer, and Backend Developer. Public OSINT and sandbox analysis of one such **offer-letter PDF** (SHA256 `21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4`) show that the campaign combines **social engineering, legal misrepresentation, evasive malware behavior, and aggressive collection of banking and identity data**.

Although **0/64 antivirus engines on VirusTotal** flagged the file as malicious, behavioral sandboxes mapped multiple MITRE ATT&CK tactics, including **sandbox evasion, credential access, and process injection staging**. ANY.RUN’s default 60‑second run also reported "No threats detected", consistent with deliberate **timing‑based evasion**.

OSINT further shows that Zorvyn:
- **Has no CIN registration on India’s MCA portal** despite using the legal suffix “Pvt. Ltd.” in offer letters and emails.
- Operates across **multiple inconsistent domains** (`zorvyn.io`, `zorvyn.org`, `zorvyn.co`) with **recent registrations** that do not match its claimed founding year of 2022.
- Uses **fake or highly suspicious LinkedIn employee profiles** and AI‑generated office imagery to simulate legitimacy.
- Asks selected candidates to submit **bank account details, Aadhaar, PAN and full home address before any verified onboarding**, framed as “stipend processing” and “welcome kit” workflows.

The combined evidence indicates a **high‑risk, likely fraudulent operation** whose primary objectives are **credential theft and financial/identity data harvesting**, rather than genuine employment.

***

<a id="case-context-timeline"></a>

## 2. Case Context & Timeline

### 2.1 Typical Candidate Journey

Across Reddit, LinkedIn posts, and YouTube analyses, the following pattern emerges:

1. **Mass Outreach & Hiring Posts**  
   - LinkedIn and job platforms show large‑scale hiring for multiple internship roles with **30–45K monthly stipends and high PPOs**, often claiming **“120+ interns”** being onboarded.
   - Application is usually via LinkedIn Easy Apply, Internshala, or similar platforms.

2. **Screening Assignment Instead of Proper Interviews**  
   - Many candidates report **no real technical interview**, only a time‑bound assignment (e.g., 100 MCQs in 120 minutes, or a full React dashboard build).
   - Assignments often require **3–12 hours of work**, with no guaranteed feedback.

3. **Polished Offer Letter with Unrealistic Benefits**  
   - Selected candidates receive a **highly polished 4‑page offer letter** on “Zorvyn FinTech Pvt. Ltd.” letterhead, listing generous stipend, WFH arrangement, and PPO at 11–14 LPA.
   - The PDF is signed by a “CEO” and includes NDAs, confidentiality clauses, HR policies, and sometimes **FinTech‑style language about payment processing and compliance**.

4. **Urgency & Deadline Pressure**  
   - Candidates are often given **24 hours or less** to sign and return the offer, or emails are sent **after the stated deadline**, creating panic and limiting verification time.

5. **Onboarding Portals Demanding Sensitive Data**  
   - Email onboarding flows contain portal links asking for **bank account details, IFSC, Aadhaar, PAN, full home address, and sometimes device preferences** (keyboard, mouse, T‑shirt size) under the pretext of stipend disbursal and welcome kits.
   - Some flows explicitly state that **“banking and payment details will be collected”** and that the candidate is **“solely responsible for ensuring that the payment information provided is accurate.”**

6. **Silence, Moving Goalposts, or Domain Changes**  
   - Many interns report doing assignments and signing letters but **never receiving clear joining details, stipend payment, or verifiable HR contacts**.
   - Domain changes (e.g., `zorvyn.io` to `zorvyn.org`) break previous portals, meaning candidates cannot access submissions or see application status.

### 2.2 Analyst’s Specific Sample

The sample investigated here is a PDF offer letter named **`Offer_Letter_Manichand_Gupta.pdf`** (title in metadata: “Internship Offer Letter | Zorvyn FinTech Pvt. Ltd.”) that was subsequently re‑submitted to sandboxes under generic names such as `attachment.pdf`.

ANY.RUN’s 60‑second analysis reported *“No malicious indicators”* and 0 suspicious processes, while VirusTotal’s behavioral engines (CAPE, Jujubox, Zenbox) detected extensive suspicious activity despite 0/64 AV detections.



***

<a id="company-infrastructure-osint-profile"></a>

## 3. Company & Infrastructure OSINT Profile

### 3.1 Claimed Identity vs Legal Reality

Zorvyn markets itself consistently as **“Zorvyn FinTech Pvt. Ltd.”**, a FinTech firm claiming to have been **“Empowering Financial Innovation Since 2022”**. However, independent checks show the following:

| Check | Observation |-
|------|-------------|-
| MCA (India) CIN search for “Zorvyn FinTech Pvt. Ltd.” | **No company record found** on the Ministry of Corporate Affairs portal. |-
| Right to use “Pvt. Ltd.” in India | Legally reserved for entities registered with MCA and assigned a CIN; using it without registration is misrepresentation. |-
| Company’s explanation | HR replies to candidates claim Zorvyn is **registered in the UAE**, therefore “no CIN,” while still signing communication as “Pvt. Ltd.” in India. |-
| UAE entity verification | Candidates and independent researchers report **no verifiable UAE trade license or registration number** publicly shared. |-

This mismatch between **legal form claimed (Indian Pvt. Ltd.)** and **registration story (foreign UAE entity)** is a strong red flag and matches typical patterns in cross‑border hiring scams.

<img width="1771" height="821" alt="Screenshot 2026-04-12 144043" src="https://github.com/user-attachments/assets/1e1a4509-d698-43a8-a24a-85df1eb410e2" />


### 3.2 Domain Footprint & Timeline

Community WHOIS checks and public posts provide the following timeline:

| Domain | Claimed narrative | Observed registration evidence |
|--------|-------------------|--------------------------------|
| `zorvyn.io` | Initially presented as the “official” company site; later described as suspended due to mass reporting campaigns. | Public WHOIS shows registration around **March 2025**, not 2022, and external scanners (e.g., ScamDetector, ScamAdviser) flagged risk concerns. |
| `zorvyn.org` | Later primary domain; used in email addresses (`hr@zorvyn.org`) and internship pages. | Registered in **April 2026**, again contradicting the 2022 founding claim. |
| `zorvyn.co` | Appears in onboarding URLs (e.g., `employeesupport.zorvyn.co`); sometimes cited as “employee support” subdomain. | Separate ccTLD with its own registration; used mainly for submission portals and onboarding flows |

These domain patterns support the assessment that **infrastructure is opportunistic and reactive**, not that of a long‑standing regulated FinTech firm.

<img width="1451" height="960" alt="Screenshot 2026-04-12 145808" src="https://github.com/user-attachments/assets/010e93b1-ffa2-41e5-a73a-399bdefa7398" />
<img width="1491" height="562" alt="Screenshot 2026-04-12 145919" src="https://github.com/user-attachments/assets/2806ced8-a8b4-4c83-8a22-8493c70bf7b1" />
<img width="1307" height="648" alt="Screenshot 2026-04-12 145902" src="https://github.com/user-attachments/assets/56ad865f-e1bc-4f17-ab43-45d68696a6cc" />


### 3.3 Fake Employee & Office Persona Construction

Investigations by students, Reddit users, and a Bengaluru engineer covered by mainstream media reveal several anomalies:

- **LinkedIn employees** such as multi‑year Zorvyn veterans and C‑level executives show **improbable timelines**, such as an “IIT 2015 graduate” only creating a LinkedIn profile in 2025.
- Some “employees” reuse **stock or AI‑generated profile pictures** and have thin or erratic work histories, with little activity beyond liking Zorvyn posts.
- Shared “office” photos were later admitted by Zorvyn to be sourced from a **commercial design/AI agency**, not an actual Zorvyn office.

These inconsistencies indicate a deliberate attempt to **simulate corporate legitimacy using fabricated digital personas**.

***

<a id="social-engineering-banking-identity-data-strategy"></a>

## 4. Social Engineering & Banking / Identity Data Strategy

### 4.1 Psychological Hooks

Zorvyn’s messaging is fine‑tuned to Indian fresher psychology:

- **High stipend (₹35–45K/month) + PPO up to ₹11–14 LPA** for interns with minimal interviews.
- **Full remote WFH** with flexible hours, highly attractive to non‑metro students.
- **Branded FinTech positioning** suggesting cutting‑edge work in finance and payments.
- **Strict NDAs and legalistic language** in offer letters to make the opportunity feel scarce and premium.

The combination of **status, money, and urgency** is designed to suppress skepticism and push candidates to sign quickly.

### 4.2 Data Collection Flow

From multiple victims’ descriptions and offer/onboarding screenshots:

1. **Offer Letter Clauses**  
   The PDF explicitly states that Zorvyn will **collect “banking and payment details”** from the intern and that the intern is **responsible for ensuring payment information is accurate**.

2. **Onboarding Portal**  
   After acceptance, candidates receive credentials (sometimes transmitted in plaintext email) to an **employee portal** where they are required to enter:
   - Full name, date of birth, phone number, and permanent address.
   - Bank account number, IFSC code, and sometimes UPI ID.
   - Aadhaar and PAN details ostensibly for KYC and stipend processing.

3. **Welcome Kit & Equipment Narrative**  
   Some flows mention **T‑shirt size, peripherals (keyboard, mouse)** and shipping addresses for “welcome kits”, which normalizes the request for precise residential data.

4. **No Transparent Payment History**  
   Despite hundreds of reported offer letters and long assignments, OSINT yields **no credible, independently verifiable reports of consistent stipend payouts and internship completion certificates**, which would be expected if this were a genuine large‑scale program.

### 4.3 Likely Fraud Objectives

Based on these patterns, combined with evasive malware behavior in the PDF, the campaign likely targets:

- **Bank account takeover and fraudulent transactions** using collected account details and potential SIM‑swap or social engineering of banks.
- **Identity theft** — Aadhaar and PAN allow creation of **synthetic identities** or unauthorized loans/credit lines.
- **Credential harvesting** via the PDF’s suspicious behavior (VaultSvc, DPAPI, browser profile access), harvesting saved browser passwords and corporate credentials
- **Monetization of free labor** by having students complete complex assignments that could be repurposed without paying them, although the primary risk appears to be data abuse.

This aligns with a **dual‑track fraud model**: one track harvesting personal/financial data, the other extracting unpaid technical work.

***

<a id="technical-analysis-offer-letter-pdf"></a>

## 5. Technical Analysis of the Offer-Letter PDF

## 5.0 Behavioral Overview — What This PDF Actually Does

> ⚠️ **Analyst Note:** The following describes **confirmed behavioral indicators** 
> observed across CAPE, Jujubox, and Zenbox sandbox engines. Full payload 
> detonation was **not confirmed** due to deliberate sandbox evasion by the sample. 
> All findings represent what was **observed and logged** — not assumed.

---

### Phase 1 — Environment Fingerprinting (Evasion First)

Before executing any malicious logic, the PDF triggers a series of 
environment checks to determine if it is running on a real victim machine 
or inside a security analysis environment:

| API Call | Purpose |
|---|---|
| `IsDebuggerPresent` | Detects attached debuggers or analysis tools |
| `GetTickCount` / `GetTickCount64` | Checks if system clock is artificially accelerated (common in sandboxes) |
| `Sleep()` | Stalls execution to outlast default sandbox timeout windows |
| `GetAdaptersAddresses` | Enumerates network adapters to detect VM/sandbox network profiles |

**Result:** If any check suggests an analysis environment, the payload 
remains dormant — explaining the **0/64 VirusTotal AV result** and the 
**"No threats detected" ANY.RUN verdict**. The file only proceeds on 
what it determines to be a real endpoint.

---

### Phase 2 — Defense Removal

Once environment checks pass, the sample disables a key protection 
before attempting any credential access:

```text
Registry Write:
SOFTWARE\Adobe\Acrobat Reader\DC\DLLInjection\bBlockDLLInjection = 0
```

Adobe Reader ships with a built-in DLL injection protection mechanism. 
Setting this value to `0` **explicitly disables that protection**, 
allowing foreign code to be injected into the trusted `Acrobat.exe` 
process without triggering Adobe's own defenses. This is a preparation 
step — not accidental behavior.

---

### Phase 3 — Credential & Data Access (Confirmed Behavioral Indicators)

The following access attempts were **directly observed in sandbox logs**:

**A. Browser Credential Decryption via DPAPI**
```text
Module loaded: C:\Windows\SYSTEM32\DPAPI.dll
Files accessed:
  Edge\User Data\Default\Secure Preferences
  Edge\User Data\Default\Local State
  INetCookies\ESE\
```
`DPAPI.dll` is Windows' native Data Protection API — the same component 
browsers use to **encrypt saved passwords on disk**. Loading it alongside 
direct access to browser profile files is the standard method used by 
credential-stealing malware to **decrypt saved passwords without needing 
to know the master key**. Session cookies stored here also allow 
**authentication bypass without a password**, rendering 2FA ineffective.

**B. Windows Credential Vault Access**
```text
Service opened: VaultSvc (Windows Credential Manager)
Service opened: clipsvc  (Clipboard service)
```
`VaultSvc` is the service that manages Windows Credential Manager — 
the store for saved Wi-Fi passwords, RDP credentials, Outlook login 
details, and network share credentials. A PDF document has **no 
legitimate reason** to open this service.

**C. LSASS Process Context**
```text
Process observed in tree: lsass.exe (PID 716)
```
LSASS (Local Security Authority Subsystem Service) holds **active 
session tokens, NTLM password hashes, and Kerberos tickets** in memory. 
Its presence in the process tree aligns with MITRE T1003 (OS Credential 
Dumping). Direct memory interaction was not confirmed within the sandbox 
window, but its appearance is a significant indicator of credential 
harvesting intent.

**D. Enterprise Authentication Token Access**
```text
Files accessed:
  C:\Users\<USER>\AppData\Roaming\arcot\ids
  C:\Users\<USER>\Documents\ArcotIDs
```
Arcot IDs are enterprise SSO and 2FA authentication tokens (RSA Arcot 
WebFort format). Accessing these paths indicates targeting of 
**stored enterprise credentials beyond standard browser passwords**.

---

### Phase 4 — Silent Second-Stage Payload Delivery

```text
Process spawned: C:\Windows\System32\msiexec.exe /V
Mutex created:   Global\_MSIExecute
```

Opening a PDF should **never** invoke Windows Installer (`msiexec.exe`). 
The `/V` flag is a **silent installation switch** — it runs with no 
visible window, no UAC prompt, and no user notification. The creation 
of the `Global\_MSIExecute` mutex (which prevents two installs from 
running simultaneously) confirms an **active install sequence was 
initiated**. What was being installed was not captured within the 
sandbox execution window, but this pattern is consistent with 
**second-stage RAT or backdoor delivery** observed in known infostealer 
families. [See CAPE Sandbox Signatures — Section 5.3]

---

### Phase 5 — Anti-Forensic Cleanup

```text
Created then DELETED:
  HKEY_LOCAL_MACHINE\System\Acrobatviewercpp473
  HKEY_LOCAL_MACHINE\SYSTEM\Acrobatbrokerserverdispatchercpp789
```

These registry keys were **created and removed within the same execution 
session**. They do not exist in any legitimate Adobe documentation. Their 
naming mimics Adobe software to blend in with legitimate registry entries, 
while their deletion before session end is consistent with **anti-forensic 
artifact cleanup** — a standard technique to hinder post-incident 
investigation and timeline reconstruction.

---

### Confidence Assessment

| Finding | Confidence | Basis |
|---|---|---|
| Sandbox evasion active | ✅ High | Direct API call logs |
| DLL injection protection disabled | ✅ High | Registry write confirmed |
| Browser credential access attempted | ✅ High | File paths + DPAPI load confirmed |
| Windows Credential Vault accessed | ✅ High | VaultSvc service open confirmed |
| LSASS credential dumping | ⚠️ Medium | Process tree context only, no direct dump confirmed |
| Second-stage payload installed | ⚠️ Medium | msiexec spawned, payload not captured |
| Data successfully exfiltrated | ❌ Not confirmed | Evasion prevented full sandbox detonation |

> **Bottom line:** The behavioral evidence is consistent with an 
> **evasive infostealer dropper**. Complete execution was not observed 
> due to sandbox-aware timing logic. The combination of credential 
> access APIs, DLL protection removal, silent MSI execution, and 
> anti-forensic cleanup constitutes **sufficient grounds to classify 
> this file as malicious with high confidence**.

### 5.1 File Characteristics

Key metadata from sandbox and static inspection:

| Property | Value |
|----------|-------|
| Filename | `Offer_Letter_Manichand_Gupta.pdf` (also seen as `attachment.pdf`) |
| Size | 172.14 KB |
| Type | PDF document, version 1.7 |
| Pages | 4 |
| Language | English |
| Producer | **WeasyPrint 68.1** (Python HTML→PDF generator) |
| SHA256 | `21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4` |

The use of **WeasyPrint** rather than Word/Google Docs or a mainstream HRMS strongly suggests **programmatic, large‑scale generation of offer letters**, consistent with mass phishing or scam campaigns.

<img width="1399" height="439" alt="Screenshot 2026-04-12 144253" src="https://github.com/user-attachments/assets/f7f6b5c9-8817-4356-8a58-0c7fce881179" />


### 5.2 Antivirus vs Behavior Engines

- VirusTotal: **0/64 engines** detected the file as malicious at the time of analysis.
- ANY.RUN: default 60‑second run with “heavy evasion” disabled reported **no malicious or suspicious processes**.
- VirusTotal behavioral analysis (CAPE, Jujubox, Zenbox) recorded multiple **MITRE ATT&CK techniques**, process injections, and suspicious registry and file operations.

This divergence is explained by **anti‑analysis techniques** that prevent the payload from fully detonating under common sandbox conditions.

<img width="1906" height="1002" alt="Screenshot 2026-04-12 142605" src="https://github.com/user-attachments/assets/b187fccd-09af-42a9-8ee0-bcb9ec724d1b" />
<img width="1853" height="897" alt="Screenshot 2026-04-12 143217" src="https://github.com/user-attachments/assets/68e085a1-0c9b-4376-a568-04eb8b0b5dd9" />

## 5.2a MITRE ATT&CK Technique Mapping

| Tactic | Technique | ID | Evidence |
|---|---|---|---|
| Defense Evasion | Virtualization/Sandbox Evasion | T1497.001 | `IsDebuggerPresent`, `GetTickCount64`, `Sleep` |
| Defense Evasion | Process Injection | T1055 | `bBlockDLLInjection = 0` |
| Credential Access | OS Credential Dumping | T1003 | `lsass.exe`, `VaultSvc`, `DPAPI.dll` |
| Credential Access | Credentials from Password Stores | T1555.003 | Edge profile, cookies, Arcot IDs accessed |
| Execution | Windows Management Instrumentation | T1047 | `wmiprvse.exe` spawned |
| Execution | Exploitation for Client Execution | T1203 | Acrobat crash processor spawned 2x |
| Persistence | MSI-based Install | T1218.007 | `msiexec.exe /V` spawned silently |
| Discovery | Query Registry | T1012 | Extensive HKCU/HKLM reads |
| Discovery | System Information Discovery | T1082 | `GetAdaptersAddresses`, system fingerprinting |

### 5.3 Anti‑Analysis & Sandbox Evasion

Behavioral logs show repeated use of APIs typical for sandbox detection and timing evasion:

- `IsDebuggerPresent` — checks whether a debugger or analysis tool is attached.
- `GetTickCount` / `GetTickCount64` — measures elapsed time to detect accelerated clocks used by sandboxes.
- `Sleep` — delays execution long enough to exceed default sandbox timeouts.
- `GetAdaptersAddresses` — enumerates network interfaces, useful for identifying virtualized or atypical environments.

Together, these calls implement a **sandbox‑aware execution strategy**: behave benignly under quick automated analysis, then reveal full behavior only on real endpoints.

<img width="1823" height="701" alt="Screenshot 2026-04-12 143233" src="https://github.com/user-attachments/assets/80170695-9dd8-4b2d-8db4-8b6897218f28" />
<img width="1700" height="947" alt="Screenshot 2026-04-12 143718" src="https://github.com/user-attachments/assets/0236de3a-98e7-4311-a0cc-bcc599a098b8" />

### CAPE Sandbox Signature Classifications

| Severity | Signature | Implication |
|---|---|---|
| 🔴 Red (Malicious) | Creates suspended process | Injection preparation |
| 🔴 Red | Resumes thread in foreign process | Code injection |
| 🔴 Red | Writes to physical drive | Dangerous low-level access |
| 🟠 Orange (Suspicious) | WMI queries | Anti-VM detection |
| 🟠 Orange | Multiple user-agents in traffic | C2 masquerading |
| 🟠 Orange | Hidden window creation | Stealth execution |
| 🟢 Green (Info) | Reads own binary | Self-inspection |
| 🟢 Green | HTTP requests made | Network exfil possible |


### 5.4 Credential & System Reconnaissance

Behavioral artifacts indicate a strong focus on credentials and system profiling:

- **Services opened:** `VaultSvc` (Windows Credential Manager), `clipsvc` (clipboard), and other system services.
- **Modules loaded:** `DPAPI.dll` (Data Protection API), used to decrypt locally stored secrets, and browser/Outlook‑related DLLs.
- **Processes in tree:** `lsass.exe` appears in the broader context, aligning with credential dumping techniques (T1003) even if full interaction is not visible in short runs.
- **File access:** paths associated with **Edge browser profiles, cookies, Arcot IDs, and Windows credential storage** are opened, suggesting harvesting of stored credentials and tokens.

These operations go far beyond what is necessary for viewing a static PDF and are consistent with **infostealer behavior**.

<img width="1696" height="756" alt="Screenshot 2026-04-12 142820" src="https://github.com/user-attachments/assets/84df27b5-4287-4c4a-a005-7cf013cd0e7b" />
<img width="1887" height="891" alt="Screenshot 2026-04-12 143600" src="https://github.com/user-attachments/assets/fcbe940a-85a8-4629-86d6-af089b02085d" />
<img width="1582" height="431" alt="Screenshot 2026-04-12 143654" src="https://github.com/user-attachments/assets/973f861d-820d-43e0-bb64-e729f4fd3400" />


### 5.5 Process Injection Preparation

Registry and mutex activity show pre‑staging for process injection:

- Registry write: `SOFTWARE\Adobe\Acrobat Reader\DC\DLLInjection\bBlockDLLInjection = 0` — disables Adobe Reader’s DLL injection protection.
- Creation of global mutexes such as `Global\_MSIExecute` and installer‑related locks, consistent with planned use of **msiexec‑based payloads**.

Even if the injection is not fully observed within the sandbox window, disabling DLL injection safeguards is a strong indicator of **planned code injection into trusted processes**.

<img width="1646" height="788" alt="Screenshot 2026-04-12 144001" src="https://github.com/user-attachments/assets/5996ac92-91d5-4284-a67b-18763c47495d" />


### 5.6 Suspicious MSI Activity

Sandbox logs show the spawning of:

```text
C:\Windows\System32\msiexec.exe C:\Windows\system32\msiexec.exe /V
```

Under normal circumstances, opening a PDF should not trigger **Windows Installer**. The `/V` invocation suggests preparation for a **silent or parameterized install**, which could be used to deploy a second‑stage payload (e.g., a backdoor, RAT, or persistence agent).

### 5.7 Fake Adobe Registry Keys & Cleanup

Two registry keys are created and then deleted during execution:

- `HKEY_LOCAL_MACHINE\System\Acrobatviewercpp473`
- `HKEY_LOCAL_MACHINE\SYSTEM\Acrobatbrokerserverdispatchercpp789`

These keys do not appear in legitimate Adobe documentation and use naming patterns that blend Adobe terms with random suffixes. Their creation and removal during a single run suggest **staging artifacts or anti‑forensic cleanup**, which is typical of evasive malware.

### 5.8 Why ANY.RUN Reported “Clean”

ANY.RUN’s environment for this task used:

- A 60‑second execution window.
- Heavy evasion turned **off**.
- Standard Windows 10 image with Adobe installed.

Given the observed use of `Sleep` and timing‑based checks, it is likely that **malicious branches never executed within that time limit**, yielding a false sense of security. This highlights the importance of **extended, evasion‑aware sandbox runs** for PDF and document‑based malware.



***

<a id="combined-threat-model"></a>

## 6. Combined Threat Model

Bringing together the social engineering and technical vectors, Zorvyn’s operation can be modeled as follows:

1. **Attraction & Legitimacy Layer**  
   - High stipends, FinTech branding, polished offer letters, LinkedIn presence.

2. **Commitment & Work Extraction Layer**  
   - Time‑consuming assignments and tight deadlines bind candidates psychologically and create sunk‑cost feelings.

3. **Data Harvesting Layer**  
   - Onboarding portals and PDF clauses are used to solicit **banking, identity, and contact data**, shifting responsibility for accurate data onto the victim.

4. **Endpoint Compromise Layer**  
   - The offer‑letter PDF behaves like an **evasive infostealer dropper**, pre‑staging credential access, DLL injection, and msiexec‑based payload delivery.

5. **Potential Monetization Paths**  
   - Unauthorized financial transactions, fraudulent loan applications, credential resale, or use of harvested access for further intrusions (e.g., against universities or employers).

This layered approach explains why many victims report **no direct demand for upfront fees**; the primary value lies in **data and access**, not direct payment.

***

<a id="indicators-of-compromise"></a>

## 7. Indicators of Compromise (IOCs)

### 7.1 File Hashes

```text
MD5:    9F3E4A4BAF7005517EBABD71A70C884A
SHA1:   176D01AF0FBB0868AD13467751ECFB9791887D14
SHA256: 21A28029ACD9C884DF80D11C9F9D355D4C2E4B183A5D7E35F84CE3589B453BC4
```



### 7.2 Domains & Emails

```text
zorvyn.io
zorvyn.org
zorvyn.co
employeesupport.zorvyn.co
hrapi.zorvyn.org

hr@zorvyn.org
hr@zorvyn.co
onboarding@zorvyn.org
```



### 7.3 Behavioral & Configuration IOCs

- Adobe registry key: `SOFTWARE\Adobe\Acrobat Reader\DC\DLLInjection\bBlockDLLInjection = 0`.
- Rogue keys: `HKLM\System\Acrobatviewercpp473`, `HKLM\SYSTEM\Acrobatbrokerserverdispatchercpp789`.
- Suspicious processes when PDF opened: `Acrobat.exe`, `AcroCEF.exe`, `msiexec.exe`, `wmiprvse.exe`, interaction with `lsass.exe` context.
- Services opened: `VaultSvc`, `clipsvc`, `wscsvc`.
- Access to Edge profile files, cookies, Arcot IDs, and credential‑related directories.

### 7.4 JA3 & Network

VirusTotal behavior reports a specific **JA3 fingerprint** and a small set of TLS/HTTPS connections, primarily to Adobe and Microsoft infrastructure, which may serve as **cover traffic** for further actions. These network IOCs should be used in **conjunction with file and host indicators**, not in isolation.

JA3 TLS Fingerprint: cd08e31494f9531f560d64c695473da9

***

<a id="recommended-defensive-actions"></a>

## 8. Recommended Defensive Actions

### 8.1 For Individual Victims

- **Do not share further data** with any Zorvyn‑branded domain or email.
- **Reset passwords** for email, banking, and any accounts that might have been saved in the browser on the affected device.
- **Clear browser saved passwords and tokens**; consider migrating to a password manager with 2FA.
- Run **full AV + reputable anti‑malware scans**, preferably including an offline scan and a second opinion tool.
- Treat any unexplained bank, UPI, or loan activity as potentially linked and **notify the bank immediately**.
- File a complaint at **cybercrime.gov.in** and call the national cyber helpline **1930** where applicable.

### 8.2 For Universities & Training/Placement Cells

- Issue **formal advisories** warning students about Zorvyn‑branded offers and explaining how to verify company registrations via MCA and WHOIS.
- Integrate **basic OSINT checks** into placement workflows before circulating external internship opportunities.
- Encourage students to **report suspicious offers** centrally so patterns can be seen early.

### 8.3 For SOC / Blue‑Team Environments

- Add the **file hash and domain IOCs** to blocklists and EDR watchlists.
- Tune detections around:
  - Adobe Reader spawning **msiexec.exe**.
  - Adobe processes opening **VaultSvc**, DPAPI libraries, and LSASS‑adjacent activity.
  - Suspicious registry writes under `...\DLLInjection` and creation of Acrobat‑looking keys under HKLM\System.
- Extend sandbox runs for document files to **several minutes with evasion heuristics enabled**.

***

<a id="conclusion"></a>

> **🔎 Verify This Yourself**  
> Paste the SHA256 hash `21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4`  
> directly into [VirusTotal](https://www.virustotal.com) → Behavior tab.  
> Search "Zorvyn FinTech Private Limited" on [MCA.gov.in](https://www.mca.gov.in/mcafoportal/viewCompanyMasterData.do).

## 9. Conclusion

The Zorvyn FinTech internship campaign illustrates how **modern hiring scams blend believable corporate branding with technically sophisticated, evasive tooling**. Legal misrepresentation (use of “Pvt. Ltd.” without MCA registration), recent disposable domains, fabricated employee identities, and aggressive collection of banking and identity data form the **social and legal layer of the fraud**.

On the technical side, the offer‑letter PDF associated with this campaign behaves not like a static HR document but like an **evasive infostealer dropper**, pre‑positioned to harvest credentials and prepare process injection and MSI‑based payload delivery while defeating common sandbox setups.

Taken together, the evidence strongly supports treating Zorvyn‑branded offers as **high‑risk and potentially malicious**. Until the entity provides verifiable, jurisdiction‑appropriate registration details and a transparent record of genuine stipends and internships completed, the safest course of action for students and professionals is **complete avoidance and prompt reporting to cybercrime authorities**.

---

<a id="references"></a>

## References

1.  [VT_Scan](https://www.virustotal.com/gui/file/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4/behavior)

2. [any.run_reoprt.pdf](https://any.run/report/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4/cdb74be3-1bd9-4f93-add3-a18696fc6f13?_gl=1*qdzbg3*_gcl_au*NTI0MTk4ODguMTc3Mzg5NDAyMw..*FPAU*NTI0MTk4ODguMTc3Mzg5NDAyMw..*_ga*MTQyNzg5Njk2MS4xNzczODk0MDIw*_ga_53KB74YDZR*czE3NzU5ODUxNTAkbzQxJGcxJHQxNzc1OTg3NDIxJGo1MCRsMCRoMTc0ODMzMjA0Ng..) - File name: Offer_Letter_Manichand_Gupta.pdf [Full analysis](https://app.any.run/tasks/cdb74be3-1bd9-4f93-add3-a18696fc6f13)

3. [ZORVYN SCAM!!! CEO's FAKE EDUCATION DEGREE](https://www.reddit.com/r/InternshipsIndia/comments/1sg0g0n/zorvyn_scam_ceos_fake_education_degree/) - SCAM ALERT. Over the past few weeks, Zorvyn FinTech has been aggressively hiring interns with stipen...

4. [Mursalin Molla's Post](https://www.linkedin.com/posts/themursalinmolla_cybersecurity-jobscam-zorvynscam-activity-7448798613629046784-mzGK) - WARNING: Zorvyn FinTech is running a fake internship scam targeting students and freshers in India. ...

5. [Karan Rajeshbhai Mungara's Post](https://www.linkedin.com/posts/withkarann_freshers-indiajobs-jobseekers-activity-7448105735990861825-gN2h) - My sister received an offer letter from Zorvyn FinTech Pvt. Ltd. yesterday. ₹40,000/month stipend. F...

6. [Dhiraj K.'s Post](https://www.linkedin.com/posts/dhiraj-kushwaha_possible-hiring-scam-on-1st-april-i-received-activity-7447181988714954752-GqW2) - Possible Hiring Scam ⚠️ On 1st April, I received a mail from a company called "Zorvyn" saying I was ...

7. [Concerns over Zorvyn internship legitimacy](https://www.reddit.com/r/LegalAdviceIndia/comments/1sic5mo/concerns_over_zorvyn_internship_legitimacy/) - its a 6month remote intern with a 35-45k stipend per month based on role. now they responded with an...

8. [Sujal Tripathi's Post](https://www.linkedin.com/posts/sujaltripathi_zorvyn-zorvynfintech-internshipindia-activity-7448957310850400256-J-Qi) - 🚨 Zorvyn FinTech Internship — Sharing My Full Experience. Community, I Need Your Help. A few days ag...

9. [Zorvyn FinTech Ka Sach — Fake Internship Offer Letter ...](https://www.youtube.com/watch?v=nu3YNkkgO_k) - ... Zorvyn FinTech verify karo: mca.gov.in pe search karo "Zorvyn FinTech Private Limited" ✓ Cyber s...

10. [Zorvyn Internship Is Real Or Fake Quora](https://www.instagram.com/popular/zorvyn-internship-is-real-or-fake-quora/) -  Designation: Associate Software Engineer Education: BE / B.Tech Batch: 2023 / 2024 / 2025 CTC: ₹6 ...

11. [Is Zorvyn FinTech internship legit? Got an offer letter, need ...](https://www.reddit.com/r/IndiaInternshipDaily/comments/1sgvahg/is_zorvyn_fintech_internship_legit_got_an_offer/) - Yes their company is not registered in MCA (Ministry of Corporate Affairs).....did you check in the ...

12. [Bengaluru techie calls out 'hiring scam after spotting 'fake' ...](https://www.hindustantimes.com/trending/bengaluru-techie-calls-out-hiring-scam-after-spotting-fake-employee-profiles-dont-waste-your-time-101775650579679.html) - In a post on X, the techie claimed that a company called “Zorvyn” appeared suspicious after he was s...
