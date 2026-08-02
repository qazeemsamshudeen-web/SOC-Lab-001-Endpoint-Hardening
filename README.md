# SOC Lab #001: Endpoint Hardening & Privilege Management

**Defending the Perimeter: A Blue Team Investigation into Endpoint Security**  
**Author:** Qazeem Samshudeen Temitope  
**Role:** Aspiring SOC Analyst | Endpoint Security Enthusiast  
📄 **Full Presentation Report:** [![Download PDF](https://img.shields.io/badge/Download-Full_PDF_Report-blue?style=for-the-badge&logo=adobeacrobatreader)](./Qazeem-samshudeen-SOC-analyst-endpoint-hardening-lab-report.pdf)

---

## 📌 Executive Summary
This project demonstrates practical endpoint hardening on a simulated Windows environment by implementing the **Principle of Least Privilege (PoLP)** and **Identity Segregation**. The primary goal is to reduce the system's attack surface, prevent malware persistence, and limit potential lateral movement.

---

## 🛠️ Lab Execution & Evidence

### Phase 1: Identity Segregation
* **Concept:** Splitting daily operations from high-risk administrative power.
* **Action:** Created a dedicated, standalone local administrative account (`LocalAdmin`).
* **Security Result:** Demoted standard daily activities away from administrative credentials to neutralize credential harvesting risks.

<img width="653" height="243" alt="number3" src="https://github.com/user-attachments/assets/a6eae628-ea49-4327-8120-b4a5cbfd4612" />



### Phase 2: Privilege Demotion
* **Concept:** Removing root access from primary daily user accounts.
* **Action:** Lowered the primary profile (`QAZEEMADMIN`) authority level from *Administrator* to *Standard User*.
* **Security Result:** Stripped the active administrative token from daily operations, requiring explicit elevation for system-level changes.

<img width="1055" height="868" alt="Screenshot 7" src="https://github.com/user-attachments/assets/756fdf38-b166-47a6-a7d9-19b50522cbd5" />


### Phase 3: The Security Audit & Verification
* **Concept:** Verifying that file-system controls actively enforce boundary restrictions.
* **Action:** Attempted unauthorized access from the Standard User profile into restricted administrative directories (`C:\Users\QAZEEMADMIN`).
* **Result:** **AUDIT PASSED.** Windows NTFS intercepted the request and triggered a User Account Control (UAC) prompt, requiring an administrative password to proceed.

<img width="831" height="698" alt="KUSFHJFVJKLFVJNKFD" src="https://github.com/user-attachments/assets/b0a925a1-bdf0-4ec2-8bda-4314c691c294" />


---

## 📊 SOC Monitoring & Detection Perspective

Hardening is the **shield**, but active monitoring is the **eyes**. A SOC Analyst tracks key event log indicators to confirm these boundaries hold:

| Event ID | Focus Area | Description / Threat Vector |
| :--- | :--- | :--- |
| **Event ID 4720** | User Creation | Detects unauthorized account creation / backdoor accounts. |
| **Event ID 4625** | Failed Logon | Identifies potential Brute-Force attacks targeting `LocalAdmin`. |
| **Event ID 4672** | Special Privileges | Monitors standard user accounts triggering unexpected superuser rights. |

---

## 🔑 Key Takeaways
1. **Zero Trust Principles:** Trust is a vulnerability. Verifying actions through UAC Elevation establishes a defensible OS foundation.
2. **Effective Sandboxing:** Enforcing PoLP breaks malware persistence chains and prevents unauthorized Registry or Firewall alterations.
3. **Operational Hygiene:** Endpoint hardening is an ongoing auditing standard, not a one-time configuration.

---

## 💻 Environment & Tools Used
* **Operating System:** Windows 10/11 Home/Pro
* **Documentation & Design:** Canva
* **Forensic Evidence Capture:** Windows Snipping Tool
