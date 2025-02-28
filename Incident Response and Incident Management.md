# Incident Response and Incident Management.


A structured breakdown of the Incident Response:

---

### Incident Response Overview
- **Definition**: The technical aspect of dealing with an incident.
- **Primary Question**: "What happened?"
- **Responsibility**: The incident response team investigates using techniques and technologies.

---

### Initial Investigation
- **Starting Point**: Often begins in the Security Operations Center (SOC) by reviewing event-triggered alert information.
- **Tools Providing Alerts**:
  1. **EDR or AV Alert**:
     - Detects anomalous activity on a specific host.
     - Example: Alert for attempts to monitor a user’s keystrokes.
  2. **Network Tap Alert**:
     - Detects anomalous network activity.
     - Example: Alert for a host scanning other hosts in the network.
  3. **SIEM Alert**:
     - Security Information and Event Management system.
     - Alerts based on custom rules created by analysts.
     - Example: "Impossible travel" rule (user account logged in from two countries simultaneously).

- **Alert Information**:
  - Provides detailed data for analysts to review.
  - Example (SIEM): Includes recent logon events + historical logon data (e.g., past few months).

---

### When Alert Information Isn’t Enough
- **Next Step**: Digital Forensics
- **Definition**: A hands-on investigation to gather additional information.
- **Techniques**:
  1. **Hard Disk Recovery**:
     - From infected host.
     - Purpose: Investigate how malware was introduced.
  2. **Volatile Memory Recovery**:
     - From infected host’s RAM.
     - Purpose: Analyze how the malware operates.
  3. **System and Network Log Recovery**:
     - From multiple devices.
     - Purpose: Determine how malware spread.

---

### Goal of Incident Response
- **Objective**: Understand the **scope** of the incident accurately.
- **Importance of Scope**:
  - Links to Incident Management process for closing the incident.
- **Risks of Misjudging Scope**:
  1. **Overestimating Scope**:
     - Leads to drastic, unnecessary actions.
     - Impact: Disrupts business operations.
  2. **Underestimating Scope**:
     - Leads to insufficient actions.
     - Impact: Threat actor remains active; incident persists.

---
.



---

### Incident Management Overview
- **Definition**: The process aspect of dealing with an incident.
- **Primary Question**: "How do we respond to what happened?"
- **Prerequisite**: Understanding the scope of the incident (from Incident Response).

---

### Key Responsibilities of Incident Management
1. **Triaging the Incident**:
   - Update incident severity as new information emerges.
   - Involve additional stakeholders (e.g., Subject Matter Experts - SMEs) to assist.

2. **Guiding Actions with Playbooks**:
   - Use predefined playbooks to direct incident response actions.

3. **Deciding Actions**:
   - Determine strategies for:
     - **Containment**: Limit the incident’s spread.
     - **Eradication**: Remove the threat.
     - **Recovery**: Restore normal operations.

4. **Managing Communication**:
   - Decide what information to communicate:
     - **Internally**: To team members and stakeholders.
     - **Externally**: To clients, public, or regulators.

5. **Documenting the Incident**:
   - Record key details:
     - Actions taken.
     - Effects of those actions on resolving the incident.

6. **Closing the Incident**:
   - Finalize the incident response.
   - Analyze information to improve future processes and procedures.

---

### Importance of Incident Management
- **Effective Response**: Requires both Incident Response (technical) and Incident Management (process).
- **Common Misconception**: Technical skills alone are not enough; management is equally critical.

---



