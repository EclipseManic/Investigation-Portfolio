# 🔍 SOC & Fraud Investigation: Zorvyn FinTech Remote Internship Campaign

> **Analyst:** Manichand Gupta  
> **Date:** 12 April 2026  
> **Scope:** Technical malware analysis, fraud modus operandi, and company OSINT profile for Zorvyn FinTech “internship” offers  
> **Verdict:** High‑risk scam operation with evasive malware and financial/identity data harvesting intent

***


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

Multiple Indian students and freshers have reported receiving highly attractive remote internship offers from an entity calling itself **“Zorvyn FinTech Pvt. Ltd.”**, typically promising **₹35–45K/month stipends and PPOs up to ₹11–14 LPA** for roles such as Cybersecurity Analyst, Data Analyst, Frontend Developer, and Backend Developer. Public OSINT and sandbox analysis of one such **offer-letter PDF** (SHA256 `21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4`) show that the campaign combines **social engineering, legal misrepresentation, evasive malware behavior, and aggressive collection of banking and identity data**.[^1][^2][^3][^4][^5]

Although **0/64 antivirus engines on VirusTotal** flagged the file as malicious, behavioral sandboxes mapped multiple MITRE ATT&CK tactics, including **sandbox evasion, credential access, and process injection staging**. ANY.RUN’s default 60‑second run also reported "No threats detected", consistent with deliberate **timing‑based evasion**.[^5][^6]

OSINT further shows that Zorvyn:
- **Has no CIN registration on India’s MCA portal** despite using the legal suffix “Pvt. Ltd.” in offer letters and emails.[^3][^4][^1]
- Operates across **multiple inconsistent domains** (`zorvyn.io`, `zorvyn.org`, `zorvyn.co`) with **recent registrations** that do not match its claimed founding year of 2022.[^4][^1]
- Uses **fake or highly suspicious LinkedIn employee profiles** and AI‑generated office imagery to simulate legitimacy.[^2][^7][^4]
- Asks selected candidates to submit **bank account details, Aadhaar, PAN and full home address before any verified onboarding**, framed as “stipend processing” and “welcome kit” workflows.[^8][^9][^4]

The combined evidence indicates a **high‑risk, likely fraudulent operation** whose primary objectives are **credential theft and financial/identity data harvesting**, rather than genuine employment.

***

<a id="case-context-timeline"></a>

## 2. Case Context & Timeline

### 2.1 Typical Candidate Journey

Across Reddit, LinkedIn posts, and YouTube analyses, the following pattern emerges:[^10][^1][^2][^4][^8]

1. **Mass Outreach & Hiring Posts**  
   - LinkedIn and job platforms show large‑scale hiring for multiple internship roles with **30–45K monthly stipends and high PPOs**, often claiming **“120+ interns”** being onboarded.[^3][^10]
   - Application is usually via LinkedIn Easy Apply, Internshala, or similar platforms.[^10]

2. **Screening Assignment Instead of Proper Interviews**  
   - Many candidates report **no real technical interview**, only a time‑bound assignment (e.g., 100 MCQs in 120 minutes, or a full React dashboard build).[^8][^3][^10]
   - Assignments often require **3–12 hours of work**, with no guaranteed feedback.[^1][^3]

3. **Polished Offer Letter with Unrealistic Benefits**  
   - Selected candidates receive a **highly polished 4‑page offer letter** on “Zorvyn FinTech Pvt. Ltd.” letterhead, listing generous stipend, WFH arrangement, and PPO at 11–14 LPA.[^9][^4][^3]
   - The PDF is signed by a “CEO” and includes NDAs, confidentiality clauses, HR policies, and sometimes **FinTech‑style language about payment processing and compliance**.[^4][^9]

4. **Urgency & Deadline Pressure**  
   - Candidates are often given **24 hours or less** to sign and return the offer, or emails are sent **after the stated deadline**, creating panic and limiting verification time.[^9]

5. **Onboarding Portals Demanding Sensitive Data**  
   - Email onboarding flows contain portal links asking for **bank account details, IFSC, Aadhaar, PAN, full home address, and sometimes device preferences** (keyboard, mouse, T‑shirt size) under the pretext of stipend disbursal and welcome kits.[^4][^8][^9]
   - Some flows explicitly state that **“banking and payment details will be collected”** and that the candidate is **“solely responsible for ensuring that the payment information provided is accurate.”**[^9]

