# Threat Intelligence Report: APT41
- Written: January 14, 2025
- Updated: May 28, 2025
<br /><br />

## Executive Summary

APT41, also known as Wicked Panda, BARIUM, Brass Typhoon, Winnti, and HOODOO, is a prolific Chinese state-sponsored threat group active since at least 2012. Uniquely, APT41 blends state-directed cyber espionage with financially motivated cybercrime, targeting a wide spectrum of industries worldwide. The group’s operations demonstrate advanced technical capabilities, persistent access, and a notable ability to adapt their tactics, techniques, and procedures (TTPs) to evade detection and maximize impact. Recent campaigns highlight APT41’s innovative use of cloud services—including Google Calendar—for command-and-control (C2), and the deployment of new malware families such as TOUGHPROGRESS, PLUSDROP, and PLUSINJECT.
<br /><br />

## Attribution and Overview

- **Aliases:** Wicked Panda, BARIUM, Brass Typhoon, Winnti, HOODOO, Axiom, Blackfly, Bronze Atlas, Earth Baku, RedGolf, Red Kelpie, TA415
- **Assessed Sponsorship:** Chinese state, with some operations possibly outside direct state control
- **Active Since:** At least 2012
- **Primary Motivations:** Espionage (intellectual property, trade secrets, PII), Financial gain (ransomware, supply chain compromise, theft from gaming industry)
- **Target Sectors:** Healthcare, telecom, technology, finance, education, retail, logistics, automotive, video game industry, government entities, shipping, media, and entertainment

APT41 is unique among Chinese APTs for conducting financially motivated operations alongside state-sponsored espionage. The group has targeted organizations in at least 14 countries, including the United States, United Kingdom, France, Italy, India, Japan, South Korea, Switzerland, Turkey, Taiwan, Thailand, and others. Operations align with China’s Five-Year economic development plans and strategic initiatives such as “Made in China 2025,” but also include opportunistic campaigns for personal gain.
<br /><br />

## Recent Campaigns and Innovations

APT41 has recently demonstrated a high degree of innovation in their attack chains, particularly through the abuse of cloud services for C2 and the deployment of new malware families:

- **TOUGHPROGRESS:** In late 2024, APT41 leveraged a malware family dubbed TOUGHPROGRESS, distributed via spear-phishing emails linking to a ZIP archive hosted on a compromised government website. The archive contained a malicious LNK file disguised as a PDF and several JPG images, with “6.jpg” as an encrypted payload and “7.jpg” as a DLL used for decryption and execution.
- **Multi-stage Infection Chain:**
    - **PLUSDROP:** Decrypts and executes the next stage in memory.
    - **PLUSINJECT:** Performs process hollowing on svchost.exe to inject the final payload.
    - **TOUGHPROGRESS:** Communicates with attacker-controlled Google Calendar events for C2, embedding encrypted commands and exfiltrated data within event descriptions.
- **Technical Innovations:** The malware employs memory-only payloads, XOR-based encryption, LZNT1 compression, process hollowing, control flow obfuscation, and dynamic function resolution via custom hashing. It uses register-based indirect calls and 64-bit register overflow to evade static analysis.
- **Cloud Services Abuse:** APT41 has used Google Calendar, Sheets, and Drive for C2, as well as free web hosting (Cloudflare Workers, InfinityFree, TryCloudflare) to distribute malware.
<br /><br />

## Operations and Targeting

### Dual Mission: Espionage and Cybercrime

- **Espionage:**
    - Targets include healthcare (medical devices, pharmaceuticals, clinical trials), high-tech (semiconductors, cloud computing, advanced hardware), telecom, media, travel, education, government, and dissident groups.
    - Operations often coincide with major business events (e.g., M&A, market entry, political events).
    - APT41 has targeted dissidents and media organizations, including pro-democracy groups in Hong Kong and a Taiwanese media company.

- **Financially Motivated Activity:**
    - Persistent targeting of the video game industry (development studios, publishers, distributors), including source code theft, digital certificate compromise, virtual currency manipulation, ransomware deployment, and supply chain compromise.
    - Cryptocurrency theft and mining (e.g., Monero via XMRig).
    - Financial operations often occur outside standard Chinese working hours, indicating moonlighting.
<br /><br />

## Supply Chain Compromise

APT41 has executed multiple software supply chain compromises, injecting malicious code into legitimate software updates—sometimes signed with stolen certificates from targeted companies. Notable incidents include:

- 2014: Southeast Asian video game distributors (Path of Exile, League of Legends, FIFA Online 3) – SOGU backdoor.
- 2017: NetSarang software (ShadowPad) – POISONPLUG.SHADOW.
- 2018: ASUS Live Update utility (ShadowHammer) – POISONPLUG, highly targeted by MAC address.
- 2018: East/Southeast Asian game distributors (Infestation, PointBlank) – CRACKSHOT backdoor.
- 2024–2025: Use of stolen code-signing certificates from South Korean and Russian gaming/tech companies to sign DUSTTRAP and related malware.
<br /><br />

