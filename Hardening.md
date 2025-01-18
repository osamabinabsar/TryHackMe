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




