6. **Silence, Moving Goalposts, or Domain Changes**  
   - Many interns report doing assignments and signing letters but **never receiving clear joining details, stipend payment, or verifiable HR contacts**.[^1][^8][^10]
   - Domain changes (e.g., `zorvyn.io` to `zorvyn.org`) break previous portals, meaning candidates cannot access submissions or see application status.[^10][^1]

### 2.2 Analyst’s Specific Sample

The sample investigated here is a PDF offer letter named **`Offer_Letter_Manichand_Gupta.pdf`** (title in metadata: “Internship Offer Letter | Zorvyn FinTech Pvt. Ltd.”) that was subsequently re‑submitted to sandboxes under generic names such as `attachment.pdf`.[^6][^5]

ANY.RUN’s 60‑second analysis reported *“No malicious indicators”* and 0 suspicious processes, while VirusTotal’s behavioral engines (CAPE, Jujubox, Zenbox) detected extensive suspicious activity despite 0/64 AV detections.[^6][^5]

[^6]

***

<a id="company-infrastructure-osint-profile"></a>

## 3. Company & Infrastructure OSINT Profile

### 3.1 Claimed Identity vs Legal Reality

Zorvyn markets itself consistently as **“Zorvyn FinTech Pvt. Ltd.”**, a FinTech firm claiming to have been **“Empowering Financial Innovation Since 2022”**. However, independent checks show the following:[^1][^10]

| Check | Observation | Source |
|------|-------------|--------|
| MCA (India) CIN search for “Zorvyn FinTech Pvt. Ltd.” | **No company record found** on the Ministry of Corporate Affairs portal. | [^1][^4][^10] |
| Right to use “Pvt. Ltd.” in India | Legally reserved for entities registered with MCA and assigned a CIN; using it without registration is misrepresentation. | [^1][^4] |
| Company’s explanation | HR replies to candidates claim Zorvyn is **registered in the UAE**, therefore “no CIN,” while still signing communication as “Pvt. Ltd.” in India. | [^7][^8][^11] |
| UAE entity verification | Candidates and independent researchers report **no verifiable UAE trade license or registration number** publicly shared. | [^7][^8][^10] |

This mismatch between **legal form claimed (Indian Pvt. Ltd.)** and **registration story (foreign UAE entity)** is a strong red flag and matches typical patterns in cross‑border hiring scams.

[Figure Placeholder F1: MCA portal search result showing "No matching results found" for Zorvyn query.]

### 3.2 Domain Footprint & Timeline

Community WHOIS checks and public posts provide the following timeline:[^4][^10][^1]

| Domain | Claimed narrative | Observed registration evidence |
|--------|-------------------|--------------------------------|
| `zorvyn.io` | Initially presented as the “official” company site; later described as suspended due to mass reporting campaigns. | Public WHOIS shows registration around **March 2025**, not 2022, and external scanners (e.g., ScamDetector, ScamAdviser) flagged risk concerns.[^1][^10] |
| `zorvyn.org` | Later primary domain; used in email addresses (`hr@zorvyn.org`) and internship pages. | Registered in **April 2026**, again contradicting the 2022 founding claim.[^1][^4] |
| `zorvyn.co` | Appears in onboarding URLs (e.g., `employeesupport.zorvyn.co`); sometimes cited as “employee support” subdomain. | Separate ccTLD with its own registration; used mainly for submission portals and onboarding flows.[^9] |

These domain patterns support the assessment that **infrastructure is opportunistic and reactive**, not that of a long‑standing regulated FinTech firm.

[Figure Placeholder F2: WHOIS record for zorvyn.io showing creation date 2025-03-25.]
[Figure Placeholder F3: WHOIS record for zorvyn.org showing creation date 2026-04-06.]
[Figure Placeholder F4: WHOIS record for zorvyn.co showing creation date 2026-04-06.]

### 3.3 Fake Employee & Office Persona Construction

Investigations by students, Reddit users, and a Bengaluru engineer covered by mainstream media reveal several anomalies:[^7][^12][^2]

