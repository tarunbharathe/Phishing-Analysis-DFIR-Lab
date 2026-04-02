# Phishing Forensics & Incident Response Lab
## Technical Analysis of Modern Phishing Vectors (Quishing & Malicious Macros)

###  Project Objective
This lab documents the end-to-end investigation of two sophisticated phishing attack lifecycles. The goal was to simulate a Tier 1/2 SOC Analyst workflow: triaging alerts, correlating logs in a SIEM, performing host-based forensics, and neutralizing threats via network containment.

---

###  Technical Stack
*   **SIEM/Log Management:** Sysmon (Event IDs 1, 3, 22), Windows Event Logs.
*   **Endpoint Security:** EDR Simulation (Process Tree Analysis, Host Isolation).
*   **Threat Intelligence:** VirusTotal, AbuseIPDB, IPFS Gateway analysis.
*   **Forensics Tools:** ZXing (QR Decoding), CyberChef.

---

###  Case Study #1: SOC251 - Quishing (QR Code Phishing)
**Scenario:** An employee received a high-urgency email regarding a "Mandatory MFA Update."
*   **Key Findings:** 
    *   **Evasion:** Attackers utilized a QR code to hide the malicious URL from standard email gateway scanners.
    *   **Infrastructure:** The QR code resolved to a decentralized **IPFS (InterPlanetary File System)** gateway (`ipfs.io`), leveraging a legitimate domain's reputation to bypass filters.
*   **Result:** **True Positive.** Intercepted before credential harvest.
*   **[Screenshots located in /Case-01-Quishing]**

---

###  Case Study #2: SOC205 - Malicious Macro Execution
**Scenario:** A suspicious "Invoice" document was executed on a finance department workstation.
*   **Key Findings:**
    *   **Chain of Infection:** Malicious `.docm` file utilized VBA macros to spawn `powershell.exe`.
    *   **C2 Communication:** Analyzed **Sysmon Event ID 22 (DNS Query)** to identify a callback to a malicious Command & Control (C2) domain: `www.greyhathacker.net`.
*   **Result:** **True Positive.** Infection neutralized via network isolation.
*   **[Screenshots located in /Case-02-Macros]**

---

###  Global Mitigation Strategy
Based on these investigations, the following "Defense in Depth" controls were proposed:
1.  **ASR Rules:** Implement Attack Surface Reduction rules to block Office apps from creating child processes.
2.  **DNS Filtering:** Block known decentralized storage gateways (IPFS.io) unless required for business.
3.  **User Awareness:** Targeted training on "Quishing" (QR Phishing) and the risk of mobile-vector attacks.

---

**Analyst:** [Tarun Bharathe]
**Environment:** LetsDefend SOC Simulation