![image](https://github.com/user-attachments/assets/a2ee096a-50ab-4da3-b2eb-90c6ca30da6d)
![image](https://github.com/user-attachments/assets/cfca1c49-925c-4b50-a82c-c82dbe021732)


![dcab2ddeb05cd1300a0d2142d87b447e](https://github.com/user-attachments/assets/7bb32ac3-597b-4561-a5e4-02b7f36ceac6)


 **Preparation**, **Detection and Analysis**, **Containment, Eradication, and Recovery**, and **Post-Incident Activity**, 
---

### Preparation
- **Importance**: Critical for effective incident handling; reduces damage by enabling quick, accurate responses under stress.
- **Goal**: Minimize mistakes during incidents by being well-prepared.
- **Preparation Steps**:
  1. **Identify and Document Stakeholders**:
     - Key contacts and call trees for use during incidents.
  2. **Create and Update Playbooks**:
     - Guides for handling known incident types.
  3. **Conduct Exercises**:
     - Tabletop exercises and cyber war games to test team readiness.
  4. **Threat Hunting**:
     - Continuously search for threats to develop new alert rules based on attacker techniques.

---

### Detection and Analysis
- **Purpose**: Answer "What has happened?" (Primary phase of Incident Response).
- **Triage**: Often a middle step to assess severity (incorporated into this phase in NIST framework).
- **Severity**: Determines if an alert becomes an incident and its level.
- **Actions**:
  1. **Review Alerts**:
     - Check AV, EDR, and SIEM dashboards.
  2. **Forensic Investigation**:
     - Analyze system and network artifacts.
  3. **Malware Analysis**:
     - Study malware to understand behavior and create detection signatures.
- **Outcome**: Blue team provides scope details to the incident manager.

---

### Containment, Eradication, and Recovery
- **Purpose**: Address the incident (Primary phase of Incident Management).
- **Sub-Phases** (Order Matters):
  1. **Containment**:
     - Goal: "Stop the bleed" – prevent incident from worsening.
     - Example: Block threat actor access.
  2. **Eradication**:
     - Goal: Remove threat actor from the environment.
     - Example: Eliminate malware or compromised accounts.
  3. **Recovery**:
     - Goal: Restore normal operations (Business as Usual - BAU).
     - Example: Recover affected systems.
- **Why Order Matters**:
  - Eradication or recovery before containment allows threat actor to persist (e.g., re-compromising credentials via Active Directory).
- **Cyclic Nature**:
  - Phases 2 (Detection/Analysis) and 3 (Containment/Eradication/Recovery) loop:
    - Full scope isn’t known initially; actions start while investigation continues.
    - Effects of actions inform further steps until BAU is restored.

---

### Post-Incident Activity
- **Purpose**: Evaluate the incident to improve future responses.
- **Process**:
  - Review what happened.
  - Identify lessons learned.
  - Update processes, playbooks, and preparedness for next incident.
- **Key Idea**: Incident closure isn’t the end; learning enhances future resilience.

---

### Additional Notes
- **NIST Framework**: Combines triage into Detection and Analysis.
- **Cyclic Process**: Actions and investigation run concurrently until resolution.
- **Task**: Open and complete the static site to demonstrate understanding of the incident management process.

---

---

### Common Pitfalls Overview
- **Context**: Pitfalls can occur before, during, or after an incident, impacting response effectiveness.

---

### 1. Insufficient Hardening
- **Definition**: Skipping security best practice configurations post-deployment.
- **Cause**: Prioritizing speed/profits over security; security seen as a hindrance.
- **Process**:
  - Hardening: Adjusts initial configurations to align with security standards.
  - Often skipped after deployment.
- **Impact**:
  - Increases likelihood of incidents.
  - Most stopped early, but one successful incident can be costly.
- **Solution**:
  - Perform hardening during development (Shift Left principle – from Secure SDLC).
  - Don’t skip hardening post-deployment.

---

### 2. Insufficient Logging
- **Definition**: Inadequate collection of log data for alerting and analysis.
- **Cause**:
  - Cost of SIEM data ingestion (charged by throughput).
  - Expensive to send logs from remote devices (e.g., ATMs over mobile networks).
- **Impact**:
  - "Flying blind" – blue team lacks visibility.
  - Limited retention on local devices; threat actors may erase logs.
  - Late detection or inability to determine incident scope.
- **Consequence**: Incidents detected only after impact occurs.

---

### 3. Insufficient- and Over-Alerting
- **Definition**: Poor alert management in SIEM systems.
- **Issues**:
  1. **Insufficient Alerting**:
     - Too much data; no actionable alerts (needle in haystack).
     - Solution: Threat hunting to create useful alerts.
  2. **Over-Alerting**:
     - Too many false positives create noise ("cry wolf").
     - Team ignores alerts, missing real incidents.
- **Solution**: Optimize signal-to-noise ratio in alerts via threat hunting.
- **Impact**: Delayed response until significant impact occurs.

---

### 4. Insufficient Determination of Incident Scope
- **Definition**: Failing to accurately assess the incident’s full extent.
- **Challenge**: Full scope often unknowable initially; best efforts required.
- **Impact**:
  - **Underestimation**: Insufficient actions; threat actor persists.
  - **Overestimation**: Drastic actions disrupt business unnecessarily.
- **Solution**: No quick fix; requires continuous team preparation and skill development.

---

### 5. Insufficient Accountability
- **Definition**: Actions discussed but not executed due to lack of ownership.
- **Cause**: No one assigned responsibility; assumption actions are done.
- **Impact**: Incident grows as no containment/eradication occurs.
- **Solution**:
  - Effective Incident Management:
    - Document actions.
    - Assign responsible individuals.
    - Require feedback post-action.

---

### 6. Insufficient Backups
- **Definition**: Lack of reliable, isolated backups for recovery.
- **Cause**:
  - Poor backup policies/processes.
  - Over-reliance on High Availability Disaster Recovery (DR) systems.
- **Impact**:
  - Ransomware can replicate to DR if not isolated.
  - No recovery option if backups fail or are inaccessible.
- **Solution**: Maintain offline/remote backups alongside modern DR systems.

---

### Key Takeaways
- **Prevention**: Address hardening, logging, and backups before incidents.
- **Response**: Improve alerting, scope determination, and accountability during incidents.
- **Task**: Open and play the static site game to practice overcoming these pitfalls.

---


 To summarise:

    Incidents are a part of life. Incidents will happen, and therefore we need to prepare to deal with them.
    Not all events and alerts will lead to an incident. Even when there is an incident, we have different response levels that we can use to deal with the incident.
    Incident response focuses on answering the question of what has happened during an incident. Incident management focuses on effectively taking actions to close off the incident.
    There are many different roles and responsibilities during an incident. Even if you are not part of the blue team, you may be a first responder or may be called upon as a subject matter expert to help the blue team deal with an incident.
    Most organisations have their own incident management framework, but most are based on the NIST incident management framework that covers the four phases of Preparation, Detection & Analyses, Containment, Eradication & Recovery, and Post Incident Analysis.
    Several things can go wrong during an incident, and preparation can assist in reducing the impact that these pitfalls can have.