- **LinkedIn employees** such as multi‑year Zorvyn veterans and C‑level executives show **improbable timelines**, such as an “IIT 2015 graduate” only creating a LinkedIn profile in 2025.[^12]
- Some “employees” reuse **stock or AI‑generated profile pictures** and have thin or erratic work histories, with little activity beyond liking Zorvyn posts.[^2][^4]
- Shared “office” photos were later admitted by Zorvyn to be sourced from a **commercial design/AI agency**, not an actual Zorvyn office.[^1]

These inconsistencies indicate a deliberate attempt to **simulate corporate legitimacy using fabricated digital personas**.

***

<a id="social-engineering-banking-identity-data-strategy"></a>

## 4. Social Engineering & Banking / Identity Data Strategy

### 4.1 Psychological Hooks

Zorvyn’s messaging is fine‑tuned to Indian fresher psychology:[^3][^9][^10][^4]

- **High stipend (₹35–45K/month) + PPO up to ₹11–14 LPA** for interns with minimal interviews.
- **Full remote WFH** with flexible hours, highly attractive to non‑metro students.
- **Branded FinTech positioning** suggesting cutting‑edge work in finance and payments.
- **Strict NDAs and legalistic language** in offer letters to make the opportunity feel scarce and premium.

The combination of **status, money, and urgency** is designed to suppress skepticism and push candidates to sign quickly.

### 4.2 Data Collection Flow

From multiple victims’ descriptions and offer/onboarding screenshots:[^8][^9][^4]

1. **Offer Letter Clauses**  
   The PDF explicitly states that Zorvyn will **collect “banking and payment details”** from the intern and that the intern is **responsible for ensuring payment information is accurate**.[^9]

2. **Onboarding Portal**  
   After acceptance, candidates receive credentials (sometimes transmitted in plaintext email) to an **employee portal** where they are required to enter:
   - Full name, date of birth, phone number, and permanent address.
   - Bank account number, IFSC code, and sometimes UPI ID.
   - Aadhaar and PAN details ostensibly for KYC and stipend processing.[^8][^4][^9]

3. **Welcome Kit & Equipment Narrative**  
   Some flows mention **T‑shirt size, peripherals (keyboard, mouse)** and shipping addresses for “welcome kits”, which normalizes the request for precise residential data.[^4]

4. **No Transparent Payment History**  
   Despite hundreds of reported offer letters and long assignments, OSINT yields **no credible, independently verifiable reports of consistent stipend payouts and internship completion certificates**, which would be expected if this were a genuine large‑scale program.[^10][^8][^1]

### 4.3 Likely Fraud Objectives

Based on these patterns, combined with evasive malware behavior in the PDF, the campaign likely targets:

- **Bank account takeover and fraudulent transactions** using collected account details and potential SIM‑swap or social engineering of banks.[^9]
- **Identity theft** — Aadhaar and PAN allow creation of **synthetic identities** or unauthorized loans/credit lines.[^9]
- **Credential harvesting** via the PDF’s suspicious behavior (VaultSvc, DPAPI, browser profile access), harvesting saved browser passwords and corporate credentials.[^5][^6]
- **Monetization of free labor** by having students complete complex assignments that could be repurposed without paying them, although the primary risk appears to be data abuse.[^3][^10][^1]

This aligns with a **dual‑track fraud model**: one track harvesting personal/financial data, the other extracting unpaid technical work.

***

<a id="technical-analysis-offer-letter-pdf"></a>

## 5. Technical Analysis of the Offer-Letter PDF

### 5.1 File Characteristics

Key metadata from sandbox and static inspection:[^5][^6]

| Property | Value |
|----------|-------|
| Filename | `Offer_Letter_Manichand_Gupta.pdf` (also seen as `attachment.pdf`) |
| Size | 172.14 KB |
| Type | PDF document, version 1.7 |
| Pages | 4 |
| Language | English |
| Producer | **WeasyPrint 68.1** (Python HTML→PDF generator) |
| SHA256 | `21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4` |

The use of **WeasyPrint** rather than Word/Google Docs or a mainstream HRMS strongly suggests **programmatic, large‑scale generation of offer letters**, consistent with mass phishing or scam campaigns.[^6]

[Figure Placeholder F5: Static information panel showing PDF version 1.7, page count 4, and producer WeasyPrint 68.1.]

### 5.2 Antivirus vs Behavior Engines

