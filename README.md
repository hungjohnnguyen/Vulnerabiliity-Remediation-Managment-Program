# Vulnerability Management Program Implementation

In this project, we simulate the implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  
[Draft Policy](https://docs.google.com/document/d/1tx2xxKo-FgmGyjub9MSgKi6hk2ujimTsSfu4dRnroBc/edit?tab=t.0#heading=h.wzer8el0objm)

### Step 2) Mock Meeting: Policy Buy-In (Stakeholders)

This phase simulates a stakeholder meeting designed to secure buy-in from the server team for the proposed Vulnerability Management Policy. The purpose is twofold:

Introduce the draft policy — outlining its scope, responsibilities, and remediation timelines for vulnerabilities of varying severity.
Assess operational feasibility — ensuring the remediation expectations are realistic and achievable given the team’s resources, testing procedures, and business continuity needs.
The meeting begins with the Security Lead presenting the policy, emphasizing its role in reducing risk exposure for critical systems and safeguarding sensitive client data. The server team is invited to share practical concerns, especially regarding the short turnaround time for critical vulnerability remediation.
Through discussion, it becomes clear that the original 48-hour remediation window for critical vulnerabilities may be impractical due to testing, change management processes, and the potential impact on production environments. The team collectively agrees to extend the window to one week, with an emergency override clause for high-risk situations requiring immediate patching.

By the end of this phase:

The policy draft is adjusted collaboratively to balance security requirements with operational realities.
Stakeholders feel heard and invested, improving the likelihood of policy adoption.
Next steps include revising the document to reflect changes and preparing it for upper management review.
[Mock Meeting Transcript](https://docs.google.com/document/d/1EqCftRpALkrcHu-LwlWhAWxDiDP7upBpc4gj_DD5uwI/edit?tab=t.0)
 
  <img src="https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/vulnerabilitypolicybuyin.png" alt="image" width="400">
</div>


### Step 3) Policy Finalization and Senior Leadership Sign-Off

After collecting feedback from the server team, adjustments were made to ensure the policy was realistic and achievable in daily operations. In particular, remediation timelines were revised to balance security urgency with operational feasibility.
Following revisions, the policy was submitted to senior leadership for final review and approval. Once signed off, it became the official guiding document for the organization’s vulnerability management program.

Key Outcomes:

Incorporated cross-team feedback to improve practical implementation.
Adjusted aggressive remediation timelines to align with resource constraints while maintaining compliance.
Obtained executive approval, giving the policy authority for enforcement and reference in pushback scenarios.
  
[Finalized Policy](https://docs.google.com/document/d/1SGi0z2lfUgrIGqCaSvyBk8TQcluz-hSMR0twnRnOP7E/edit?tab=t.0)
<div style="text-align: center;">
    <img src="https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/Policyfinalizationandseniorleadershipsighnoff.png" alt="image" width="400">
</div>

---

## Step 4) Mock Meeting: Initial Scan Permission (Server Team)

As part of the vulnerability management rollout, the security team met with the server team to discuss initiating credentialed scans.  

<details>
  <summary>📝 Transcript (click to expand)</summary>

**Context:**  
The goal of this session was to address server team concerns, establish trust in the scanning process, and agree on how to safely begin credentialed vulnerability scans.  

---

**[Hung Nguyen, Security Lead]:** Thanks for joining today. As part of our vulnerability management rollout, we’d like to begin credentialed scanning on the servers. Before we dive in, we want to make sure your team is comfortable with the process.  

**[Jordan, Server Admin]:** Understood. Our main concern is the performance impact on production systems. We can’t risk downtime during critical business hours.  

**[Hung Nguyen, Security Lead]:** Absolutely. To address that, we propose starting with just one server. This way, we can monitor CPU, memory, and network impact before rolling it out further.  

**[Priya, Server Admin]:** Which server are you thinking of?  

**[Hung Nguyen, Security Lead]:** We’d suggest starting with a non-critical server in the staging environment, unless you’d prefer a low-risk production server.  

**[Jordan, Server Admin]:** Staging makes sense. We can afford a little more flexibility there. But we’ll need to make sure access is properly controlled.  

**[Hung Nguyen, Security Lead]:** Agreed. We’ll be using Just-In-Time (JIT) Active Directory credentials. That means the account only exists for the duration of the scan and is automatically removed afterwards. This way, no standing privileges exist.  

**[Priya, Server Admin]:** That helps. How often are you planning to run these scans?  

**[Hung Nguyen, Security Lead]:** For the pilot, just once. If resource impact is minimal, we’ll discuss moving to a regular schedule—likely weekly or biweekly.  

**[Jordan, Server Admin]:** Alright, let’s proceed with a single scan on staging using JIT credentials. But please share the resource usage report afterward.  

**[Hung Nguyen, Security Lead]:** Absolutely. We’ll document findings, scan duration, and performance logs, then review them with your team.  

**[Jordan, Server Admin]:** Perfect. Let’s schedule it after business hours tomorrow.  

**[Hung Nguyen, Security Lead]:** Sounds good. Thanks, everyone—this is a solid step toward improving visibility without disrupting operations.  

---

### 📌 Outcome
- **Decision:** Approved pilot credentialed scan on staging server.  
- **Safeguards:** JIT Active Directory credentials, monitoring CPU/memory/network usage.  
- **Next Steps:** Run pilot scan after business hours; share performance/resource report with server team.  

</details>
<div style="text-align: center;">
    <img src= "https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/Initalscanmeeting.png" alt="image" width="400">
</div>
---

### Step 5) Initial Scan of Server Team Assets

In this phase, a deliberately vulnerable Windows Server instance is provisioned to represent the server team’s environment. The system is intentionally misconfigured and outdated to introduce common security weaknesses, including missing patches, insecure services, and legacy protocols. Once the environment is prepared, an authenticated vulnerability scan is conducted using temporary credentials to replicate real-world conditions and ensure accurate detection. The scan results are then exported in a sanitized report, which serves as the foundation for prioritizing risks, documenting remediation efforts, and tracking improvements in subsequent phases of the project.

<img width="635" alt="image" src="https://github.com/user-attachments/assets/937cccbd-36bb-4445-97b9-e915085cda81" style="border: 2px solid black;">

[Scan 1 - Initial Scan](https://github.com/hungjohnnguyen/Vulnerabiliity-Remediation-Managment-Program/blob/main/finalprojectscan-john_initialscan.pdf)




---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

## Step 7) Distributing Remediations to Remediation Teams

In this step, remediation scripts and reports are distributed to the server team to streamline their remediation efforts.  

<details>
  <summary>📧 Mock Email: Vulnerability Remediation Scripts for Testing and Deployment (click to expand)</summary>

---

**Subject:** Vulnerability Remediation Scripts for Testing and Deployment  

Hi Team,  

Following the results of our initial vulnerability scan and assessment, we have prepared a set of remediation scripts to streamline the mitigation process. These scripts address several high-priority issues and are designed for easy integration into your existing deployment platforms (e.g., SCCM).  

Before pushing these changes into production, please conduct thorough testing in your staging environment to validate functionality and confirm compatibility with your systems.  

### Vulnerabilities and Remediations Addressed
- **Third-Party Software Removal:** Automated removal of Wireshark to reduce unnecessary attack surface.  
- **Windows OS Secure Configuration:**  
  - Disable insecure protocols.  
  - Remove/disable weak cipher suites.  
  - Review and restrict Guest account group membership.  

Your feedback will be critical to ensuring these remediations are both effective and minimally disruptive. Please share any issues or observations after testing so we can refine the scripts prior to the full rollout.  

Thank you for your prompt attention to this effort.  

Best regards,  
**[Hung Nguyen]**  
Security Operations  

---

### 📷 Email Screenshot (Mockup)

![Email Template](https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/vulnerabilityemail.png)
</details>


---

## Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

After running the initial vulnerability discovery scan, the server team gathered to review the findings.  

<details>
  <summary>📝 Transcript (click to expand)</summary>

**Context:**  
The goal of this session was to validate identified issues, discuss remediation approaches, and prepare remediation packages for submission to the Change Control Board (CAB).

---

**[Hung Nguyen, Security Lead]:** Thank you all for joining. Today’s focus is the results of our initial discovery scan. Overall, the scan flagged outdated software versions, insecure user accounts, and several deprecated protocols still in use.  

**[Server Admin 1]:** Yes, I noticed multiple servers still running older versions of Java and a few legacy applications with embedded dependencies. We’ll need to schedule upgrades or replacements.  

**[Server Admin 2]:** On the accounts side, the scan flagged some inactive service accounts that still have elevated privileges. Disabling those should be a quick win.  

**[Jordan, Security Analyst]:** Correct. We also saw deprecated protocols — specifically SMBv1 and TLS 1.0 — enabled on some Windows servers. Those configurations need to be updated as part of our hardening efforts.  

**[Hung Nguyen, Security Lead]:** Good observations. The remediation scripts for removing outdated software and disabling insecure protocols are ready. We’ll also include a package to restrict the flagged accounts.  

**[Server Admin 1]:** Understood. We’ll test those remediation packages in staging first, then prepare them for CAB review.  

**[Server Admin 2]:** Agreed. Once CAB approves, we can schedule deployment during the next maintenance window.  

**[Hung Nguyen, Security Lead]:** Perfect. Let’s finalize the remediation packages and submit them to CAB this week. Thank you, everyone.  

---

### 📌 Outcome
- **Identified Issues:** Outdated software, insecure accounts, deprecated protocols.  
- **Next Steps:** Remediation packages prepared and readied for CAB submission.  
- **Owner:** Server Team, with oversight from Security Operations.  

</details>


## Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed the plan to remove insecure protocols and weak cipher suites.  

<details>
  <summary>📝 Transcript (click to expand)</summary>

**Context:**  
The CAB convened to review and approve the remediation plan addressing insecure protocols and weak cipher suites. The proposal included a rollback script and a phased (tiered) deployment approach to minimize operational risk.

---

**[CAB Chair]:** Welcome, everyone. Today’s agenda is the remediation plan targeting insecure protocols and deprecated cipher suites. Security Ops, can you brief us on the proposal?  

**[Hung Nguyen, Security Lead]:** Certainly. Our scans identified systems still running SMBv1 and TLS 1.0, along with several weak cipher suites. The remediation package disables those settings. We’ve also included a rollback script in case critical services encounter issues.  

**[Server Admin]:** We validated the package in staging. Everything worked as expected, and the rollback process restores original settings within minutes.  

**[Application Owner]:** Any concerns about compatibility with legacy applications?  

**[Server Admin]:** A few legacy apps are flagged for extra testing. None are business-critical, and we have the rollback safeguard if needed.  

**[CAB Chair]:** And the deployment strategy?  

**[Hung Nguyen, Security Lead]:** Tiered rollout—start with non-critical servers, monitor stability/performance, then move to critical systems after validation.  

**[CAB Member]:** Are monitoring and reporting in place?  

**[Hung Nguyen, Security Lead]:** Yes. We’ll review logs daily and provide CAB updates after each wave.  

**[CAB Chair]:** With rollback and phased deployment, risk is acceptable. Any objections?  

**[CAB Members]:** None.  

**[CAB Chair]:** Approved. Proceed as outlined and report after each phase.

---

### 📌 Outcome
- **Decision:** CAB approved remediation plan.  
- **Scope:** Disable SMBv1, TLS 1.0, and weak cipher suites.  
- **Safeguards:** Rollback script + tiered deployment.  
- **Next Steps:** Begin phased rollout, monitor, and report progress to CAB.

</details>


---
### Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to uninstall the outdated version of Wireshark from the systems. A follow-up vulnerability scan verified that the removal was successful and the issue had been resolved.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  

<img width="634" alt="image" src="https://github.com/user-attachments/assets/7b4f9ab2-d230-4458-ac0f-c0ff070ae79a">

[Scan 2 - Wireshark Removal](https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/finalprojectscan-wiresharkremeidiation72khw.pdf)


#### Remediation Round 2: Insecure Protocols & Ciphers

The server team leveraged PowerShell scripts to disable insecure protocols and remove weak cipher suites. A subsequent vulnerability scan confirmed that the configurations had been successfully updated, and the scan results were documented for future reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)

<img width="630" alt="image" src="https://github.com/user-attachments/assets/0e96120d-8ec9-4f76-8e42-79c752200010">

[Scan 3 - Ciphersuites and Protocols](https://github.com/hungjohnnguyen/Vulnerability-Remediation-Managment-Program/blob/main/finalprojectscan-john_scan3.pdf)


#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1jVgikjfrV1YjOcL3QRT_oUB0Y82w22V7/view?usp=drive_link)


#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1tmDjeHl5uiGitRwWy8kFRi33q-nGi1Zt/view?usp=drive_link)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="https://github.com/user-attachments/assets/51f0aae8-7f36-4d90-b29f-5257e57155f9">

[Remediation Data](https://docs.google.com/spreadsheets/d/1FTtFfZYmFsNLU6pm8nTzsKyKE-d2ftXzX_DPwcnFNfA/edit?gid=0#gid=0)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