## Attack Lifecycle

APT41’s operations typically follow this lifecycle:

1. **Initial Compromise:**
    - Spear-phishing (often with .chm attachments or ZIP archives containing LNK files), exploitation of public-facing applications, supply chain compromise, valid accounts, remote access tools, and web shells.
2. **Establish Foothold:**
    - Deployment of web shells (ANTSWORD, BLUEBEAM, CHINACHOP, ASPXSpy), custom and public malware (HIGHNOON, SOGU, Gh0st, BEACON/Cobalt Strike, DUSTPAN), credential theft, masquerading as antivirus software.
3. **Privilege Escalation:**
    - Use of tools like Mimikatz, ACEHASH, GEARSHIFT; exploitation of Windows Credential Editor, password hash dumping, account manipulation; advanced kernel manipulation (targeting ntoskrnl.exe).
4. **Internal Reconnaissance:**
    - Built-in Windows commands, custom tools (WIDETONE, HIGHNOON, SOGU), enumeration of users, groups, and network topology.
5. **Lateral Movement:**
    - RDP, SMB, scheduled tasks, compromised accounts, WMIEXEC, DLL side-loading, registry/service modification.
6. **Persistence:**
    - Backdoors, bootkits (ROCKBOOT), rootkits (Adore-NG), registry modifications, scheduled tasks, startup files, PowerShell, Sticky Keys vulnerability; DUSTTRAP DLL trojanizing and service creation.
7. **Complete Mission:**
    - Data exfiltration (RAR archives, custom tools), manipulation of in-game or cryptocurrency assets, ransomware deployment, anti-forensics (log/command history clearing), and C2 via legitimate platforms (Google Calendar, Google Drive, GitHub, Pastebin, Steam, Microsoft TechNet).
<br /><br />

## Technical Toolset

*APT41 uses a broad arsenal of malware, including:*

- **Backdoors/RATs:** HIGHNOON, SOGU, POISONPLUG, CROSSWALK, Gh0st, ZXSHELL, HOMEUNIX, PHOTO, XDOOR, PACMAN, HKDOOR, DEADEYE, DOWNTIME, WINTERLOVE, BEACON, TOUGHPROGRESS.
- **Credential Theft:** Mimikatz, ACEHASH, GOODLUCK.
- **Keyloggers:** GEARSHIFT.
- **Loaders/Downloaders:** CRACKSHOT, EASYNIGHT, LATELUNCH, SWEETCANDLE, LOWKEY, TIDYELF, DUSTPAN, PLUSDROP, PLUSBED.
- **Rootkits/Bootkits:** Adore-NG, ROCKBOOT, FRONTWHEEL.
- **Web Shells:** ANTSWORD, BLUEBEAM, CHINACHOP, ASPXSpy.
- **Crypto-miners:** XMRig.
- **Ransomware:** Encryptor RaaS.
- **Supply Chain Implants:** POISONPLUG.SHADOW, POISONPLUG, CRACKSHOT.
- **Data Exfiltration:** SQLULDR2, PINEGROVE.
<br /><br />

*Recent Malware Details:*

- **DUSTPAN:** In-memory dropper, loads BEACON payloads encrypted with chacha20, disguised as Windows binaries, made persistent via Windows services.
- **DUSTTRAP:** Multi-stage plugin framework, uses AES-128-CFB encryption, trojanizes legitimate DLLs, advanced evasion (restores original DLL contents after malicious code is loaded).
- **PINEGROVE:** Command-line uploader for exfiltrating data to OneDrive.
- **SQLULDR2:** Used for exporting Oracle database contents.
- **TOUGHPROGRESS:** Uses Google Calendar for C2, with modules for decryption, process hollowing, and encrypted command/result exchange via calendar events.
<br /><br />

## Tactics, Techniques, and Procedures (TTPs)

- **Initial Access:** Spear-phishing (attachments, malicious LNKs), supply chain compromise, exploiting public-facing applications, valid accounts, external remote services.
- **Execution:** Command-line, PowerShell, scheduled tasks, DLL hijacking, web shells, process hollowing (PLUSINJECT).
- **Persistence:** Registry run keys, bootkits, new services, scheduled tasks, web shells, account manipulation, DLL trojanizing (DUSTTRAP).
- **Privilege Escalation:** Credential dumping, token manipulation, process injection, kernel exploitation, accessibility features.
- **Defense Evasion:** Obfuscated files, code signing (stolen certificates), indicator removal, process hollowing, rootkits, memory-only payloads, dynamic hashing.
- **Credential Access:** Brute force, credential dumping, input capture.
- **Discovery:** Account discovery, permission groups, process and network discovery, system info gathering.
- **Lateral Movement:** Pass-the-hash, RDP, SMB, remote file copy.
- **Collection:** Keylogging, screen capture, data from local and networked systems.
- **Exfiltration:** Compression, encryption, C2 channels (including Google Calendar and OneDrive), cloud storage.
- **Impact:** Data encryption (ransomware), cryptocurrency mining.
<br /><br />