- VirusTotal: **0/64 engines** detected the file as malicious at the time of analysis.[^5]
- ANY.RUN: default 60‑second run with “heavy evasion” disabled reported **no malicious or suspicious processes**.[^6]
- VirusTotal behavioral analysis (CAPE, Jujubox, Zenbox) recorded multiple **MITRE ATT&CK techniques**, process injections, and suspicious registry and file operations.[^5]

This divergence is explained by **anti‑analysis techniques** that prevent the payload from fully detonating under common sandbox conditions.

[Figure Placeholder F6: VirusTotal file summary showing 0/64 detections with grouped sandbox reports enabled.]
[Figure Placeholder F7: Activity summary panel showing MITRE signatures, dropped files, and network communications.]

[^5]

### 5.3 Anti‑Analysis & Sandbox Evasion

Behavioral logs show repeated use of APIs typical for sandbox detection and timing evasion:[^6][^5]

- `IsDebuggerPresent` — checks whether a debugger or analysis tool is attached.
- `GetTickCount` / `GetTickCount64` — measures elapsed time to detect accelerated clocks used by sandboxes.
- `Sleep` — delays execution long enough to exceed default sandbox timeouts.
- `GetAdaptersAddresses` — enumerates network interfaces, useful for identifying virtualized or atypical environments.

Together, these calls implement a **sandbox‑aware execution strategy**: behave benignly under quick automated analysis, then reveal full behavior only on real endpoints.

[Figure Placeholder F8: Highlighted anti-analysis API calls (IsDebuggerPresent, GetTickCount, GetTickCount64, Sleep, GetAdaptersAddresses).]
[Figure Placeholder F9: Malware behavior/signatures panel showing anti-virtualization and evasion indicators.]

### 5.4 Credential & System Reconnaissance

Behavioral artifacts indicate a strong focus on credentials and system profiling:[^5]

- **Services opened:** `VaultSvc` (Windows Credential Manager), `clipsvc` (clipboard), and other system services.
- **Modules loaded:** `DPAPI.dll` (Data Protection API), used to decrypt locally stored secrets, and browser/Outlook‑related DLLs.
- **Processes in tree:** `lsass.exe` appears in the broader context, aligning with credential dumping techniques (T1003) even if full interaction is not visible in short runs.
- **File access:** paths associated with **Edge browser profiles, cookies, Arcot IDs, and Windows credential storage** are opened, suggesting harvesting of stored credentials and tokens.

These operations go far beyond what is necessary for viewing a static PDF and are consistent with **infostealer behavior**.

[Figure Placeholder F10: Process tree showing Acrobat.exe, AcroCEF.exe, wmiprvse.exe, and lsass.exe context.]
[Figure Placeholder F11: Shell/Executed commands listing from sandbox summary.]
[Figure Placeholder F12: Processes extra info panel (Acrobat.exe, msiexec.exe, AcroCEF.exe with PIDs and parent PIDs).]

### 5.5 Process Injection Preparation

Registry and mutex activity show pre‑staging for process injection:[^5]

- Registry write: `SOFTWARE\Adobe\Acrobat Reader\DC\DLLInjection\bBlockDLLInjection = 0` — disables Adobe Reader’s DLL injection protection.
- Creation of global mutexes such as `Global\_MSIExecute` and installer‑related locks, consistent with planned use of **msiexec‑based payloads**.

Even if the injection is not fully observed within the sandbox window, disabling DLL injection safeguards is a strong indicator of **planned code injection into trusted processes**.

[Figure Placeholder F13: Registry keys set/deleted showing bBlockDLLInjection and rogue Acrobat* keys.]

### 5.6 Suspicious MSI Activity

Sandbox logs show the spawning of:

```text
C:\Windows\System32\msiexec.exe C:\Windows\system32\msiexec.exe /V
```

Under normal circumstances, opening a PDF should not trigger **Windows Installer**. The `/V` invocation suggests preparation for a **silent or parameterized install**, which could be used to deploy a second‑stage payload (e.g., a backdoor, RAT, or persistence agent).[^5]

### 5.7 Fake Adobe Registry Keys & Cleanup

Two registry keys are created and then deleted during execution:

- `HKEY_LOCAL_MACHINE\System\Acrobatviewercpp473`
- `HKEY_LOCAL_MACHINE\SYSTEM\Acrobatbrokerserverdispatchercpp789`

