# 🚨 Uber Data Breach Report – 2022 Analysis
**👨‍🎓 Author:** Ahmed Rashwan  
**📅 Report Date:** 2024  

---

## 🚀 Executive Summary  
This report analyzes the Uber data breach that occurred on **September 15, 2022**, attributed to an 18-year-old threat actor allegedly affiliated with the **LAPSUS$ group**. The attacker gained access to Uber’s internal infrastructure through **social engineering** techniques and **MFA fatigue** attacks, exposing critical systems and services despite the use of multi-factor authentication.

---

## 🔍 Breach Incident Analysis  

### Initial Compromise  
The breach began with the compromise of an external Uber contractor’s device via malware, leading to leaked credentials. Despite MFA being enabled, the attacker used an **MFA fatigue attack**, persistently sending login prompts. Eventually, the contractor approved one, believing it was a legitimate request, especially after receiving a **spoofed WhatsApp message** claiming to be from Uber IT.

### Lateral Movement & Privilege Escalation  
Once inside, the attacker accessed Uber's internal VPN using the stolen credentials. Tools such as **Nmap** were likely used to enumerate the internal network. The attacker discovered a **network share** containing **PowerShell scripts** with **hardcoded credentials** for Uber’s **Thycotic Privileged Access Management (PAM)** system, enabling privilege escalation.

---

## 🛠 Compromised Services & Severity Breakdown

| Service          | Severity | Description                                                                 |
|------------------|----------|-----------------------------------------------------------------------------|
| Thycotic PAM     | Critical | Access to high-privilege credentials across internal services and AWS.     |
| AWS Instance     | Critical | Full control over applications, ability to exfiltrate or manipulate data.  |
| VMware vSphere   | Critical | Bridged cloud and on-premises infrastructure at risk of further breaches.  |
| SentinelOne      | High     | Potential for attacker to alter endpoint data or avoid detection.          |
| Slack Workspace  | Medium   | Internal messaging access, used for potential phishing or lateral moves.   |
| GSuite Admin     | Medium   | Admin console access to manage users and modify internal collaboration.    |
| HackerOne        | Medium   | Access to private vulnerability reports and proofs of concept.             |

**Additional Breached Services:**
- **Financial Data**: Accessed via `avengers.uberinternal.com`, exposing expense records.  
- **vSphere Client**: Access to virtual machine infrastructure.  
- **Google Workplace Admin Console**: Email and collaboration data at risk.  

---

## 🧱 Assets at Risk  
- **Employee Data**: Due to Thycotic PAM compromise.  
- **Cloud Infrastructure**: AWS services were fully accessible.  
- **Internal Communications**: Slack and Google Workspace compromised.  

---

## 👥 Affected Stakeholders  
- **Uber Shareholders**: Share price dropped by 5.2%.  
- **Customers**: Trust potentially damaged, despite no confirmed leak of user data.  
- **Employees**: Exposed credentials and operational disruption.  

---

## 📉 Impact on CIA Triad  

| CIA Property     | Impact Description                                                                 |
|------------------|-------------------------------------------------------------------------------------|
| Confidentiality  | **Severely impacted** due to extensive unauthorized data access.                   |
| Integrity        | **Potentially impacted** – attacker had the ability to modify sensitive data.      |
| Availability     | **Temporarily impacted** during incident response and service containment.         |

---

## 🛠 Techniques and Tools Used by the Attacker  
- **Social Engineering**: Core attack vector (MFA fatigue via WhatsApp).  
- **Malware**: Used to steal initial contractor credentials.  
- **Nmap**: Likely used for internal network scanning.  
- **SMBmap**: Assumed for enumerating Windows Share contents.  
- **Active Directory Explorer**: Used to navigate AD structures.  

---

## 🔒 Recommended Countermeasures  
- **Remove Hardcoded Credentials**: Prevent privilege escalation through insecure scripting.  
- **Strengthen PAM Authentication**: Add additional MFA layers or context-aware controls.  
- **Robust Credential Hygiene**: Enforce password rotation, use salting, and encrypt stored secrets.  
- **Employee Awareness Training**: Combat social engineering with regular simulations and training.  

---

## 📜 References  
- Browne, R. (2022). *CNBC*. [Uber Investigates Cybersecurity Incident](https://www.cnbc.com/2022/09/16/uber-investigates-cybersecurity-incident-after-reports-of-a-hack.html)  
- Jackson, M. (2022). *GitGuardian*. [Uber Breach 2022 – Everything You Need to Know](https://blog.gitguardian.com/uber-breach-2022/)  
- Sjouwerman, S. (2022). *KnowBe4*. [Uber Security Breach 'Looks Bad'](https://blog.knowbe4.com/)  
- Uber Team (2022). *Uber Newsroom*. [Security Update](https://www.uber.com/newsroom/security-update/)  
- Munir, M. Q. (Savitar0x01). [Twitter Post](https://twitter.com/Savitar0x01/status/1570580235716014081/photo/1)  
- vx-underground. [Twitter Post](https://twitter.com/vxunderground/status/1570598055560482817)  
