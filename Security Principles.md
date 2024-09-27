# Security Principles

`It is impossible to achieve perfect security; no solution is 100% secure`


### CIA triad one step ahead
Going one more step beyond the CIA security triad, we can think of:

**Authenticity** : Authentic means not fraudulent or counterfeit. Authenticity is about ensuring that the document/file/data is from the claimed source.

**Nonrepudiation** : Repudiate means refusing to recognize the validity of something. Nonrepudiation ensures that the original source cannot deny that they are the source of a particular document/file/data. This characteristic is indispensable for various domains, such as shopping, patient diagnosis, and banking.

**Parkerian Hexad**

In 1998, Donn Parker proposed the Parkerian Hexad, a set of six security elements. They are:

1. Availability
2. Utility
3. Integrity
4. Authenticity
5. Confidentiality
6. Possession

**Utility**: Utility focuses on the usefulness of the information. For instance, a user might have lost the decryption key to access a laptop with encrypted storage. Although the user still has the laptop with its disk(s) intact, they cannot access them. In other words, although still available, the information is in a form that is not useful, i.e., of no utility.

**Possession**: This security element requires that we protect the information from unauthorized taking, copying, or controlling. For instance, an adversary might take a backup drive, meaning we lose possession of the information as long as they have the drive. Alternatively, the adversary might succeed in encrypting our data using ransomware; this also leads to the loss of possession of the data.
![image](https://github.com/user-attachments/assets/72cfca04-e412-43fc-9473-8655e0a8e3ca)


## DAD
![1742c9b384adb60b896481b2416d2f8a](https://github.com/user-attachments/assets/0ed8b555-57f7-410b-a91a-ebb98cae7bf0)

The security of a system is attacked through one of several means. It can be via the disclosure of secret data, alteration of data, or destruction of data.

**Disclosure** is the opposite of confidentiality. In other words, disclosure of confidential data would be an attack on confidentiality.
**Alteration** is the opposite of Integrity. For example, the integrity of a cheque is indispensable.
**Destruction/Denial** is the opposite of Availability.

Protecting confidentiality and integrity to an extreme can restrict availability, and increasing availability to an extreme can result in losing confidentiality and integrity. Good security principles implementation requires a balance between the three.

## Bell-LaPadula Model
The Bell-LaPadula Model aims to achieve confidentiality by specifying three rules:

**Simple Security Property:** This property is referred to as “no read up”; it states that a subject at a lower security level cannot read an object at a higher security level. This rule prevents access to sensitive information above the authorized level.
**Star Security Property:** This property is referred to as “no write down”; it states that a subject at a higher security level cannot write to an object at a lower security level. This rule prevents the disclosure of sensitive information to a subject of lower security level.
**Discretionary-Security Property:** This property uses an access matrix to allow read and write operations. An example access matrix is shown in the table below and used in conjunction with the first two properties.

| Subjects |  	Object A |  	Object B |
| --|
| Subject 1 |  	Write 	| No access |
| Subject 2 |  	Read/Write |  	Read | 

The first two properties can be summarized as “write up, read down.” You can share confidential information with people of higher security clearance (write up), and you can receive confidential information from people with lower security clearance (read down).

There are certain limitations to the Bell-LaPadula model. For example, it was not designed to handle file-sharing.

## Biba Model
The Biba Model aims to achieve integrity by specifying two main rules:

**Simple Integrity Property:** This property is referred to as “no read down”; a higher integrity subject should not read from a lower integrity object.
**Star Integrity Property:** This property is referred to as “no write up”; a lower integrity subject should not write to a higher integrity object.

These two properties can be summarized as “read up, write down.” This rule is in contrast with the Bell-LaPadula Model, and this should not be surprising as one is concerned with confidentiality while the other is with integrity.

Biba Model suffers from various limitations. One example is that it does not handle internal threats (insider threat).

## Clark-Wilson Model
The Clark-Wilson Model also aims to achieve integrity by using the following concepts:

**Constrained Data Item (CDI):** This refers to the data type whose integrity we want to preserve.
**Unconstrained Data Item (UDI):** This refers to all data types beyond CDI, such as user and system input.
**Transformation Procedures (TPs):** These procedures are programmed operations, such as read and write, and should maintain the integrity of CDIs.
**Integrity Verification Procedures (IVPs):** These procedures check and ensure the validity of CDIs.

#### Other models

- Brewer and Nash model
- Goguen-Meseguer model (Domain seperation)
- Sutherland model
- Graham-Denning model
- Harrison-Ruzzo-Ullman model



## ISO/IEC 19249
### ISO/IEC 19249:2017 Information technology - Security techniques - Catalogue of architectural and design principles for secure products, systems and applications.


ISO/IEC 19249 lists **five _architectural_ principles**:

**Domain Separation:** Every set of related components is grouped as a single entity; components can be applications, data, or other resources. Each entity will have its own domain and be assigned a common set of security attributes. For example, consider the x86 processor privilege levels: the operating system kernel can run in ring 0 (the most privileged level). In contrast, user-mode applications can run in ring 3 (the least privileged level). Domain separation is included in the Goguen-Meseguer Model.
**Layering:** When a system is structured into many abstract levels or layers, it becomes possible to impose security policies at different levels; moreover, it would be feasible to validate the operation. Let’s consider the OSI (Open Systems Interconnection) model with its seven layers in networking. Each layer in the OSI model provides specific services to the layer above it. This layering makes it possible to impose security policies and easily validate that the system is working as intended. Another example from the programming world is disk operations; a programmer usually uses the disk read and write functions provided by the chosen high-level programming language. The programming language hides the low-level system calls and presents them as more user-friendly methods. Layering relates to Defence in Depth.
**Encapsulation:** In object-oriented programming (OOP), we hide low-level implementations and prevent direct manipulation of the data in an object by providing specific methods for that purpose. For example, if you have a clock object, you would provide a method increment() instead of giving the user direct access to the seconds variable. The aim is to prevent invalid values for your variables. Similarly, in larger systems, you would use (or even design) a proper Application Programming Interface (API) that your application would use to access the database.
**Redundancy:** This principle ensures availability and integrity. There are many examples related to redundancy. Consider the case of a hardware server with two built-in power supplies: if one power supply fails, the system continues to function. Consider a RAID 5 configuration with three drives: if one drive fails, data remains available using the remaining two drives. Moreover, if data is improperly changed on one of the disks, it would be detected via the parity, ensuring the data’s integrity.
**Virtualization:** With the advent of cloud services, virtualization has become more common and popular. The concept of virtualization is sharing a single set of hardware among multiple operating systems. Virtualization provides sandboxing capabilities that improve security boundaries, secure detonation, and observance of malicious programs.

ISO/IEC 19249 teaches **five _design_ principles**:

**Least Privilege:** You can also phrase it informally as “need-to basis” or “need-to-know basis” as you answer the question, “who can access what?” The principle of least privilege teaches that you should provide the least amount of permissions for someone to carry out their task and nothing more. For example, if a user needs to be able to view a document, you should give them read rights without write rights.
**Attack Surface Minimisation:** Every system has vulnerabilities that an attacker might use to compromise a system. Some vulnerabilities are known, while others are yet to be discovered. These vulnerabilities represent risks that we should aim to minimize. For example, in one of the steps to harden a Linux system, we would disable any service we don’t need.
**Centralized Parameter Validation:** Many threats are due to the system receiving input, especially from users. Invalid inputs can be used to exploit vulnerabilities in the system, such as denial of service and remote code execution. Therefore, parameter validation is a necessary step to ensure the correct system state. Considering the number of parameters a system handles, the validation of the parameters should be centralized within one library or system.
**Centralized General Security Services:** As a security principle, we should aim to centralize all security services. For example, we would create a centralized server for authentication. Of course, you might take proper measures to ensure availability and prevent creating a single point of failure.
**Preparing for Error and Exception Handling:** Whenever we build a system, we should take into account that errors and exceptions do and will occur. For instance, in a shopping application, a customer might try to place an order for an out-of-stock item. A database might get overloaded and stop responding to a web application. This principle teaches that the systems should be designed to fail safe; for example, if a firewall crashes, it should block all traffic instead of allowing all traffic. Moreover, we should be careful that error messages don’t leak information that we consider confidential, such as dumping memory content that contains information related to other customers.


## Zero Trust versus Trust but Verify
**Trust but Verify:** This principle teaches that we should always verify even when we trust an entity and its behaviour. An entity might be a user or a system. Verifying usually requires setting up proper logging mechanisms; verifying indicates going through the logs to ensure everything is normal. In reality, it is not feasible to verify everything; just think of the work it takes to review all the actions taken by a single entity, such as Internet pages browsed by a single user. This requires automated security mechanisms, such as proxy, intrusion detection, and intrusion prevention systems.


**Zero Trust:** This principle treats trust as a vulnerability, and consequently, it caters to insider-related threats. After considering trust as a vulnerability, zero trust tries to eliminate it. It is teaching indirectly, “never trust, always verify.” In other words, every entity is considered adversarial until proven otherwise. Zero trust does not grant trust to a device based on its location or ownership. This approach contrasts with older models that would trust internal networks or enterprise-owned devices. Authentication and authorization are required before accessing any resource. As a result, if any breach occurs, the damage would be more contained if a zero trust architecture had been implemented.

Microsegmentation is one of the implementations used for Zero Trust. It refers to the design where a network segment can be as small as a single host. Moreover, communication between segments requires authentication, access control list checks, and other security requirements.




Vulnerability: Vulnerable means susceptible to attack or damage. In information security, a vulnerability is a weakness.

Threat: A threat is a potential danger associated with this weakness or vulnerability.

Risk: The risk is concerned with the likelihood of a threat actor exploiting a vulnerability and the consequent impact on the business.

Finally, the Shared Responsibility Model is worth mentioning, especially with the increased reliance on cloud services. Various aspects are required to ensure proper security. They include hardware, network infrastructure, operating systems, applications, etc. However, customers using cloud services have different access levels depending on the cloud services they use. For example, an Infrastructure as a Service (IaaS) user has complete control (and responsibility) over the operating system.

On the other hand, a Software as a Service (SaaS) user has no direct access to the underlying operating system. Consequently, achieving security in a cloud environment necessitates both the cloud service provider and the user to do their parts. The Shared Responsibility Model is a cloud security framework to ensure that each party is aware of its responsibility.




--------------------------------------------------------------------


Here’s a broad explanation of the three well-known security models used in information security to enforce **confidentiality**, **integrity**, and **data control** within systems:

### 1. **Bell-LaPadula Model (Confidentiality Model)**:
The **Bell-LaPadula (BLP) model** is primarily focused on **confidentiality**—ensuring that sensitive information is protected from unauthorized access. It was designed for military and government use, where classified information needs to be tightly controlled.

#### Key Principles:
- **Simple Security Property (No Read Up)**: A subject (user/process) cannot read data at a higher security level than their clearance. This ensures that someone with a lower clearance cannot access higher-classified information.
- **Star (*) Property (No Write Down)**: A subject cannot write information to a lower security level than their own. This prevents data from leaking to less secure areas or users.
- **Discretionary Security Property**: Access to objects (files, resources) is controlled based on the identity of the subjects (users) and their permissions.

##### Example:
A user with **Secret** clearance cannot read data labeled as **Top Secret** (No Read Up), and cannot write or transfer **Secret** information to a **Confidential** system (No Write Down).

#### Summary:
The Bell-LaPadula model focuses strictly on ensuring **confidentiality** by restricting unauthorized access to sensitive information. However, it does not address data **integrity** (i.e., the correctness or trustworthiness of the data).



### 2. **Biba Integrity Model (Integrity Model)**:
The **Biba model** is the opposite of Bell-LaPadula, focusing on **integrity**—ensuring that data cannot be tampered with or corrupted by unauthorized or untrusted users. It prevents modification of data by users or processes who are not authorized to change it.

#### Key Principles:
- **Simple Integrity Property (No Write Up)**: A subject cannot modify data at a higher integrity level than their own. This prevents less trusted users from altering critical, highly trustworthy data.
- **Star (*) Integrity Property (No Read Down)**: A subject cannot read data at a lower integrity level. This prevents trusted users from being influenced by data from a less trusted source, maintaining the integrity of the system.
  
##### Example:
An application or user with **low integrity** cannot modify or write to a file marked as **high integrity** (No Write Up), and a high-integrity user cannot read files from a lower integrity level (No Read Down).

#### Summary:
The Biba model ensures that data integrity is maintained by preventing unauthorized or lower-trust users from making changes or being influenced by less trustworthy information.



### 3. **Clark-Wilson Model (Commercial Integrity Model)**:
The **Clark-Wilson model** is another integrity-focused model but is more tailored to commercial environments (e.g., banking, retail, business operations) where data integrity is critical for business operations.

#### Key Principles:
- **Well-Formed Transactions**: Only specific, authorized transactions can modify data, ensuring that changes to data occur in a controlled, predictable manner.
- **Separation of Duties**: Different roles and users must be involved in various stages of the process to prevent fraud or errors. For example, one person might initiate a transaction, but another person must approve it.
- **Auditing and Enforcement**: The system must log and audit all changes and enforce controls to ensure that only authorized actions are taken.

#### Example:
In a bank, only authorized transactions such as debits and credits are allowed to alter the account balance. Any transaction must be properly authenticated and audited, and different employees must perform different parts of the transaction to prevent fraud.

#### Summary:
The Clark-Wilson model focuses on maintaining **data integrity** in commercial applications through controlled, well-defined transactions, **separation of duties**, and rigorous **auditing** to prevent unauthorized data modification.



### In Summary:
- **Bell-LaPadula**: Focuses on **confidentiality**, preventing unauthorized users from accessing classified data.
- **Biba**: Focuses on **integrity**, ensuring unauthorized users cannot tamper with sensitive data or affect trusted information.
- **Clark-Wilson**: Also emphasizes **integrity**, but is more business-oriented, ensuring data integrity through well-formed transactions and separation of duties in commercial systems.

Each model has its specific use case depending on whether the goal is to protect confidentiality, ensure data integrity, or control data in commercial processes.















---------------------------------------
Here is an overview of the **Brewer and Nash**, **Goguen-Meseguer**, **Sutherland**, **Graham-Denning**, and **Harrison-Ruzzo-Ullman** security models, which provide different approaches to ensuring security in computer systems and information flow.



### 1. **Brewer and Nash Model (Chinese Wall Model)**:
The **Brewer and Nash model**, also known as the **Chinese Wall model**, focuses on avoiding **conflicts of interest** in environments such as financial services, law firms, or consulting companies, where entities may have access to sensitive information about competitors or conflicting clients.

#### Key Principles:
- **Dynamic Access Control**: Access decisions are based on a user's prior interactions and are dynamically adjusted to prevent conflicts of interest.
- **No Conflicts of Interest**: Once a user accesses data from one client or entity, they are prevented from accessing related or conflicting data from another client to avoid compromising confidentiality.
  
##### Example:
If an employee has accessed sensitive data for Client A (say, a bank), they cannot access sensitive data for Client B (a competitor to Client A). This prevents leaking or sharing confidential information between competitors.

#### Summary:
The Brewer and Nash model is designed to prevent conflicts of interest by restricting access to information based on the user's past interactions with different entities.



### 2. **Goguen-Meseguer Model (Non-Interference Model)**:
The **Goguen-Meseguer model** is an **integrity-focused** security model built around the concept of **non-interference**, meaning that actions in one domain (or security level) should not affect or interfere with actions in another domain.

#### Key Principles:
- **Non-Interference**: The model ensures that no user or action at a high security level can influence or interfere with a user or process at a lower security level, and vice versa. This ensures data confidentiality and integrity across domains.
- **Automata-Based Approach**: The system is modeled as a set of independent processes (or users), where one process should not interfere with another.

##### Example:
If a classified system processes secret data, the actions of a user working on unclassified data cannot be influenced by any actions or data at the classified level.

#### Summary:
The Goguen-Meseguer model is concerned with ensuring that actions at one level of security cannot interfere with or influence actions at another level, supporting integrity and confidentiality.



### 3. **Sutherland Model (Information Flow Model)**:
The **Sutherland model** is an **information flow** model that focuses on preserving **integrity** by controlling how information flows between different system components or security levels.

#### Key Principles:
- **Information Flow Control**: Ensures that information does not flow from high-integrity levels to lower-integrity levels in an uncontrolled way, which could potentially corrupt or damage critical data.
- **State Transitions**: Uses mathematical logic to track and control how information moves between states in a system to ensure no unauthorized actions or changes occur.
  
##### Example:
In a financial system, the Sutherland model would ensure that unauthorized users or processes cannot corrupt transaction records by controlling how data is accessed and modified throughout the system.

#### Summary:
The Sutherland model is designed to control and monitor the flow of information between different integrity levels to ensure that high-integrity data is not compromised by unauthorized or lower-integrity processes.



### 4. **Graham-Denning Model (Access Control Model)**:
The **Graham-Denning model** is focused on defining a set of rules for **securely managing access rights** and the delegation of those rights within a computer system. It provides a detailed framework for managing the creation, deletion, and modification of subjects (users) and objects (files/resources).

#### Key Principles:
- **Eight Basic Actions**: The model defines eight basic operations that govern how subjects and objects interact:
  1. Create Object
  2. Delete Object
  3. Create Subject
  4. Delete Subject
  5. Read Access
  6. Grant Access
  7. Delete Access
  8. Transfer Access
- **Access Control Lists (ACLs)**: The model supports the management of access rights via access control lists that specify who can perform which actions on what resources.

##### Example:
A user with the appropriate permissions can create a file (object), assign read or write access to another user (subject), and later revoke that access or delete the file.

#### Summary:
The Graham-Denning model is used for defining and managing access control rights and permissions within a system, specifying how subjects (users) interact with objects (resources) securely.



### 5. **Harrison-Ruzzo-Ullman (HRU) Model**:
The **Harrison-Ruzzo-Ullman model** is an **extension of the Graham-Denning model** and provides a formal, mathematical framework for **managing access rights** within a computer system. It focuses on the administration and modification of access controls dynamically during system execution.

#### Key Principles:
- **Access Control Matrix**: The HRU model uses an access control matrix to define who can perform what actions on which objects.
- **Operations on Access Rights**: The model defines the ability to modify access rights dynamically using operations like **create**, **delete**, **read**, and **write**, providing flexibility in managing system access.
- **Safety Problem**: A key contribution of this model is the introduction of the "safety problem"—the question of whether a system can guarantee that a specific access right cannot be leaked to an unauthorized subject.

##### Example:
A system administrator can create a new user and assign them specific access rights, such as read-only access to a file, but the system must ensure that these rights cannot be escalated or transferred inappropriately.

#### Summary:
The Harrison-Ruzzo-Ullman model provides a mathematical basis for managing access controls dynamically and addresses the question of whether a system is "safe" from unauthorized access right propagation.



### In Summary:
- **Brewer and Nash Model**: Prevents conflicts of interest by controlling access based on past interactions.
- **Goguen-Meseguer Model**: Enforces non-interference between security domains to protect integrity.
- **Sutherland Model**: Focuses on controlling the flow of information to maintain system integrity.
- **Graham-Denning Model**: Provides rules for managing access rights and how users interact with system resources.
- **Harrison-Ruzzo-Ullman Model**: Extends access control models with a focus on the dynamic administration of rights and the safety of access controls.

Each of these models addresses different aspects of security, from preventing conflicts of interest to ensuring data integrity and managing dynamic access rights.









----------------------------------------
ISO/IEC 19249 is an important international standard that provides a framework for security techniques, specifically focusing on **security capabilities of information technology (IT) products**. It is intended to help developers, system architects, and security engineers incorporate security features into their products and services by defining a structured approach to ensuring security capabilities across various domains. Below is a comprehensive overview of ISO/IEC 19249.

### Overview of ISO/IEC 19249:
The full title of the standard is **ISO/IEC 19249: Security Techniques – Catalog of Architectural and Design Principles for Secure Products, Systems, and Applications**. This standard outlines a **catalog of architectural and design principles** that can be applied to IT products, systems, and applications to enhance their security.

### Key Goals:
The primary goal of ISO/IEC 19249 is to **improve the security posture** of IT systems and products by providing a set of **design principles** that can be applied during development. These principles help:
1. **Reduce vulnerabilities**.
2. **Enhance resilience** to attacks.
3. **Ensure the confidentiality, integrity, and availability** of data.
4. Provide **guidance on security architecture** that can be adapted to different industries and use cases.



### Structure of ISO/IEC 19249:
ISO/IEC 19249 is structured around **security design principles** that are applied to system architecture and software development. These principles are organized into various categories that reflect different aspects of secure design.

Here are the **four main categories** covered in ISO/IEC 19249:

### 1. **Principles of Secure Design**:
These are high-level principles that guide the overall design of secure systems. They help ensure that security is considered throughout the product life cycle—from conceptualization to deployment and maintenance.

#### Key Principles:
- **Minimize Attack Surface**: Design systems with the smallest possible set of features exposed to potential attackers. By reducing the number of entry points, you limit opportunities for attacks.
- **Separation of Privileges**: Ensure that different system components operate with the least amount of privilege required. This prevents a compromise of one component from spreading throughout the system.
- **Fail-Safe Defaults**: Systems should default to a secure state, especially during failure. When errors occur, access should be denied rather than allowed.
- **Least Privilege**: Ensure that users and system processes are granted only the minimum level of access necessary to perform their functions.
  


### 2. **Security Architecture Patterns**:
These patterns provide **templates for securing the design of systems and networks**. Security patterns ensure that architecture is structured in a way that makes it inherently more secure against common threats.

#### Example Patterns:
- **Layered Security (Defense-in-Depth)**: Implement multiple layers of security controls, so if one layer is breached, others still provide protection.
- **Isolated Execution Environments**: Run critical functions or processes in separate environments to prevent interference or exploitation by compromised processes.
- **Use of Secure Components**: Incorporate security-enhanced components like trusted platforms or secure hardware into the system design to improve overall security.



### 3. **Cryptographic Design Principles**:
Cryptographic mechanisms are fundamental to modern security systems, and ISO/IEC 19249 outlines principles for **correctly integrating cryptographic methods** into product and system design.

#### Key Cryptographic Principles:
- **Use Strong Algorithms**: Use cryptographic algorithms that are recognized as secure by the cryptographic community (e.g., AES, RSA). Avoid proprietary or weak algorithms.
- **Key Management**: Properly manage encryption keys, ensuring secure storage, distribution, and rotation. Weak key management often leads to system compromise, even when using strong cryptography.
- **Secure Communication Channels**: Always encrypt sensitive data during transmission, ensuring that unauthorized parties cannot intercept or modify the data in transit.
  


### 4. **Operational Security and Management**:
This category focuses on principles that ensure secure operation and management of IT systems over time, addressing concerns like **monitoring**, **logging**, and **maintenance**.

#### Key Operational Principles:
- **Secure Configuration**: Systems should be deployed with secure default configurations and regularly updated to address new threats. Configuration management should ensure that no unnecessary services are running.
- **Regular Patching and Updates**: Ensure that systems are regularly updated to protect against known vulnerabilities. Vulnerability management is critical for maintaining the security posture of deployed systems.
- **Auditing and Logging**: Implement logging of security-relevant events and perform regular audits to detect and respond to potential security incidents.



### ISO/IEC 19249 in Practice:
To apply ISO/IEC 19249 effectively, developers and security engineers must integrate these principles into every phase of the **software development life cycle (SDLC)**. Here’s how ISO/IEC 19249 can guide different stages of development:

#### 1. **Requirements Analysis**:
During the requirements phase, security requirements should be explicitly defined based on the organization’s risk profile. This is where the principle of **least privilege** and **fail-safe defaults** can be included.

#### 2. **Design**:
At the design stage, **security architecture patterns** like **defense-in-depth**, **use of secure components**, and **minimization of attack surface** should be incorporated into the system architecture.

#### 3. **Implementation**:
Developers must follow **secure coding practices** based on ISO/IEC 19249 principles, such as using **strong cryptography**, preventing **buffer overflows**, and ensuring **input validation**.

#### 4. **Testing**:
In testing, **penetration testing** and **vulnerability scanning** should be performed to evaluate the effectiveness of the security controls implemented, ensuring compliance with the principles outlined in ISO/IEC 19249.

#### 5. **Deployment and Maintenance**:
After deployment, continuous **monitoring**, **logging**, **auditing**, and **patch management** are crucial to maintaining the security of the system over time.



### Benefits of ISO/IEC 19249:
1. **Enhanced Security**: By following a structured set of principles, organizations can reduce the risk of vulnerabilities and better protect against security threats.
2. **Consistency in Security Design**: The standard provides a common framework and language for discussing and implementing security, promoting consistency across projects.
3. **Compliance and Assurance**: Adopting ISO/IEC 19249 helps organizations align with international security standards, which can assist with regulatory compliance and improving trust with clients and stakeholders.
4. **Scalability**: The principles can be applied across a variety of industries, product types, and system complexities, making them highly adaptable.


### How ISO/IEC 19249 Fits into Other Security Standards:
ISO/IEC 19249 complements other security standards, such as:
- **ISO/IEC 27001**: An information security management standard, which focuses on security controls and governance.
- **ISO/IEC 15408 (Common Criteria)**: A security framework that provides a structured way of evaluating and certifying the security of IT products.
- **ISO/IEC 29147**: Guidelines for vulnerability disclosure, which align well with the operational security principles in ISO/IEC 19249.

Together, these standards provide a comprehensive approach to managing security, both at the governance level (ISO/IEC 27001) and at the product or system level (ISO/IEC 19249).

### Conclusion:
ISO/IEC 19249 provides an invaluable framework for ensuring the **secure design** and **architecture** of IT systems and products. By following its design principles and security architecture patterns, organizations can mitigate vulnerabilities, enhance resilience against attacks, and ensure that security is embedded throughout the product lifecycle. Integrating ISO/IEC 19249 with other security standards and practices ensures a holistic approach to **information security** and **cyber resilience**.