These keys do not appear in legitimate Adobe documentation and use naming patterns that blend Adobe terms with random suffixes. Their creation and removal during a single run suggest **staging artifacts or anti‑forensic cleanup**, which is typical of evasive malware.[^5]

### 5.8 Why ANY.RUN Reported “Clean”

ANY.RUN’s environment for this task used:

- A 60‑second execution window.
- Heavy evasion turned **off**.
- Standard Windows 10 image with Adobe installed.[^6]

Given the observed use of `Sleep` and timing‑based checks, it is likely that **malicious branches never executed within that time limit**, yielding a false sense of security. This highlights the importance of **extended, evasion‑aware sandbox runs** for PDF and document‑based malware.

[^6]

***

<a id="combined-threat-model"></a>

## 6. Combined Threat Model

Bringing together the social engineering and technical vectors, Zorvyn’s operation can be modeled as follows:

1. **Attraction & Legitimacy Layer**  
   - High stipends, FinTech branding, polished offer letters, LinkedIn presence.[^3][^1][^4]

2. **Commitment & Work Extraction Layer**  
   - Time‑consuming assignments and tight deadlines bind candidates psychologically and create sunk‑cost feelings.[^1][^3]

3. **Data Harvesting Layer**  
   - Onboarding portals and PDF clauses are used to solicit **banking, identity, and contact data**, shifting responsibility for accurate data onto the victim.[^8][^4][^9]

4. **Endpoint Compromise Layer**  
   - The offer‑letter PDF behaves like an **evasive infostealer dropper**, pre‑staging credential access, DLL injection, and msiexec‑based payload delivery.[^6][^5]

5. **Potential Monetization Paths**  
   - Unauthorized financial transactions, fraudulent loan applications, credential resale, or use of harvested access for further intrusions (e.g., against universities or employers).[^9][^5]

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

- Adobe registry key: `SOFTWARE\Adobe\Acrobat Reader\DC\DLLInjection\bBlockDLLInjection = 0`.[^5]
- Rogue keys: `HKLM\System\Acrobatviewercpp473`, `HKLM\SYSTEM\Acrobatbrokerserverdispatchercpp789`.[^5]
- Suspicious processes when PDF opened: `Acrobat.exe`, `AcroCEF.exe`, `msiexec.exe`, `wmiprvse.exe`, interaction with `lsass.exe` context.[^5]
- Services opened: `VaultSvc`, `clipsvc`, `wscsvc`.[^5]
- Access to Edge profile files, cookies, Arcot IDs, and credential‑related directories.[^5]

### 7.4 JA3 & Network

VirusTotal behavior reports a specific **JA3 fingerprint** and a small set of TLS/HTTPS connections, primarily to Adobe and Microsoft infrastructure, which may serve as **cover traffic** for further actions. These network IOCs should be used in **conjunction with file and host indicators**, not in isolation.[^6][^5]

***

<a id="recommended-defensive-actions"></a>

## 8. Recommended Defensive Actions

### 8.1 For Individual Victims

- **Do not share further data** with any Zorvyn‑branded domain or email.
- **Reset passwords** for email, banking, and any accounts that might have been saved in the browser on the affected device.[^9]
- **Clear browser saved passwords and tokens**; consider migrating to a password manager with 2FA.
- Run **full AV + reputable anti‑malware scans**, preferably including an offline scan and a second opinion tool.[^5]
- Treat any unexplained bank, UPI, or loan activity as potentially linked and **notify the bank immediately**.
- File a complaint at **cybercrime.gov.in** and call the national cyber helpline **1930** where applicable.[^1][^9]

### 8.2 For Universities & Training/Placement Cells

- Issue **formal advisories** warning students about Zorvyn‑branded offers and explaining how to verify company registrations via MCA and WHOIS.[^3][^1]
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

## 9. Conclusion

The Zorvyn FinTech internship campaign illustrates how **modern hiring scams blend believable corporate branding with technically sophisticated, evasive tooling**. Legal misrepresentation (use of “Pvt. Ltd.” without MCA registration), recent disposable domains, fabricated employee identities, and aggressive collection of banking and identity data form the **social and legal layer of the fraud**.[^12][^3][^4][^1]

