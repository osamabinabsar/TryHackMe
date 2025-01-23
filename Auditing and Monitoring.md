# Auditing and Monitoring.md

## Audit objectives and types

- Assess teh effectiveness of internal controls
- Identify and assess risks
- assess teh efficiency and effectiveness of information systems
- ensure compliance with laws and regualtions

![image](https://github.com/user-attachments/assets/c56f4325-a9af-437c-b1d2-2f9567a6ad30)


### Audit Types

- Internal
- External
- Third party audits

## Audit Frameworks

 - COSO
 - COBIT
 - ISAE 3402
 - ISO 27001
 - ITIL
 - PCI DSS
 - SOC 2
 - SOX



### Audit Frameworks Explained  

Here’s a breakdown of key audit frameworks, their focus areas, and relevance in compliance and governance:  

---

#### **1. COSO (Committee of Sponsoring Organizations of the Treadway Commission)**  
- **Focus**: Internal controls, risk management, and fraud prevention.  
- **Key Components**:  
  - **Five Components**: Control Environment, Risk Assessment, Control Activities, Information/Communication, Monitoring.  
  - **Enterprise Risk Management (ERM)**: Integrates risk into strategic decision-making.  
- **Use Case**: Widely used for financial reporting compliance (e.g., SOX).  

---

#### **2. COBIT (Control Objectives for Information and Related Technologies)**  
- **Focus**: IT governance and management.  
- **Key Components**:  
  - **Domains**: Align, Plan, Build, Run, Monitor.  
  - **Processes**: 40+ governance and management objectives.  
- **Use Case**: Align IT operations with business goals and regulatory requirements.  

---

#### **3. ISAE 3402 (International Standard on Assurance Engagements)**  
- **Focus**: Assurance reports on controls at service organizations (e.g., cloud providers).  
- **Key Components**:  
  - **Type I**: Design of controls at a specific point in time.  
  - **Type II**: Design and operational effectiveness over a period.  
- **Use Case**: Critical for outsourcing audits (e.g., SaaS providers).  

---

#### **4. ISO 27001 (International Organization for Standardization)**  
- **Focus**: Information Security Management Systems (ISMS).  
- **Key Components**:  
  - **Risk Assessment**: Identify and mitigate security risks.  
  - **Annex A Controls**: 114 controls (e.g., access control, cryptography).  
- **Use Case**: Global standard for certifying organizational security practices.  

---

#### **5. ITIL (Information Technology Infrastructure Library)**  
- **Focus**: IT service management (ITSM) best practices.  
- **Key Components**:  
  - **Service Lifecycle**: Strategy, Design, Transition, Operation, Improvement.  
  - **Incident/Problem Management**: Streamline IT service delivery.  
- **Use Case**: Improve IT service quality and align with business needs.  

---

#### **6. PCI DSS (Payment Card Industry Data Security Standard)**  
- **Focus**: Protection of cardholder data.  
- **Key Components**:  
  - **12 Requirements**: Includes encryption, network security, and access controls.  
  - **Regular Audits**: Annual assessments by Qualified Security Assessors (QSAs).  
- **Use Case**: Mandatory for organizations handling credit card transactions.  

---

#### **7. SOC 2 (Service Organization Control 2)**  
- **Focus**: Controls over security, availability, processing integrity, confidentiality, and privacy.  
- **Key Components**:  
  - **Trust Services Criteria**: Five categories of controls.  
  - **Type I/Type II**: Similar to ISAE 3402 but broader in scope.  
- **Use Case**: Assurance for cloud providers and SaaS companies.  

---

#### **8. SOX (Sarbanes-Oxley Act)**  
- **Focus**: Financial reporting accuracy and corporate governance.  
- **Key Components**:  
  - **Sections 302/404**: CEO/CFO accountability and internal control audits.  
  - **IT Controls**: Focus on systems impacting financial data (e.g., ERP).  
- **Use Case**: Required for publicly traded companies in the U.S.  

---

### **How These Frameworks Interrelate**  
- **Compliance Synergy**: ISO 27001 and SOC 2 often overlap in security controls.  
- **Governance**: COBIT and ITIL align IT operations with business strategy.  
- **Industry-Specific**: PCI DSS for payment cards, SOX for financial reporting.  

**Best Practices**:  
- Use a combination (e.g., COSO + COBIT for integrated risk and IT governance).  
- Align frameworks with organizational goals (e.g., ISO 27001 for global security compliance).  

By leveraging these frameworks, organizations can ensure robust governance, compliance, and risk management across operations.

![image](https://github.com/user-attachments/assets/6ea105e6-f0b4-4c83-8e7e-768d07c76035)



## Auditing IT infrastructure and operations

### Audit process
- Planning
- Information gathering
- Risk assessment and control evaluation
- Testing
- Analysis and findings
- Reporting
- Follow-up

![Hank Hackerson - The Most Boring AND Useful Topic In CySec Auditing   Monitoring Security Engineer Course  Czb2djc2yOM - 2134x1200 - 22m17s](https://github.com/user-attachments/assets/d2e9f6ad-c542-44ec-b1d2-6ab689c322f6)

### Audit Process Explained  

The audit process is a structured approach to evaluating an organization’s controls, compliance, and risk management practices. Below is a breakdown of its key stages:  

---

#### **1. Planning**  
- **Purpose**: Define the scope, objectives, and methodology of the audit.  
- **Key Activities**:  
  - Identify audit criteria (e.g., regulatory standards like ISO 27001, PCI DSS).  
  - Assign roles (auditors, stakeholders).  
  - Develop an audit schedule and resource plan.  
- **Best Practice**: Align with frameworks like **COSO** (for risk management) or **COBIT** (for IT governance).  

---

#### **2. Information Gathering**  
- **Purpose**: Collect data to understand processes, controls, and risks.  
- **Key Activities**:  
  - Review policies, procedures, and prior audit reports.  
  - Interview stakeholders (e.g., IT teams, process owners).  
  - Analyze system configurations and access logs.  
- **Tools**: Document management systems, questionnaires, workflow diagrams.  

---

#### **3. Risk Assessment and Control Evaluation**  
- **Purpose**: Identify risks and assess the effectiveness of controls.  
- **Key Activities**:  
  - Map risks to business objectives (e.g., data breaches, compliance failures).  
  - Evaluate control design (e.g., access controls, encryption).  
  - Use frameworks like **ISO 27001** (for security) or **NIST CSF** (for risk scoring).  
- **Example**: If a system lacks multi-factor authentication (MFA), flag it as a high-risk finding.  

---

#### **4. Testing**  
- **Purpose**: Validate whether controls operate as intended.  
- **Key Activities**:  
  - **Substantive Testing**: Verify transactions (e.g., sample invoices for SOX compliance).  
  - **Compliance Testing**: Check adherence to policies (e.g., password complexity rules).  
  - **Penetration Testing**: Simulate attacks to uncover vulnerabilities.  
- **Tools**: Automated scanners (e.g., Nessus), manual inspection.  

---

#### **5. Analysis and Findings**  
- **Purpose**: Interpret test results and identify gaps.  
- **Key Activities**:  
  - Categorize findings (e.g., critical, major, minor).  
  - Root cause analysis (e.g., why a control failed).  
  - Compare results against audit criteria (e.g., PCI DSS requirements).  
- **Output**: Draft findings with evidence (e.g., screenshots, logs).  

---

#### **6. Reporting**  
- **Purpose**: Communicate results to stakeholders.  
- **Key Components**:  
  - Executive summary (high-level risks and recommendations).  
  - Detailed findings (e.g., non-compliance with GDPR Article 32).  
  - Actionable remediation steps (e.g., "Implement DLP for data privacy").  
- **Formats**: SOC 2 reports, internal audit memos, or compliance certificates.  

---

#### **7. Follow-Up**  
- **Purpose**: Ensure corrective actions are implemented.  
- **Key Activities**:  
  - Track remediation progress (e.g., patch deployment).  
  - Re-audit critical issues if unresolved.  
  - Update risk registers and audit plans.  
- **Best Practice**: Use tools like Jira or ServiceNow to manage action items.  

---

### **Integration with Frameworks**  
- **ISO 27001**: Aligns with risk assessment and control evaluation phases.  
- **SOC 2**: Reporting phase includes Trust Services Criteria (security, availability, etc.).  
- **SOX**: Testing and reporting focus on financial controls.  

**Example Workflow**:  
1. **Planning**: Scope a PCI DSS audit for an e-commerce platform.  
2. **Testing**: Check if cardholder data is encrypted (AES-256).  
3. **Findings**: Flag unencrypted logs in a backup server.  
4. **Reporting**: Recommend encryption and quarterly vulnerability scans.  
5. **Follow-Up**: Confirm fixes within 30 days.  

By following this structured process, organizations can ensure compliance, mitigate risks, and improve operational resilience.




### Audit Areas

- Information Systems hardware
- OS
- File Systems
- Database Management Systems
- Network Infrastructure
- Network Operating Controls
- IT Operations
- Lights-out operations
- Problem management operations
- Monitoring Operations
- Procurement
- Business Continuity Plane
- DDisaster Recovery Planning

### Descriptive Explanation of Audit Areas  

#### **1. Information Systems Hardware**  
- **Focus**: Physical devices such as servers, workstations, routers, and storage systems.  
- **Audit Objectives**:  
  - **Maintenance**: Verify hardware is regularly updated, patched, and free from vulnerabilities.  
  - **Security**: Ensure physical access controls (e.g., biometric locks, surveillance) and encryption for storage media.  
  - **Compliance**: Check adherence to standards like ISO 27001 for asset management.  
- **Why It Matters**: Outdated or unsecured hardware can lead to data breaches or system failures.  

---

#### **2. Operating Systems (OS)**  
- **Focus**: Software managing hardware/resources (e.g., Windows, Linux).  
- **Audit Objectives**:  
  - **Patch Management**: Confirm OS updates are applied promptly to mitigate vulnerabilities (e.g., CVE-listed flaws).  
  - **Configuration**: Review user permissions, disabled unnecessary services, and audit logs.  
  - **Access Controls**: Ensure least privilege principles and MFA for administrative access.  
- **Standards**: NIST SP 800-53 for security configurations.  

---

#### **3. File Systems**  
- **Focus**: Structures organizing data storage (e.g., NTFS, ext4).  
- **Audit Objectives**:  
  - **Permissions**: Validate access rights (e.g., read/write privileges) to prevent unauthorized data exposure.  
  - **Integrity**: Check for tampering via checksums or cryptographic hashing.  
  - **Encryption**: Ensure sensitive files are encrypted (e.g., BitLocker, LUKS).  
- **Why It Matters**: Poorly managed file systems risk data leaks or ransomware attacks.  

---

#### **4. Database Management Systems (DBMS)**  
- **Focus**: Systems storing and managing structured data (e.g., Oracle, MySQL).  
- **Audit Objectives**:  
  - **Access Controls**: Review roles (e.g., DBA vs. read-only users) and audit SQL query logs.  
  - **Backups**: Confirm regular, encrypted backups and test restoration procedures.  
  - **Encryption**: Ensure data-at-rest (AES-256) and in-transit (TLS) encryption.  
- **Compliance**: GDPR, HIPAA, or PCI DSS for sensitive data handling.  

---

#### **5. Network Infrastructure**  
- **Focus**: Devices enabling communication (e.g., routers, switches, firewalls).  
- **Audit Objectives**:  
  - **Configuration**: Check firewall rules, VLAN segmentation, and firmware updates.  
  - **Traffic Monitoring**: Validate intrusion detection/prevention systems (IDS/IPS) and traffic encryption (VPNs).  
  - **Redundancy**: Assess failover mechanisms (e.g., BGP routing) to prevent outages.  
- **Frameworks**: CIS Benchmarks for network device hardening.  

---

#### **6. Network Operating Controls**  
- **Focus**: Policies governing network behavior (e.g., ACLs, QoS).  
- **Audit Objectives**:  
  - **Access Control Lists (ACLs)**: Ensure only authorized IPs/ports can communicate.  
  - **Traffic Prioritization**: Verify QoS policies align with business-critical applications.  
  - **Compliance**: Align with internal policies or standards like ISO 27032 for cybersecurity.  

---

#### **7. IT Operations**  
- **Focus**: Day-to-day management of IT services.  
- **Audit Objectives**:  
  - **Change Management**: Review approval workflows for system modifications.  
  - **Incident Response**: Assess procedures for detecting, reporting, and resolving issues (e.g., ITIL framework).  
  - **Capacity Planning**: Ensure resources (e.g., storage, bandwidth) meet demand.  

---

#### **8. Lights-Out Operations**  
- **Focus**: Automated/remote IT management (e.g., robotic process automation).  
- **Audit Objectives**:  
  - **Reliability**: Test scripts/tools for errors or security gaps.  
  - **Remote Access Security**: Validate VPNs, MFA, and session logging.  
  - **Failover**: Confirm automated failover to backup systems during failures.  

---

#### **9. Problem Management Operations**  
- **Focus**: Processes for diagnosing and resolving recurring issues.  
- **Audit Objectives**:  
  - **Root Cause Analysis (RCA)**: Check documentation of past incidents and corrective actions.  
  - **Knowledge Base**: Ensure solutions are logged for future reference (e.g., ServiceNow).  
  - **Continuous Improvement**: Measure reduction in incident recurrence.  

---

#### **10. Monitoring Operations**  
- **Focus**: Tools tracking system performance and security (e.g., Nagios, Splunk).  
- **Audit Objectives**:  
  - **Alert Configuration**: Verify thresholds for CPU usage, disk space, and security events.  
  - **Log Management**: Ensure logs are retained, encrypted, and analyzed for anomalies.  
  - **Response Times**: Assess SLA adherence for resolving alerts.  

---

#### **11. Procurement**  
- **Focus**: Acquisition of IT assets/services.  
- **Audit Objectives**:  
  - **Vendor Due Diligence**: Evaluate security practices of third-party providers.  
  - **Cost-Benefit Analysis**: Ensure purchases align with budget and operational needs.  
  - **Contract Compliance**: Review terms for SLAs, data ownership, and exit clauses.  

---

#### **12. Business Continuity Planning (BCP)**  
- **Focus**: Strategies to maintain operations during disruptions.  
- **Audit Objectives**:  
  - **Plan Completeness**: Validate BCP covers critical functions (e.g., payroll, customer support).  
  - **Testing**: Confirm regular drills (e.g., tabletop exercises) and updates post-test.  
  - **Alignment**: Ensure BCP aligns with risk assessments and organizational goals.  

---

#### **13. Disaster Recovery Planning (DRP)**  
- **Focus**: Restoring IT systems post-disaster.  
- **Audit Objectives**:  
  - **Recovery Time Objective (RTO)**: Verify systems can be restored within agreed timelines.  
  - **Backup Integrity**: Test data restoration from off-site/cloud backups.  
  - **Documentation**: Ensure DRP includes step-by-step recovery procedures and contact lists.  

---

### **Key Takeaways**  
- **Holistic Approach**: Audits should integrate technical checks (e.g., encryption) with process reviews (e.g., change management).  
- **Standards Alignment**: Leverage frameworks like ISO 27001, NIST, or ITIL to guide audit criteria.  
- **Continuous Improvement**: Use findings to refine policies, training, and tooling.  

By systematically evaluating these areas, organizations can mitigate risks, ensure compliance, and enhance operational resilience.


---
![Hank Hackerson - The Most Boring AND Useful Topic In CySec Auditing   Monitoring Security Engineer Course  Czb2djc2yOM - 2134x1200 - 24m40s](https://github.com/user-attachments/assets/dafe6591-9d86-40c5-8696-4f89ea70bcdc)
![Hank Hackerson - The Most Boring AND Useful Topic In CySec Auditing   Monitoring Security Engineer Course  Czb2djc2yOM - 2134x1200 - 25m22s](https://github.com/user-attachments/assets/b891cee2-3f1c-46ea-8848-b2d28e302e2e)

---

## Logs

![image](https://github.com/user-attachments/assets/9143828f-4118-45a1-887e-8864a7d9a0ef)

- Troubleshooting
- Monitoring
- Auditing
- Compliance

## Log management on Linux

> /var/log

**Types:**
- System logs
- Application logs
- Security Logs

> aureport
![Hank Hackerson - The Most Boring AND Useful Topic In CySec Auditing   Monitoring Security Engineer Course  Czb2djc2yOM - 2134x1200 - 34m50s](https://github.com/user-attachments/assets/d7404160-1058-490f-b3ba-89a6d76e8493)

## Log Management on windwos

- system logs
- application logs
- security logs
- forwarded events logs


![image](https://github.com/user-attachments/assets/c748b3b6-1b06-4870-9bfa-6c050f85f338)






![image](https://github.com/user-attachments/assets/136ca0b7-ff6d-4e21-bd8d-b768e53ca3e9)



## Monitoring

### Descriptive Explanation of Monitoring in Cloud Security  

Monitoring is a foundational element of cloud security and operational management, serving as the "eyes and ears" of an organization's IT infrastructure. Below is a detailed breakdown of its critical roles and benefits:  

---

#### **1. Troubleshooting and Maintenance**  
- **Purpose**: Rapid identification and resolution of operational faults.  
- **How It Works**:  
  - **Real-Time Alerts**: Tools like **AWS CloudWatch** or **Nagios** detect anomalies (e.g., server downtime, network latency).  
  - **Log Analysis**: Centralized logging platforms (e.g., Splunk, ELK Stack) aggregate data to pinpoint root causes (e.g., misconfigured firewall rules).  
  - **Automated Remediation**: Integrate with tools like **Ansible** to auto-resolve recurring issues (e.g., restarting crashed services).  
- **Example**: A sudden spike in database latency triggers an alert, allowing IT teams to trace it to an overloaded query and optimize indexing.  

---

#### **2. Performance Optimization**  
- **Purpose**: Enhance system efficiency and user experience.  
- **How It Works**:  
  - **Resource Metrics**: Track CPU usage, memory consumption, and bandwidth to identify bottlenecks.  
  - **Latency Monitoring**: Tools like **Datadog** measure response times for APIs or web applications.  
  - **Load Balancing**: Use metrics to redistribute traffic (e.g., AWS Elastic Load Balancer).  
- **Example**: High latency in a video streaming service prompts adjustments to CDN configurations or server scaling.  

---

#### **3. Preventing Failures**  
- **Purpose**: Proactively address issues before they escalate.  
- **How It Works**:  
  - **Predictive Analytics**: Machine learning models (e.g., Azure Anomaly Detector) forecast disk space exhaustion or hardware degradation.  
  - **Capacity Planning**: Monitor storage trends to preemptively add resources.  
  - **Health Checks**: Automated scripts validate system integrity (e.g., Kubernetes liveness probes).  
- **Example**: Detecting a storage array nearing 90% capacity allows teams to expand storage before outages occur.  

---

#### **4. Security Risk Mitigation**  
- **Purpose**: Detect and neutralize threats in real time.  
- **How It Works**:  
  - **Intrusion Detection Systems (IDS)**: Tools like **Snort** flag suspicious network traffic (e.g., port scanning).  
  - **SIEM Platforms**: **Splunk** or **QRadar** correlate logs to identify breaches (e.g., repeated failed login attempts).  
  - **Behavioral Analytics**: UEBA tools detect insider threats (e.g., abnormal data downloads).  
- **Example**: A sudden surge in outbound traffic triggers an alert, revealing a data exfiltration attempt.  

---

#### **5. Regulatory Compliance**  
- **Purpose**: Meet legal and industry standards.  
- **How It Works**:  
  - **Audit Trails**: Tools like **AWS CloudTrail** log user actions for GDPR or HIPAA audits.  
  - **Policy Enforcement**: Continuous checks ensure adherence to rules (e.g., encryption for PCI DSS).  
  - **Automated Reporting**: Generate compliance dashboards (e.g., SOC 2 reports) for auditors.  
- **Example**: Automated logs proving encryption of sensitive data satisfy a GDPR compliance audit.  

---

### **Key Tools and Technologies**  
- **Infrastructure Monitoring**: Prometheus, Zabbix  
- **Security Monitoring**: Wazuh, Palo Alto Cortex XDR  
- **Compliance**: Qualys, Tenable.io  

---

### **Why Monitoring is Non-Negotiable**  
- **Minimizes Downtime**: Rapid fault resolution keeps systems available (e.g., 99.9% uptime SLAs).  
- **Cost Efficiency**: Prevents over-provisioning by optimizing resource usage.  
- **Trust Building**: Demonstrates commitment to security and reliability for customers and regulators.  

By integrating robust monitoring practices, organizations can maintain resilient, secure, and high-performing cloud environments while staying ahead of evolving threats and compliance demands.


![image](https://github.com/user-attachments/assets/4cca90f2-3923-43f8-a3d4-8348c24c73a4)


## SIEM Basics

### Key Capabilities of SIEM (Security Information and Event Management) Technology  

SIEM technology plays a pivotal role in modern cybersecurity by unifying data collection, analysis, and response. Below is a detailed explanation of its core capabilities and their significance:  

---

#### **1. Data Aggregation**  
- **What It Does**: Collects and centralizes data from diverse sources, including network devices (firewalls, routers), security controls (antivirus, IDS/IPS), servers, cloud platforms, and databases.  
- **Why It Matters**:  
  - Provides a **holistic view** of the IT environment, enabling security teams to monitor all activities from a single pane of glass.  
  - Eliminates silos by integrating logs from on-premises, cloud, and hybrid systems.  
- **Example**: A SIEM tool like **Splunk** or **IBM QRadar** aggregates logs from AWS, Azure, and on-premises servers to track user access across all platforms.  

---

#### **2. Correlation and Analysis**  
- **What It Does**: Analyzes events and logs to identify patterns indicative of malicious activity.  
- **Why It Matters**:  
  - Detects **advanced threats** (e.g., multi-stage attacks) that single-point solutions might miss.  
  - Uses rules and machine learning to link seemingly unrelated events (e.g., failed logins followed by unusual data transfers).  
- **Example**: Correlating a phishing email alert with a sudden spike in outbound traffic to flag a potential data exfiltration attempt.  

---

#### **3. Alerting and Reporting**  
- **What It Does**: Generates real-time alerts for suspicious activities and produces compliance-ready reports.  
- **Why It Matters**:  
  - **Accelerates incident response** by notifying teams of critical issues (e.g., ransomware deployment).  
  - Simplifies compliance with regulations (e.g., GDPR, PCI DSS) through audit trails and pre-built report templates.  
- **Example**: A SIEM triggers an alert for repeated failed login attempts on an admin account and generates a weekly report for SOC 2 compliance.  

---

#### **4. Forensic Analysis**  
- **What It Does**: Enables historical investigation of security incidents using archived logs and event data.  
- **Why It Matters**:  
  - Helps trace the **root cause** of breaches (e.g., identifying how attackers bypassed defenses).  
  - Supports post-incident reviews to strengthen future security measures.  
- **Example**: After a breach, analysts use SIEM logs to reconstruct the attack timeline, revealing a compromised third-party vendor account.  

---

#### **5. Threat Intelligence Feeds**  
- **What It Does**: Integrates external threat data (e.g., known malicious IPs, malware signatures) to enhance detection.  
- **Why It Matters**:  
  - **Proactively blocks threats** by leveraging global threat intelligence (e.g., MITRE ATT&CK framework).  
  - Prioritizes alerts based on the relevance of known attack patterns.  
- **Example**: A SIEM cross-references incoming traffic with a threat feed to block connections to a ransomware command-and-control server.  

---

#### **6. Automation and Orchestration**  
- **What It Does**: Automates responses to common threats (e.g., isolating infected devices, blocking malicious IPs).  
- **Why It Matters**:  
  - **Reduces manual effort** and response time during incidents.  
  - Integrates with tools like SOAR (Security Orchestration, Automation, and Response) for end-to-end workflows.  
- **Example**: A SIEM automatically quarantines a workstation exhibiting ransomware behavior and notifies the security team via Slack.  

---

### **SIEM’s Role in Compliance and Security Posture**  
- **Regulatory Compliance**:  
  - Provides **audit trails** for standards like HIPAA (healthcare) or ISO 27001 (security management).  
  - Demonstrates adherence to data protection laws through detailed logging and reporting.  
- **Security Posture**:  
  - Enables **continuous monitoring** to detect and mitigate risks in real time.  
  - Strengthens defenses by aligning security practices with industry frameworks (e.g., NIST Cybersecurity Framework).  

---

### **Key SIEM Tools**  
- **Enterprise Solutions**: Splunk Enterprise Security, IBM QRadar, Microsoft Sentinel.  
- **Open-Source Options**: Elastic Security (ELK Stack), Wazuh.  

By leveraging these capabilities, SIEM technology empowers organizations to detect threats faster, streamline compliance, and maintain a robust security posture in evolving threat landscapes.



![image](https://github.com/user-attachments/assets/dba71ac6-77f8-4786-902a-2ecf3371d60b)
