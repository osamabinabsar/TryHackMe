# Hardening(Linux System, Windows, Active Directory, Network System)

## Linux
- boot access = root access

![image](https://github.com/user-attachments/assets/98921b04-988c-4602-b473-0b31a1201397)

## LUKS (Linux Unified Key Setup)
-
- ![image](https://github.com/user-attachments/assets/c1f90ff0-8923-4639-b448-e9b27458f066)
LUKS (Linux Unified Key Setup) is a standard for disk encryption on Linux. It provides a way to encrypt entire block devices, such as hard drives, USB drives, or partitions, ensuring that the data stored on them is secure. LUKS is widely used due to its flexibility, strong security features, and integration with the Linux kernel.

### Key Features of LUKS:
1. **Full Disk Encryption**: Encrypts entire block devices, making it suitable for securing entire drives or partitions.
2. **Multiple Keys**: Supports multiple encryption keys, allowing for key management and recovery options.
3. **Key Derivation Function (KDF)**: Uses PBKDF2 (Password-Based Key Derivation Function 2) to strengthen passphrases against brute-force attacks.
4. **Cipher Flexibility**: Allows users to choose from various encryption algorithms (e.g., AES, Serpent, Twofish) and modes (e.g., XTS, CBC).
5. **Header Backup**: The LUKS header contains critical information for decryption. Users can back up this header to recover data if the header becomes corrupted.
6. **Cross-Distribution Compatibility**: LUKS is supported across most Linux distributions, making it a portable encryption solution.

### How LUKS Works:
1. **Header**: The LUKS header stores metadata, including encryption parameters, key slots, and other information required for decryption.
2. **Key Slots**: LUKS supports up to 8 key slots, each of which can store a passphrase or key. This allows for multiple users or backup keys.
3. **Master Key**: The actual encryption key used to encrypt the data is stored in the header, encrypted by the keys in the key slots.
4. **Encryption Process**: When a device is unlocked using a passphrase or key, the master key is decrypted and used to encrypt/decrypt the data on the fly.

### Common Use Cases:
- **Encrypting Hard Drives**: Protects sensitive data on laptops, desktops, or servers.
- **Removable Media**: Encrypts USB drives or external hard drives for secure data transport.
- **Cloud Storage**: Encrypts virtual disks or volumes used in cloud environments.

### Basic Commands for LUKS:
1. **Formatting a Device with LUKS**:
   ```bash
   sudo cryptsetup luksFormat /dev/sdX
   ```
   This command initializes a LUKS partition on `/dev/sdX`.

2. **Opening a LUKS Device**:
   ```bash
   sudo cryptsetup open /dev/sdX my_encrypted_device
   ```
   This unlocks the LUKS device and maps it to `/dev/mapper/my_encrypted_device`.

3. **Creating a Filesystem**:
   ```bash
   sudo mkfs.ext4 /dev/mapper/my_encrypted_device
   ```
   Creates a filesystem on the unlocked device.

4. **Mounting the Device**:
   ```bash
   sudo mount /dev/mapper/my_encrypted_device /mnt
   ```
   Mounts the encrypted device to `/mnt`.

5. **Closing a LUKS Device**:
   ```bash
   sudo cryptsetup close my_encrypted_device
   ```
   Closes the LUKS device and removes the mapping.

6. **Adding a New Passphrase**:
   ```bash
   sudo cryptsetup luksAddKey /dev/sdX
   ```
   Adds a new passphrase to an existing LUKS device.

7. **Backing Up the LUKS Header**:
   ```bash
   sudo cryptsetup luksHeaderBackup /dev/sdX --header-backup-file luks-header.img
   ```
   Backs up the LUKS header to a file for recovery purposes.

### Security Considerations:
- **Strong Passphrases**: Use long, complex passphrases to protect against brute-force attacks.
- **Header Backup**: Always back up the LUKS header to avoid data loss in case of corruption.
- **Physical Security**: LUKS protects data at rest, but physical access to an unlocked device can still compromise security.

LUKS is a powerful tool for securing data on Linux systems, and its integration with the Linux kernel makes it a reliable choice for disk encryption.
![image](https://github.com/user-attachments/assets/8544aacd-a3dd-4345-a8f6-35272647c47d)
![image](https://github.com/user-attachments/assets/4b8cc8ff-5952-4c19-b760-498bf8329561)
![image](https://github.com/user-attachments/assets/b4b8ce93-e7a5-452c-bfe4-0c9f061f4b4b)


_to decrypt a img file, we need to first mount it to an empty directory adn tehn use the following command_
![image](https://github.com/user-attachments/assets/a606e74d-dcb7-4632-a3a8-40fe8341b3e5)


### Firewall(linux)


#### iptables
![image](https://github.com/user-attachments/assets/635c3f50-2805-4526-95b9-ac72ed8b8cfa)
**Understanding iptables and its Configuration**

**Introduction to iptables:**

iptables is a user-space utility program that allows creation and management of the Linux kernel's firewall, known as netfilter. It is used to configure network packet filtering and NAT (Network Address Translation) rules.

**Default Chains in iptables:**

1. **INPUT Chain:**
   - Handles packets destined for the local system.
   - Example: Allowing incoming SSH connections.
     ```
     iptables -A INPUT -p tcp --dport 22 -j ACCEPT
     ```

2. **OUTPUT Chain:**
   - Manages packets generated by the local system.
   - Example: Allowing outgoing SSH responses.
     ```
     iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT
     ```

3. **FORWARD Chain:**
   - Deals with packets being routed through the system.
   - Relevant for systems acting as routers or firewalls for other devices.

**Rule Ordering and Persistence:**

- Rules are processed in order, and the first match determines the packet's fate.
- More specific rules should precede general ones (e.g., allow port 22 before dropping all traffic).
- To block all other traffic:
  ```
  iptables -A INPUT -j DROP
  iptables -A OUTPUT -j DROP
  ```
- Persistence: Use `iptables-save` to save rules and `iptables-restore` to reload them on reboot.

**Additional Considerations:**

- **Chains and Tables:**
  - Default table is `filter`, containing INPUT, OUTPUT, and FORWARD chains.
  - Other tables include `nat` for NAT and `mangle` for packet manipulation.

- **Stateful Connections:**
  - Utilize connection tracking to allow responses to outgoing connections.
  - Example:
    ```
    iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    ```

- **Listing and Flushing Rules:**
  - List rules: `iptables -L`
  - Flush rules: `iptables -F`

- **Differences Between iptables and nftables:**
  - nftables is a newer, more scalable, and flexible firewall framework.
  - Considered a successor to iptables, especially for large rule sets.

**Best Practices and Tools:**

- Use scripts or configuration management tools to automate rule setup.
- Consider performance implications of large rule sets.
- Implement logging for security auditing by adding logging rules:
  ```
  iptables -A INPUT -j LOG
  ```

In summary, iptables is a powerful tool for managing network traffic on Linux systems. Understanding its chains, tables, and rule processing order is crucial for effective firewall configuration. For more advanced and scalable setups, exploring nftables is recommended.


#### nftables

![image](https://github.com/user-attachments/assets/59b94e73-0667-47fe-992e-9b0fd5c9a3d3)

**Introduction to nftables:**

nftables represent a significant evolution in Linux firewall technology, succeeding iptables. Designed to address the limitations of iptables, nftables offer enhanced performance, scalability, and flexibility, making them an essential tool for modern network security.

**Key Features and Advantages:**

1. **Modern Architecture:**
   - nftables operate on a new framework that improves efficiency and scalability. They use a stateful packet filtering mechanism, allowing for more sophisticated rule processing.

2. **Flexibility and Expressiveness:**
   - The syntax of nftables is more flexible and expressive compared to iptables, enabling the creation of complex rulesets with ease.

3. **Advanced Features:**
   - Support for sets, timeouts, and logging enhances the capabilities of nftables, making them suitable for advanced security configurations.

**Concepts in nftables:**

- **Tables:**
  - Tables in nftables are containers for chains and rules. Unlike iptables, nftables do not come with predefined tables; you must create them explicitly. For example, `nft add table fwfilter` creates a table named "fwfilter."

- **Chains:**
  - Chains are lists of rules to which packets are submitted. In nftables, chains are created within tables and are associated with specific hooks in the netfilter framework. For instance, `nft add chain fwfilter fwinput { type filter hook input priority 0; }` creates a chain named "fwinput" that handles incoming packets.

- **Hooks:**
  - Hooks determine when a chain is evaluated in the packet processing flow. Common hooks include input, output, forward, prerouting, and postrouting.

**Configuring nftables:**

- **Creating Tables and Chains:**
  - Tables and chains must be created before rules can be added. This allows for a more organized and modular approach to firewall management.

- **Adding Rules:**
  - Rules define the filtering criteria and actions. For example, `nft add rule fwfilter fwinput tcp dport 22 accept` allows incoming SSH traffic on port 22.

- **Managing and Persisting Rules:**
  - Rules can be managed using commands like `nft list table fwfilter` to view the current configuration. Persistence across reboots can be achieved using scripts or configuration management tools.

**Security Best Practices:**

- **Principle of Least Privilege:**
  - Configure rules to allow only necessary traffic, minimizing the attack surface.

- **Logging and Monitoring:**
  - Implement logging to monitor network traffic and detect potential security incidents.

**Comparison with iptables:**

- **Scalability:**
  - nftables handle large rule sets more efficiently, making them suitable for high-traffic environments.

- **Syntax and Flexibility:**
  - nftables' syntax is more intuitive and flexible, allowing for complex rule definitions.

**Packet Flow in the Linux Kernel:**

- Understanding the packet flow through the Linux kernel is crucial for effective firewall configuration. nftables integrate seamlessly with the netfilter framework, allowing for precise control over packet processing.

**Practical Scenarios:**

- **Complex Networking Environments:**
  - nftables are advantageous in environments requiring intricate security policies, such as data centers or cloud infrastructures.

- **High-Availability Systems:**
  - Their performance and scalability make nftables ideal for high-availability setups where traffic is substantial and diverse.


## UFW

Uncomplicated Firewall (UFW) is a user-friendly interface for managing a Linux system's firewall, simplifying the complexities of `iptables`. It is designed to facilitate the configuration of an IPv4 or IPv6 host-based firewall. 

**Key Features of UFW:**

- **Simplified Management:** UFW provides straightforward commands to allow or deny traffic, making firewall management accessible even to those who may find `iptables` challenging.

- **Default Policies:** By default, UFW denies all incoming connections and allows all outgoing connections. This default stance ensures that, unless explicitly permitted, external systems cannot initiate connections to your machine, while your system can still reach out to others. 

- **Status Monitoring:** You can check the current status of UFW and view the rules that are in place using commands like `sudo ufw status` and `sudo ufw status verbose`. 

**Basic UFW Commands:**

1. **Enable UFW:**

   Before enabling UFW, it's crucial to allow SSH connections to prevent being locked out, especially if you're managing the system remotely.

   ```bash
   sudo ufw allow ssh
   sudo ufw enable
   ```

   Enabling UFW activates the firewall with the current set of rules. 

2. **Allow or Deny Specific Ports:**

   To allow incoming traffic on a specific port (e.g., port 80 for HTTP):

   ```bash
   sudo ufw allow 80/tcp
   ```

   To deny incoming traffic on a specific port:

   ```bash
   sudo ufw deny 23/tcp
   ```

   These commands specify the port and the protocol (TCP or UDP). 

3. **Delete a Rule:**

   To remove a previously added rule:

   ```bash
   sudo ufw delete allow 80/tcp
   ```

   This command deletes the rule that allows traffic on port 80. 

4. **Check UFW Status:**

   To view the current status and rules:

   ```bash
   sudo ufw status
   ```

   For a more detailed view:

   ```bash
   sudo ufw status verbose
   ```

   These commands display whether UFW is active and list the current rules. 

**Example Scenario:**

Suppose you're running a web server and an SSH server. You want to allow users to access your website and allow yourself to connect via SSH, but block all other incoming connections. You can configure UFW as follows:

```bash
sudo ufw allow 80/tcp    # Allow HTTP traffic
sudo ufw allow 443/tcp   # Allow HTTPS traffic
sudo ufw allow 22/tcp    # Allow SSH traffic
sudo ufw enable          # Enable UFW with the specified rules
```

After executing these commands, UFW will permit incoming connections on ports 80, 443, and 22, while denying all other incoming traffic. Outgoing traffic remains allowed by default. 

By utilizing UFW, you can effectively manage your system's firewall with simple commands, enhancing security without the complexity of directly handling `iptables`. 


## Remote Access(SSh, 

![image](https://github.com/user-attachments/assets/5729b725-5f79-45ba-9a20-f93549b92740)
![image](https://github.com/user-attachments/assets/90b50979-e8f6-4c47-9f71-e505fa8b5147)


## Securing user accounts

![image](https://github.com/user-attachments/assets/ae67eab3-69ec-44fb-adef-0b10652a263d)
![image](https://github.com/user-attachments/assets/569b63eb-3a9b-4103-b67f-f2fb46f593d7)
![image](https://github.com/user-attachments/assets/9e8b5d1e-a7c3-4fad-b46c-2a40e6a08c42)
![image](https://github.com/user-attachments/assets/d0282680-9165-4016-bfe6-b478988d20b3)


## Softwares and Services

- Disable uninstall unnecessary services
- block unneeded network ports
- avoid legacy protocols
  - for example, using SFTP instead of TFTP
 
- Remove identification string
  - when connected to a server, it details the version, server or program name, host os.
 

## Update and Upgrade policies.

- selecting LTS
-  Kernel Updates
-  Automatic Updates

 

   ![image](https://github.com/user-attachments/assets/1602f2bf-64df-4d2a-a3d2-aa2b53d7f45e)
  


## Audit and Log Config

![image](https://github.com/user-attachments/assets/2e4b7c6c-bd08-48b7-9fe9-8b166e669cd4)

![image](https://github.com/user-attachments/assets/9bb37c0d-45a1-4695-bebe-dff2fa529e77)

---
---


# Windows

![image](https://github.com/user-attachments/assets/9dbe4300-9e10-42f0-b693-f4e0bf1cd924)
![image](https://github.com/user-attachments/assets/76301326-d79a-4edc-b0ed-b1ff5d32e7e9)
![image](https://github.com/user-attachments/assets/621d05fb-9dc8-4863-b1f8-31885db2d6b1)
![image](https://github.com/user-attachments/assets/52ceb848-a939-4516-b620-a903887ba123)

## Identity & Access Management


![image](https://github.com/user-attachments/assets/4baa3a27-8aaf-4fd5-b848-e1d2dcbb19d9)

_Keep notification level "Always Notify" in UAC_

- Local & Group Policies
- Password Policies
- Setting a lockout Policy
  ![image](https://github.com/user-attachments/assets/305c43a3-393a-45ea-bd77-e730d7e29b74)


## Network Management

- Windows Defender Firewall(WF.msc)
  - Private Profile must be activated with Blocked Incoming Connections while using computer at home.
    ![image](https://github.com/user-attachments/assets/6f5e7ffb-1f02-452e-b60e-816b7ee8f7f1)

- Disable Unused Networking Devices
- Disable SMB Protocol
- Protect Local DNS
  - fixing host file, host file acts as a local DNS,
  - DNS translates Fully Qualified Domain Names(FQDN) into IP address.
- Mitigaring Address Resolution Protocol Attack
  - ARP resolves MAC form IP in workstations ARP cache.
  - ARP has no authenticaiton and accepts responsed from any user.
  - arp -a
    ![image](https://github.com/user-attachments/assets/d9c62ace-04d5-4ab1-8ac9-dc2bd4822f85)

- Disabling RDP
- 



## Application Management

- Trusted App Store
- MS app store for safe apps? Not all apps are found there.
- Malware Removal & Windows Defender
- MS office hardening
- AppLocker
  ![image](https://github.com/user-attachments/assets/62ebf164-4266-4254-969c-3d36344bdde2)
  ![image](https://github.com/user-attachments/assets/53d67b0c-5556-4c45-82a1-ec095bbf3481)
- Browser Hardening
- Microsoft Smart Screen
- 

  


## Storage Management

- Data Encryption Through BitLocker
- Windwos Sandbox
- Windwos Secure Boot
- BAckups


![image](https://github.com/user-attachments/assets/0d40fdda-07a7-40e4-813b-ac8c918a8d55)





![image](https://github.com/user-attachments/assets/9bb44a6c-0eb7-4015-8e85-574d3c560457)





# Active Directory Hardening

**Domain**

The domain acts as a core unit regarding the logical structure of the Active Directory. It initially stores all the critical information about the objects that belong to the domain only. 

**Domain Controller**
A Domain Controller is an Active Directory server that acts as the brain for a Windows server domain; it supervises the entire network. Within the domain, it acts as a gatekeeper for users' authentication and IT resources authorisation.

**Trees and Forests**
Trees and Forests are the two most critical concepts of the Active Directory.


**Forests**

When the sharing of the standard global catalogue, directory schema, logical structure, and directory configuration between the collections of trees is made successfully, it is called a Forest. Communication between two forests becomes possible once a forest-level trust is created.

**Trust in Active Directory**

AD trust is the established communication bridge between the domains in Active Directory. When we say one domain trusts another in the AD network, it means its resources can be shared with another domain. However, one domain's resources are not directly available to every other domain, as it is not safe. Thus, the resource sharing availability is governed by Trusts in AD. The AD trusts are of two categories, which are classified based on their characteristics or the current direction.

![56a0dbd78d255d0ff7f75f225a82f9d4](https://github.com/user-attachments/assets/dea038c9-a62b-4f8d-9781-6fb446b6e884)

AD trusts categorised based on characteristics are known as Transitive and non-Transitive trusts. Transitive trust reflects a two-way relationship between domains. If there are three domains, domain A trusts domain B and domain B has a transitive trust with domain C. Consequently, domain A will automatically trust domain C for sharing resources.

Again, AD trusts are of two types when classified based on their direction: One-way and Two-way trusts. You can access the AD trust through the following:
Server Manager > Tools > Active Directory Domains and Trust

**Container and Leaves**

For those familiar, each network part is treated as an object in AD. Anything from resources, users, services, or part of the network can be an object. The hierarchical structure of AD defines that an object may or may not contain other objects based on the scenario. When an object holds another object, it is termed a container; otherwise, it is called the leaf object.



**---**
Active Directory (AD) is a directory service developed by Microsoft for Windows domain networks. It is a critical component in enterprise environments, providing centralized management of users, computers, and other resources. Below is a technical breakdown of key AD concepts, tailored for a master's-level cybersecurity student:



### **1. Domain**
- A **domain** in AD is a logical grouping of objects (users, computers, groups, etc.) that share a common directory database and security policies.
- Domains are identified by a **Domain Name System (DNS)** name (e.g., `example.com`).
- Each domain has its own **Security Identifier (SID)**, which is used to uniquely identify the domain and its objects.
- Domains are managed by **Domain Controllers (DCs)**, which host the AD database and enforce security policies.



### **2. Domain Controller (DC)**
- A **Domain Controller** is a server that runs the AD Domain Services (AD DS) role.
- It stores the AD database (`ntds.dit`), handles authentication (via Kerberos), and enforces security policies.
- DCs replicate data among themselves to ensure high availability and fault tolerance.
- The **Primary Domain Controller (PDC) Emulator** is a FSMO (Flexible Single Master Operations) role that handles password changes and time synchronization.



### **3. Trees**
- A **tree** is a collection of one or more domains that share a contiguous namespace.
- For example, if `example.com` is the root domain, `sales.example.com` and `hr.example.com` would be child domains in the same tree.
- Domains in a tree are linked by **transitive trusts** (explained below).



### **4. Forests**
- A **forest** is the highest-level logical container in AD and consists of one or more domain trees.
- All domains in a forest share a common **schema**, **configuration**, and **global catalog**.
- The first domain created in a forest is called the **forest root domain**.
- Forests provide security boundaries; objects in one forest cannot access resources in another forest unless a **trust relationship** is established.



### **5. Trusts**
A **trust** is a relationship between two domains or forests that allows users in one domain to access resources in another. Trusts can be categorized based on **characteristics** and **directions**:

#### **Trust Based on Characteristics**
- **Transitive Trust**: Automatically extends to other domains in the same forest. For example, if Domain A trusts Domain B, and Domain B trusts Domain C, then Domain A implicitly trusts Domain C.
- **Non-Transitive Trust**: Does not extend beyond the two domains involved. For example, if Domain A trusts Domain B, and Domain B trusts Domain C, Domain A does **not** trust Domain C.

#### **Trust Based on Directions**
- **One-Way Trust**: Only one domain trusts the other. For example, Domain A trusts Domain B, but Domain B does not trust Domain A.
- **Two-Way Trust**: Both domains trust each other. This is the default trust relationship within a forest.

#### **Other Trust Types**
- **Shortcut Trust**: A manually created trust to improve authentication performance between two domains in a complex forest.
- **Forest Trust**: A trust between two forests, allowing cross-forest resource access.
- **External Trust**: A trust with a domain outside the forest, typically used for legacy systems.



### **6. Containers and Leaves**
- **Containers**: Objects in AD that can hold other objects. Examples include:
  - **Organizational Units (OUs)**: Used to organize and apply Group Policy Objects (GPOs) to users, computers, and groups.
  - **Domains**: The top-level containers in AD.
- **Leaves**: Objects that cannot contain other objects. Examples include:
  - **Users**: Represent individual accounts.
  - **Computers**: Represent devices joined to the domain.
  - **Groups**: Used to assign permissions to multiple users or computers.



### **7. Global Catalog (GC)**
- The **Global Catalog** is a distributed data repository that contains a partial replica of all objects in the forest.
- It enables fast searches for objects across domains and forests.
- The GC is also used for **universal group membership** lookups during authentication.



### **8. Schema**
- The **schema** defines the structure of the AD database, including object classes (e.g., user, computer) and attributes (e.g., `cn`, `sAMAccountName`).
- The schema is shared across all domains in a forest and is extensible to support custom attributes.



### **9. Replication**
- AD uses **multi-master replication** to synchronize data between DCs.
- Replication occurs within **sites** (high-speed LANs) and between sites (WANs) using the **Knowledge Consistency Checker (KCC)** to optimize replication topology.

### **10. Security Considerations**
- **Kerberos Authentication**: AD uses Kerberos for secure authentication. Each user and computer is issued a **Ticket Granting Ticket (TGT)** after successful login.
- **Group Policy**: Used to enforce security settings, such as password policies, account lockout policies, and software restrictions.
- **Privilege Escalation**: Misconfigured trusts or excessive permissions can lead to privilege escalation attacks (e.g., **Golden Ticket** attacks).
- **Forest Isolation**: Forests are security boundaries; compromising the forest root domain can lead to full forest compromise.



### **11. Common Attacks on AD**
- **Pass-the-Hash**: Exploits cached credentials to impersonate users.
- **Kerberoasting**: Extracts service account credentials from Kerberos tickets.
- **DCSync**: Mimics a DC to replicate sensitive data (e.g., password hashes).
- **Trust Exploitation**: Exploits misconfigured trusts to move laterally between domains or forests.



### **12. Best Practices for Securing AD**
- Implement **Least Privilege**: Grant users and systems only the permissions they need.
- Monitor **Privileged Accounts**: Regularly audit accounts with elevated privileges.
- Secure **Trust Relationships**: Limit the scope of trusts and avoid unnecessary external trusts.
- Enable **Auditing**: Monitor AD logs for suspicious activity.
- Regularly **Patch DCs**: Ensure all DCs are up to date with security patches.


This overview provides a foundational understanding of AD from both an administrative and cybersecurity perspective. As a cybersecurity student, you should focus on understanding how AD can be exploited and how to defend against such attacks.

**---**

### Securing and Authenticaiton


- securing communication and data integrity
- Using Group Policy Management Editor
![3fcb2f6dc2907f3ccaa05dd73d703dac](https://github.com/user-attachments/assets/a318c6e4-b9e7-4354-b89b-5b669e50b23c)

**LAN Manager Hash** 

The user account password for Windows isn't stored in clear text; instead, it stores passwords with two types of hash representation. When the password for any user account is changed or set with fewer than 15 characters, both LM hash (LAN Manager hash) and NT hash (Windows NT hash) are generated by Windows and can be stored in AD. The LM hash is relatively weaker than the NT and is prone to a fast brute-force attack. The best recommendation is to prevent Windows from storing the password's LM hash. You can access it through the following:

Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options > double click Network security - Do not store LM hash value on next password change policy > select "Define policy setting" 

![3a33943590f2d9431e975a762900a32b](https://github.com/user-attachments/assets/c0d49b03-cf54-416f-b1fd-ffedad1dc34c)

**SMB Signing**
SMB stands for Server Message Block. Generally, Microsoft-based networks utilise this protocol for file and print communication. Moreover, it allows secure transmission over the network. Configuring SMB signing through group policy is crucial to detect Man in the Middle (MiTM) attacks that may result in modification of SMB traffic in transit. SMB signing ensures the integrity of data for both client and server. All supported Windows versions have an SMB packet signing option.

Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options > double click Microsoft network server: Digitally sign communication (always) > select Enable Digitally Sign Communications
![46f40389033a68174450f9f97bf3a624](https://github.com/user-attachments/assets/128c3258-6234-46ee-880e-31cf2b347a5c)
![image](https://github.com/user-attachments/assets/39fad204-2d27-4e0b-b534-5d30624275fa)

**LDAP Signing**
Light Weight Directory Access Protocol (LDAP) enables locating and authenticating resources on the network. Hackers may introduce replay or MiTM attacks to launch custom LDAP requests. Therefore, LDAP signing is a Simple Authentication and Security Layer (SASL) property that only accepts signed LDAP requests and ignores other requests (plain-text or non-SSL). We can enable LDAP signing through the following:

Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options > Domain controller: LDAP server signing requirements > select Require signing from the dropdown
![465b558bb5818a308de03a599ff7f14f](https://github.com/user-attachments/assets/568ac7d5-6fac-4685-86e9-64451e49587d)
![image](https://github.com/user-attachments/assets/f3a5d2ff-ece7-45d0-b6fb-831d325189b9)

**Password Rotation **
Active Directory password security is critical to address because of security breaches and password reuse. It becomes challenging for any organisation to reset account passwords or update them everywhere, so they prefer not to do it. This scenario could have a few alternate approaches, and each method has pros and cons. 

   - **First Technique**: Creating a script to update passwords automatically in the Scheduled Task with the help of PowerShell. This method does not require any additional overhead and removes all the manual efforts for password rotation, but it requires you to write and maintain your script – which could be challenging. 
   - **Second Technique**: Add a Multi-Factor Authentication (MFA) solution to AD and choose not to change the password often. It adds a security layer, and you will not need to change your password often. You can read more about implementing MFA here.
   - **Third Technique**: Microsoft provides a solution for services account password rotation through Group Managed Services Accounts (gMSAs), which changes passwords after every 30 days. You can learn more about it here.

**Password Policies**
Attackers use various corporate password-compromise techniques, including brute force, dictionary, password spraying, credential attacks etc. All organisations must have a strict password policy to defend against all such attacks. Password policies mean different rules for creating passwords, including length, complexity, and changing frequency. For viewing and configuring the password policy, you can use the following:

Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy
![b7eb4e5bfb78c6744d05898ff3da8f83](https://github.com/user-attachments/assets/f2d76223-bba1-4291-861c-a791d2a6781d)

### Password Rotation and Active Directory (AD) Password Security

Active Directory (AD) password security is vital for mitigating risks such as security breaches, password reuse, and account compromises. Password rotation ensures that passwords are changed regularly to reduce the likelihood of unauthorized access, even if a password is compromised. However, enforcing password rotation can be operationally challenging, especially in large organizations where account management is complex.

Let’s explore the techniques mentioned for handling password rotation and their respective pros and cons.

---

### **1. Using PowerShell Scripts for Scheduled Password Rotation**

This approach involves creating and deploying PowerShell scripts to automatically update passwords at regular intervals using Windows Scheduled Tasks.

#### **How it Works:**
- A script is written in PowerShell to:
  - Generate a strong, random password.
  - Update the password for a specific account in Active Directory.
  - Optionally, update the password in applications or services dependent on that account.
- The script is executed periodically via a Scheduled Task on a Windows server or workstation.

#### **Advantages:**
- **Automation:** Eliminates manual efforts for password rotation.
- **Cost-Effective:** No need for third-party tools or solutions; relies on built-in Windows features.
- **Customizable:** Tailored to meet specific organizational requirements.

#### **Disadvantages:**
- **Complexity:** Writing, testing, and maintaining the script can be difficult, particularly for those without scripting expertise.
- **Error-Prone:** A poorly written or maintained script can cause service disruptions, e.g., if a dependent application fails to recognize the updated password.
- **Security Risks:** The script and its environment must be secured to prevent unauthorized access or misuse.

#### **Example Script:**
```powershell
# Example PowerShell script for password rotation
$AccountName = "ServiceAccount"
$NewPassword = [System.Web.Security.Membership]::GeneratePassword(16, 2)

# Update AD account password
Set-ADAccountPassword -Identity $AccountName -NewPassword (ConvertTo-SecureString $NewPassword -AsPlainText -Force)

# Log the change
Write-Output "Password for $AccountName updated successfully."
```

---

### **2. Implementing Multi-Factor Authentication (MFA)**

Instead of frequently rotating passwords, adding a Multi-Factor Authentication (MFA) layer can significantly improve security. MFA requires users to verify their identity using multiple factors, such as:
- Something they know (password).
- Something they have (a mobile device or security token).
- Something they are (biometric verification like fingerprints).

#### **Advantages:**
- **Enhanced Security:** Even if a password is compromised, the attacker cannot bypass the second authentication factor.
- **Reduced Password Management:** With MFA in place, organizations can increase the password expiration interval, reducing the need for frequent rotations.
- **User-Friendly:** Eliminates the frustration associated with remembering frequently changing passwords.

#### **Disadvantages:**
- **Initial Setup Effort:** Deploying MFA requires integration with existing systems and user onboarding.
- **Cost:** Some MFA solutions may involve licensing fees or require additional hardware.
- **Dependency on External Factors:** Authentication can fail if the secondary factor (e.g., mobile device or token) is unavailable.

#### **Example:**
- Implementing MFA with Microsoft Azure AD involves enabling conditional access policies to enforce MFA requirements for specific users or groups.

---

### **3. Using Group Managed Service Accounts (gMSAs)**

Group Managed Service Accounts (gMSAs) are an Active Directory feature designed for service accounts. These accounts automatically handle password rotation, eliminating manual intervention.

#### **How gMSAs Work:**
- gMSAs are tied to specific services or servers.
- AD manages the account’s password and rotates it every 30 days by default (this interval is configurable).
- Applications and services that use gMSAs retrieve the password programmatically.

#### **Advantages:**
- **Automated Rotation:** No need for manual intervention; AD handles everything.
- **High Security:** Passwords are not stored or shared; they are securely managed within AD.
- **Reduced Management Overhead:** Once set up, the system works seamlessly with minimal administrative effort.

#### **Disadvantages:**
- **Limited Applicability:** Only works with services and applications that support gMSAs.
- **Initial Setup Complexity:** Requires proper configuration of AD and delegation of rights to manage gMSAs.

#### **Example:**
1. Create a gMSA:
   ```powershell
   New-ADServiceAccount -Name "MyServiceAccount" -DNSHostName "myserver.domain.com" -PrincipalsAllowedToRetrieveManagedPassword "MyServerGroup"
   ```
2. Install the gMSA on a server:
   ```powershell
   Install-ADServiceAccount -Identity "MyServiceAccount"
   ```
3. Assign the gMSA to a service:
   Update the service properties to use the gMSA for authentication.

---

### **Comparison of Techniques**

| **Technique**                   | **Pros**                                                                 | **Cons**                                                                                  |
|----------------------------------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| PowerShell Scripts               | Cost-effective, customizable                                             | Requires expertise, risk of human error, ongoing maintenance                             |
| Multi-Factor Authentication (MFA)| Strong security, reduces password rotation frequency                     | Initial setup effort, potential costs, dependency on external factors                    |
| Group Managed Service Accounts   | Fully automated, highly secure                                           | Limited to specific use cases, complex initial setup                                     |

---

### **Choosing the Right Approach**

- **For general user accounts:** MFA is a robust choice, especially when frequent password rotation causes user frustration.
- **For service accounts:** gMSAs are ideal for services and applications that support them.
- **For custom or legacy environments:** PowerShell scripts may be necessary where other solutions are not viable.

Each organization should assess its requirements, resources, and technical expertise to determine the most suitable approach.

### Least Privilege Model

- Right type of accounts = User, Privilege, Shared
  - Shared accounts: These accounts are shared amongst a group of people, as the visitors with bare minimum privileges, to give limited access for a specific time. These accounts are not recommended and must be utilised in limited scenarios. 

- Role Based

**Tiered Access Model**  

The Active Directory Tiered Access Model (TAM) comprises plenty of technical controls that reduce the privilege escalation risks. It consists of a logical structure that separates Active Directory's assets by creating boundaries for security purposes. The primary goal is the protection of Active Directory's top-valued identities (Tier 0). At the same time, domain members and other users can perform routine tasks, such as email checking, surfing the internet, and using apps and other services (Tier 1, 2). It comprises three tiers, Tier 0, 1, and 2, which are as follows: 

 -   Tier 0: Top level and includes all the admin accounts, Domain Controller, and groups.
 -   Tier 1: Domain member applications and servers. 
 -   Tier 2: End-user devices like HR and sales staff (non-IT personnel).

The **Active Directory Tiered Access Model (TAM)** is a structured security framework designed to protect critical resources in an Active Directory (AD) environment by segregating access into three tiers. This approach reduces the risk of privilege escalation and unauthorized access by isolating administrative tasks from routine user activities.

---

### **Overview of the Tiered Access Model (TAM)**

TAM is based on the principle of **least privilege** and enforces security boundaries to limit the impact of potential compromises. Each tier has specific assets, roles, and access policies that help mitigate risks. Here’s how it is structured:

---

### **1. Tier 0: Critical Assets and Identities**
- **Description:** 
  - Tier 0 is the **most critical level** in the model, encompassing all highly privileged accounts, administrative systems, and sensitive resources essential for Active Directory security and operations.
  - Compromise at this level can allow attackers full control over the entire AD environment.
  
- **Examples of Tier 0 Assets:**
  - Domain Controllers (DCs).
  - AD Forest and Domain Admin accounts.
  - Enterprise Admin groups and associated service accounts.
  - Privileged Access Workstations (PAWs) used for administering Tier 0 systems.

- **Access Restrictions:**
  - Access to Tier 0 assets is limited to a small, trusted group of administrators.
  - Administrators must use secure devices (like PAWs) isolated from lower tiers to prevent lateral movement.

- **Primary Goal:** Protect the organization's most valued identities and critical AD infrastructure.

---

### **2. Tier 1: Servers and Application Management**
- **Description:** 
  - Tier 1 includes assets and accounts that manage domain-joined servers and business-critical applications.
  - These are **not as sensitive as Tier 0 assets**, but a compromise here could still result in significant disruption or an indirect path to Tier 0.

- **Examples of Tier 1 Assets:**
  - File servers, application servers, and web servers.
  - Administrative accounts and service accounts managing Tier 1 systems.
  - Business-critical applications like ERP systems or customer databases.

- **Access Restrictions:**
  - Tier 1 admins have elevated privileges to manage domain-joined servers and applications but are restricted from accessing Tier 0 systems.
  - Workstations or tools used for Tier 1 management must not overlap with those used for Tier 0.

- **Primary Goal:** Limit the risk of attackers moving from Tier 1 systems to Tier 0.

---

### **3. Tier 2: End-User Devices**
- **Description:** 
  - Tier 2 includes assets associated with everyday, non-administrative tasks performed by regular users.
  - These are the least sensitive systems in the hierarchy, but they are often the starting point for attackers due to phishing or malware.

- **Examples of Tier 2 Assets:**
  - Workstations and laptops used by end-users like HR, sales, or other non-IT personnel.
  - Accounts used for checking email, browsing the internet, or using standard applications.

- **Access Restrictions:**
  - Tier 2 users have minimal privileges and no administrative access to Tier 0 or Tier 1 assets.
  - End-user devices are typically configured with enhanced security settings, such as endpoint protection tools and least privilege access.

- **Primary Goal:** Ensure that routine user activities cannot compromise higher-tier systems.

---

### **Key Principles of the Tiered Model**

1. **Separation of Duties and Responsibilities:**
   - Admins managing Tier 0 resources should not have access to Tier 1 or Tier 2 devices, reducing the risk of lateral movement or privilege escalation.
   - Tier 1 admins should not access Tier 0 systems but can manage servers and applications in Tier 1.

2. **Access Isolation:**
   - Credentials from one tier cannot be used on assets belonging to another tier. For example:
     - Tier 0 credentials should not log into Tier 1 or Tier 2 systems.
     - Tier 1 credentials should not be used on Tier 2 workstations.

3. **Privileged Access Workstations (PAWs):**
   - Administrators of Tier 0 and Tier 1 systems must use dedicated, hardened devices (PAWs) to perform administrative tasks, ensuring their credentials are not exposed to compromised systems.

4. **Network Segmentation:**
   - Tiers are isolated from each other using network controls like firewalls and VLANs, restricting communication and lateral movement.

5. **Monitoring and Auditing:**
   - Logs and alerts are closely monitored to detect anomalies or unauthorized access attempts across the tiers.

---

### **Benefits of the Tiered Access Model**

1. **Risk Reduction:**
   - Compromises in lower tiers (e.g., end-user devices) are less likely to affect higher tiers, protecting critical AD assets.

2. **Improved Security Posture:**
   - By isolating administrative activities, the model minimizes the attack surface for privilege escalation and lateral movement.

3. **Operational Efficiency:**
   - Clear segmentation of roles and responsibilities streamlines management and simplifies access policies.

4. **Compliance:**
   - Helps organizations meet regulatory requirements by enforcing strict access control and auditing practices.

---

### **Example Scenario**
An organization experiences a phishing attack targeting Tier 2 users. Malware is installed on an end-user workstation. 
- **Impact:** The attack is contained to Tier 2 because the compromised credentials cannot access Tier 1 or Tier 0 systems.
- **Mitigation:** Admin accounts and critical AD resources remain secure, ensuring the organization can continue operations while addressing the issue at Tier 2.

---

The **Active Directory Tiered Access Model** is a robust security strategy for safeguarding critical systems and identities in complex AD environments. By enforcing logical boundaries and isolating access, organizations can effectively manage risks while maintaining operational efficiency.


Auditing


### Microsoft Security Compliance Toolkit MSCT 

Download > unzip > scripts > .ps1 run with powershell

#### Policy Analyser


![5a7f7844170f99d5085543d765cf5c5c](https://github.com/user-attachments/assets/098f2cb9-3087-4f0d-95ff-42208b7efd03)



![image](https://github.com/user-attachments/assets/33738c36-ecb3-493f-a5b1-13c57efeab1b)
![image](https://github.com/user-attachments/assets/4af54be1-9ca5-4b3b-b5c5-43e497a6e2e6)

##  Post Exploitation

some extra rooms: ZeroLogon, Breaching AD, Exploiting AD, Post Exploitation basics


### Kerberoasting (room acailable)
Kerberoasting is a common and successful post-exploitation technique for attackers to get privileged access to AD. The attacker exploits Kerberos Ticket Granting Service (TGS) to request an encrypted password, and then the attacker cracks it offline through various brute force techniques. These attacks are difficult to detect as the request is made through an approved user, and no unusual traffic pattern is generated during this process. You can prevent the attack by ensuring an additional layer of authentication through MFA or by frequent and periodic Kerberos Key Distribution Centre (KDC) service account password reset. You can learn more about the attack here.

**Publically Accessible Share**
During AD configuration, some share folders are publicly accessible or left unauthenticated, providing an initial foothold for attackers for lateral movement. You can use the Get-SmbOpenFile cmdlet in PowerShell to look for any undesired share on the network and configure access accordingly.

### **Kerberos: An Overview**

Kerberos is a network authentication protocol designed to provide strong authentication for client/server applications by using secret-key cryptography. It is the default authentication protocol used in **Active Directory (AD)** environments. Kerberos ensures secure authentication over non-secure networks by using tickets to prove identity.

---

### **Key Components of Kerberos**

1. **Key Distribution Center (KDC)**:
   - The KDC is the core component of Kerberos and consists of two services:
     - **Authentication Service (AS)**: Issues **Ticket Granting Tickets (TGTs)**.
     - **Ticket Granting Service (TGS)**: Issues **service tickets** for accessing resources.
   - The KDC is typically hosted on a Domain Controller (DC) in an AD environment.

2. **Ticket Granting Ticket (TGT)**:
   - A TGT is issued to a user after successful authentication (e.g., logging in).
   - The TGT is encrypted with the **KDC's secret key** and contains the user's identity and session key.
   - The TGT is used to request **service tickets** for accessing resources.

3. **Service Ticket (ST)**:
   - A service ticket is issued by the TGS and allows a user to access a specific resource (e.g., a file server or database).
   - The service ticket is encrypted with the **resource's secret key** and contains the user's identity and a session key.

4. **Session Key**:
   - A temporary encryption key generated by the KDC for secure communication between the client and the resource.

5. **Principal**:
   - A unique identity in Kerberos, such as a user or service account.

6. **Realm**:
   - A logical security boundary in Kerberos, equivalent to a domain in AD.

---

### **Kerberos Authentication Process**

The Kerberos authentication process involves the following steps:

1. **Authentication Request (AS-REQ)**:
   - The user sends a request to the AS for a TGT.
   - The AS verifies the user's credentials (e.g., password) and issues a TGT encrypted with the KDC's secret key.

2. **Ticket Granting Ticket (TGT)**:
   - The user receives the TGT and stores it in their **Ticket Cache**.

3. **Service Ticket Request (TGS-REQ)**:
   - The user sends the TGT to the TGS to request a service ticket for a specific resource.
   - The TGS verifies the TGT and issues a service ticket encrypted with the resource's secret key.

4. **Service Ticket (ST)**:
   - The user presents the service ticket to the resource.
   - The resource decrypts the ticket using its secret key and grants access.

5. **Mutual Authentication**:
   - Kerberos supports mutual authentication, where both the client and the resource verify each other's identity.

---

### **Kerberoasting: An Attack on Kerberos**

**Kerberoasting** is a post-exploitation attack that exploits the Kerberos protocol to extract service account credentials. It targets **Service Principal Names (SPNs)**, which are unique identifiers for services in AD.

---

### **How Kerberoasting Works**

1. **Service Accounts and SPNs**:
   - Service accounts are used to run services (e.g., SQL Server, IIS).
   - Each service account is associated with one or more SPNs (e.g., `MSSQLSvc/sqlserver.example.com`).

2. **Service Ticket Request**:
   - An attacker with a valid TGT requests a service ticket for a service account's SPN.
   - The TGS issues a service ticket encrypted with the service account's **NTLM hash**.

3. **Extracting the Service Ticket**:
   - The attacker extracts the service ticket from memory or network traffic.
   - The service ticket is encrypted with the service account's password hash.

4. **Offline Cracking**:
   - The attacker performs an **offline brute-force or dictionary attack** on the encrypted service ticket to recover the service account's password.

---

### **Steps to Perform Kerberoasting**

1. **Enumerate SPNs**:
   - Use tools like **PowerShell**, **Impacket**, or **BloodHound** to identify service accounts with SPNs.
   - Example PowerShell command:
     ```powershell
     Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
     ```

2. **Request Service Tickets**:
   - Use tools like **Mimikatz**, **Impacket's GetUserSPNs.py**, or **Rubeus** to request service tickets.
   - Example using Impacket:
     ```bash
     GetUserSPNs.py -dc-ip <DC_IP> <DOMAIN>/<USER>:<PASSWORD> -request
     ```

3. **Extract and Crack Tickets**:
   - Save the encrypted service tickets and use tools like **Hashcat** or **John the Ripper** to crack them.
   - Example Hashcat command:
     ```bash
     hashcat -m 13100 -a 0 <ticket_file> <wordlist>
     ```

---

### **Why Kerberoasting is Effective**

1. **Weak Passwords**:
   - Service accounts often have weak or static passwords.
2. **No MFA**:
   - Kerberos does not natively support multi-factor authentication (MFA).
3. **Stealthy**:
   - Kerberoasting does not generate suspicious logs, making it difficult to detect.

---

### **Mitigation and Defense**

1. **Use Strong Passwords**:
   - Ensure service accounts have long, complex passwords.
2. **Managed Service Accounts (MSAs)**:
   - Use MSAs or Group Managed Service Accounts (gMSAs) to automatically rotate passwords.
3. **Monitor SPNs**:
   - Regularly audit and remove unnecessary SPNs.
4. **Enable Logging**:
   - Monitor for unusual service ticket requests using tools like **SIEM**.
5. **Restrict Privileges**:
   - Limit the privileges of service accounts to minimize the impact of compromise.
6. **Kerberos Armoring**:
   - Use **FAST (Flexible Authentication Secure Tunneling)** to protect Kerberos messages.

---

### **Tools for Kerberoasting**

- **Impacket**: A Python toolkit for working with network protocols, including Kerberos.
- **Mimikatz**: A post-exploitation tool for extracting credentials from memory.
- **Rubeus**: A C# tool for Kerberos exploitation.
- **Hashcat/John the Ripper**: Password-cracking tools for offline attacks.

---

### **Example Scenario**

1. An attacker gains initial access to a low-privileged user account in an AD environment.
2. The attacker enumerates SPNs and identifies a service account running a SQL Server.
3. The attacker requests a service ticket for the SQL Server SPN.
4. The attacker extracts the encrypted service ticket and cracks it offline to recover the service account's password.
5. The attacker uses the compromised service account to move laterally or escalate privileges.

---

### **Conclusion**

Kerberos is a robust authentication protocol, but it is not immune to attacks like Kerberoasting. As a cybersecurity professional, understanding how Kerberos works and how it can be exploited is critical for securing AD environments. By implementing strong defenses and monitoring for suspicious activity, you can mitigate the risk of Kerberoasting and other Kerberos-based attacks.

![image](https://github.com/user-attachments/assets/546ef3fc-a425-4731-88e6-c8d8d1c5b28c)

To effectively harden Active Directory (AD) and enhance security, consider the following organized approach based on the cheat sheet:

### 1. **Privilege Management**
   - **Role-Based Access Control (RBAC):** Implement a role-based model to ensure users have only the permissions necessary for their roles, adhering to the principle of least privilege.
   - **Tiered Administrative Model:** Separate administrative roles into tiers (e.g., Tier0 for domain administrators), limiting high-level privileges to essential personnel.

### 2. **Account Security**
   - **Audit and Manage Accounts:** Regularly review and manage user accounts, ensuring that privileges are appropriately assigned and that there are no misconfigurations.
   - **Password Policies:** Enforce strong password policies, including regular rotation and complexity requirements, to protect against brute force attacks.

### 3. **Authentication Enhancements**
   - **Multi-Factor Authentication (MFA):** Implement MFA for additional security layers, especially for administrative accounts.
   - **SMB Signing:** Enable SMB signing to protect data integrity in file shares.
   - **Protect Against Credential Theft:** Be aware of attacks like Kerberoasting and implement measures to protect service account credentials.

### 4. **Remote Desktop Protocol (RDP) Security**
   - **Secure RDP Access:** Limit RDP access to necessary users, use Network Level Authentication (NLA), and ensure strong passwords are used.
   - **Monitor RDP Activity:** Keep an eye on RDP sessions for any unusual activity.

### 5. **Security Tools and Compliance**
   - **Use Security Tools:** Leverage tools like the Microsoft Security Compliance Toolkit to analyze and manage security policies.
   - **Security Baselines:** Implement and maintain security baselines to ensure consistency in security configurations across the domain.

### 6. **Regular Updates**
   - **Enable Auto-Updates:** Ensure that Windows machines are automatically updated to protect against known vulnerabilities and malware.

### 7. **Continuous Learning and Adaptation**
   - **Stay Informed:** Continuously update your knowledge about AD security, including understanding attack vectors like Kerberoasting and how to mitigate them.
   - **Explore Tools and Best Practices:** Delve into tools and best practices for managing group policies, securing accounts, and maintaining compliance.

By systematically addressing these areas, you can significantly enhance the security posture of your Active Directory environment, reducing the risk of unauthorized access and potential breaches.