On the technical side, the offer‑letter PDF associated with this campaign behaves not like a static HR document but like an **evasive infostealer dropper**, pre‑positioned to harvest credentials and prepare process injection and MSI‑based payload delivery while defeating common sandbox setups.[^6][^5]

Taken together, the evidence strongly supports treating Zorvyn‑branded offers as **high‑risk and potentially malicious**. Until the entity provides verifiable, jurisdiction‑appropriate registration details and a transparent record of genuine stipends and internships completed, the safest course of action for students and professionals is **complete avoidance and prompt reporting to cybercrime authorities**.[^10][^4][^1][^9]

---

<a id="references"></a>

## References

1. [report.md] -

2. [any.run_reoprt.pdf](https://any.run/report/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4/cdb74be3-1bd9-4f93-add3-a18696fc6f13?_gl=1*qdzbg3*_gcl_au*NTI0MTk4ODguMTc3Mzg5NDAyMw..*FPAU*NTI0MTk4ODguMTc3Mzg5NDAyMw..*_ga*MTQyNzg5Njk2MS4xNzczODk0MDIw*_ga_53KB74YDZR*czE3NzU5ODUxNTAkbzQxJGcxJHQxNzc1OTg3NDIxJGo1MCRsMCRoMTc0ODMzMjA0Ng..) - File name: Offer_Letter_Manichand_Gupta.pdf [Full analysis](https://app.any.run/tasks/cdb74be3-1bd9-4f93-add3-a18696fc6f13)

    [VT_Scan](https://www.virustotal.com/gui/file/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4/behavior)

    [Zenbox](https://vtbehaviour.commondatastorage.googleapis.com/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4_Zenbox.html?GoogleAccessId=758681729565-rc7fgq07icj8c9dm2gi34a4cckv235v1@developer.gserviceaccount.com&Expires=1775987873&Signature=cxRnWFUb3ZfFDcTXPc3kMD6UGnzbah0MgxgwgueGcynRU3DDhLDUOZ9J%2BZWa7AD%2F1c7jI%2FeruenIPWDHtkv1OkHVQvde%2FhUmOmUQy8I9YDruVUoe4gHYs8cB9apl8OTkmYuD5bLWf6dSW2IiYj5p8ImAGH6SDrcV5d7iC2KwjIeyygg%2FJVUYQ5UPj3955RGCBgZiY6P%2Fq7QvtT6QAo8oeitcZv5c2X4EGhoomlLHEZQ9KbosMS%2B%2FsXNFOic6V6tmVAM3NoK6RT%2FXqZBEOpESqOVTmn2kS0Razr1U%2BZwpQPbe6mXWD9LZEmxTB9WVzwesPsAm6E8mJFgGxcJg%2F0ya%2Bw%3D%3D&response-content-type=text%2Fhtml;)

    [VirusTotal Jujubox](https://vtbehaviour.commondatastorage.googleapis.com/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4_VirusTotal%20Jujubox.html?GoogleAccessId=758681729565-rc7fgq07icj8c9dm2gi34a4cckv235v1@developer.gserviceaccount.com&Expires=1775987901&Signature=ZlvZJmkC9qJdDe%2BbRaFY2NgABT0AB9VPE7zASTu8MK7G5wCtclD%2BimW9ifi5av2Qui5XJGZCwbc96kflqaQYcc9NMY%2Bie2T4V%2BDkxZFyTL1uJ%2B1Y%2Fgf6uNmftQkYX%2BOoN02dqlh6OLh8CpY99XkSOaJz7ffGW3wKEXFJGPu9gUOmAIdxAVrY3Rydkv7UyZA2fo%2BTDG%2FWioRThbcJ75lIRqHYHp%2FRKUO4nc3IFzrIxXbpFpsQwrwwQR%2BhEAhzpxvAC3L6xIR0VHi%2BX%2BuFt5Jq9Fib77fMuNTOmjX7XcydT7ONu0aUimX8hrsozmsweicCmj8hBHM238719kLSgsiAbw%3D%3D&response-content-type=text%2Fhtml;)

    [CAPE Sandbox](https://vtbehaviour.commondatastorage.googleapis.com/21a28029acd9c884df80d11c9f9d355d4c2e4b183a5d7e35f84ce3589b453bc4_CAPE%20Sandbox.html?GoogleAccessId=758681729565-rc7fgq07icj8c9dm2gi34a4cckv235v1@developer.gserviceaccount.com&Expires=1775987926&Signature=rae%2BEsE40X8c%2FvWrNtHgG2qZn%2Bi31vjeAR%2BqyYbDViAuMgVVXWuzqULWBYJnjNgLbpqyThQLNX2WXu6qXNzkrg7hqHQ2XdLabHjrwPW6bpUPfiK%2FeIe2miNVv5N0zSNl9KYU5tZ87WXeJVPXJiupTypMfhxQWFWN8HCOaPX%2BFK4nNux3uqbT2DERSIy0BOi2vnajSt6WQN%2FbRSx4TInWm4veDRYLNDXFoin1xvOAgmjo55Gxk0EkyJzogIOQamlH5scpbBBoEwEYiGw%2B17tYY2LS3JpTNkPg7k9aemXQQCExlLPOFPEH%2BVzYEquP91x85L2gUnOY8jBKzsaLFQ1whg%3D%3D&response-content-type=text%2Fhtml;)
    

3. [ZORVYN SCAM!!! CEO's FAKE EDUCATION DEGREE](https://www.reddit.com/r/InternshipsIndia/comments/1sg0g0n/zorvyn_scam_ceos_fake_education_degree/) - SCAM ALERT. Over the past few weeks, Zorvyn FinTech has been aggressively hiring interns with stipen...

4. [Mursalin Molla's Post](https://www.linkedin.com/posts/themursalinmolla_cybersecurity-jobscam-zorvynscam-activity-7448798613629046784-mzGK) - WARNING: Zorvyn FinTech is running a fake internship scam targeting students and freshers in India. ...

5. [Karan Rajeshbhai Mungara's Post](https://www.linkedin.com/posts/withkarann_freshers-indiajobs-jobseekers-activity-7448105735990861825-gN2h) - My sister received an offer letter from Zorvyn FinTech Pvt. Ltd. yesterday. ₹40,000/month stipend. F...

6. [Dhiraj K.'s Post](https://www.linkedin.com/posts/dhiraj-kushwaha_possible-hiring-scam-on-1st-april-i-received-activity-7447181988714954752-GqW2) - Possible Hiring Scam ⚠️ On 1st April, I received a mail from a company called "Zorvyn" saying I was ...

7. [Concerns over Zorvyn internship legitimacy](https://www.reddit.com/r/LegalAdviceIndia/comments/1sic5mo/concerns_over_zorvyn_internship_legitimacy/) - its a 6month remote intern with a 35-45k stipend per month based on role. now they responded with an...

8. [Sujal Tripathi's Post](https://www.linkedin.com/posts/sujaltripathi_zorvyn-zorvynfintech-internshipindia-activity-7448957310850400256-J-Qi) - 🚨 Zorvyn FinTech Internship — Sharing My Full Experience. Community, I Need Your Help. A few days ag...

9. [Zorvyn FinTech Ka Sach — Fake Internship Offer Letter ...](https://www.youtube.com/watch?v=nu3YNkkgO_k) - ... Zorvyn FinTech verify karo: mca.gov.in pe search karo "Zorvyn FinTech Private Limited" ✓ Cyber s...

10. [Zorvyn Internship Is Real Or Fake Quora](https://www.instagram.com/popular/zorvyn-internship-is-real-or-fake-quora/) - ‍ Designation: Associate Software Engineer Education: BE / B.Tech Batch: 2023 / 2024 / 2025 CTC: ₹6 ...

11. [Is Zorvyn FinTech internship legit? Got an offer letter, need ...](https://www.reddit.com/r/IndiaInternshipDaily/comments/1sgvahg/is_zorvyn_fintech_internship_legit_got_an_offer/) - Yes their company is not registered in MCA (Ministry of Corporate Affairs).....did you check in the ...

12. [Bengaluru techie calls out 'hiring scam after spotting 'fake' ...](https://www.hindustantimes.com/trending/bengaluru-techie-calls-out-hiring-scam-after-spotting-fake-employee-profiles-dont-waste-your-time-101775650579679.html) - In a post on X, the techie claimed that a company called “Zorvyn” appeared suspicious after he was s...