## Infrastructure and Evasion

- **C2 Channels:** Use of legitimate services (Google Calendar, Google Drive, GitHub, Pastebin, Steam, Microsoft TechNet), custom domains, dead drop resolvers, cloud-based C2 (Cloudflare Workers, OneDrive), DNS tunneling, DGA.
- **Masquerading:** Files and domains named after antivirus vendors, legitimate Windows binaries, and public cloud infrastructure.
<br /><br />

## Attribution Details

- **Identified Operators:** Personas “Zhang Xuguang” and “Wolfzhi,” both with a history of underground forum activity and domain registrations linked to APT41 operations; evidence of moonlighting.
- **Contractor Model:** Evidence suggests APT41 members may operate as contractors, working both for the state and for personal financial gain.
- **Shared Resources:** Overlaps in malware families, code-signing certificates, and infrastructure with other Chinese APTs (e.g., APT17, APT20, APT40).
<br /><br />

## Indicators of Compromise (IOCs)

- **File Hashes:** (See annex for full list; notable recent hashes include those for TOUGHPROGRESS, PLUSDROP, 6.jpg, 7.jpg, DUSTTRAP, DUSTPAN, PINEGROVE, SQLULDR2).
- **Domains:** ageofwuxia[.]com, byeserver[.]com, dnsgogle[.]com, notped[.]com, xigncodeservice[.]com, *.workers.dev, *.trycloudflare.com, www[.]eloples[.]com.
- **Email Addresses:** akbklxp@126[.]com, hackershby@126[.]com, hrsimon59@gmail[.]com, etc.
- **URLs/Platforms:** Google Calendar, Google Drive, Google Docs, Steam Community pages, Pastebin, Microsoft TechNet, Cloudflare Workers.
- **YARA Rules:** Detection rules for TOUGHPROGRESS, PLUSDROP, PLUSBED, DUSTTRAP, DUSTPAN, PINEGROVE, SQLULDR2 (see annex).
<br /><br />

## Defensive Recommendations

- Monitor for web shell activity and suspicious service creation.
- Audit use of code-signing certificates and block known abused certificates.
- Inspect for abnormal outbound connections to cloud services and dead drop resolvers.
- Patch internet-facing applications promptly, especially for known exploited vulnerabilities.
- Deploy network and endpoint monitoring for behavioral detection (lateral movement, process injection, memory-only payloads).
- Review for signs of supply chain compromise and unauthorized software updates.
- Monitor for abuse of cloud services (Google Workspace, OneDrive, Cloudflare Workers) as C2 channels.
- Apply YARA rules for recent malware families and monitor for relevant IOCs.
<br /><br />

## Conclusion

APT41 exemplifies the blurred lines between state-sponsored espionage and cybercrime. Their dual mission, technical sophistication, and willingness to innovate—such as leveraging Google Calendar for C2 and rapidly adopting new malware—make them one of the most dangerous and unpredictable threat actors globally. Defenders should remain vigilant for both targeted espionage and opportunistic financial campaigns, and closely track new TTPs, cloud service abuse, and emerging malware linked to this group.
<br /><br />

## References

- MITRE ATT&CK: [Group G0096 (APT 41)](https://attack.mitre.org/groups/G0096/)
- Madiant: [APT41, A Dual Espionage and Cyber Crime Operation (PDF)](https://services.google.com/fh/files/misc/apt41-a-dual-espionage-and-cyber-crime-operation.pdf)
- Google Cloud Blog: [APT41 Dual Espionage and Cyber Crime Operation](https://cloud.google.com/blog/topics/threat-intelligence/apt41-dual-espionage-and-cyber-crime-operation)
- Google Cloud Blog: [Mark Your Calendar: APT41 Innovative Tactics](https://cloud.google.com/blog/topics/threat-intelligence/apt41-innovative-tactics)
- Resecurity: [APT41 Threat Intelligence Report and Malware Analysis](https://www.resecurity.com/blog/article/apt-41-threat-intelligence-report-and-malware-analysis)
- The Hacker News: [Chinese APT41 Exploits Google Calendar for Malware Command-and-Control Operations](https://thehackernews.com/2025/05/chinese-apt41-exploits-google-calendar.html)
- Google Cloud Blog: [APT41 Has Arisen From the DUST](https://cloud.google.com/blog/topics/threat-intelligence/apt41-arisen-from-dust)
