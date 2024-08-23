![image](https://github.com/user-attachments/assets/f327cb54-ba34-486c-90a8-c7b1520289d1)# Metasploit


**Exploit**: A piece of code that uses a vulnerability present on the target system.
**Vulnerability**: A design, coding, or logic flaw affecting the target system. The exploitation of a vulnerability can result in disclosing confidential information or allowing the attacker to execute code on the target system.
**Payload**: An exploit will take advantage of a vulnerability. However, if we want the exploit to have the result we want (gaining access to the target system, read confidential information, etc.), we need to use a payload. Payloads are the code that will run on the target system.
      - four different directories under payloads: adapters, singles, stagers and stages.
        - Adapters: An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.
        - Singles: Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
        - Stagers: Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
        - Stages: Downloaded by the stager. This will allow you to use larger sized payloads.


Metasploit has a subtle way to help you identify single (also called “inline”) payloads and staged payloads.

    generic/shell_reverse_tcp
    windows/x64/shell/reverse_tcp

Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the “_” between “shell” and “reverse”. While the latter is a staged payload, as indicated by the “/” between “shell” and “reverse”.

Msfconsole is managed by context; this means that unless set as a global variable, all parameter settings will be lost if you change the module you have decided to use. In the example below, we have used the ms17_010_eternalblue exploit, and we have set parameters such as RHOSTS. If we were to switch to another module (e.g. a port scanner), we would need to set the RHOSTS value again as all changes we have made remained in the context of the ms17_010_eternalblue exploit.  

Another essential piece of information returned is in the “rank” column. Exploits are rated based on their reliability. The table below provides their respective descriptions.
![a88c8d37283878e01447853a68578deb](https://github.com/user-attachments/assets/63b3732c-0db5-45b1-9407-90d205ef0f96)

Source: https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking 

        search type:auxiliary telnet command. 

_When dealing with Metasploit, you may see five different prompts:_

The regular command prompt: You can not use Metasploit commands here.

**Regular command prompt**

           
    root@ip-10-10-XX-XX:~#

        

The msfconsole prompt: msf6 (or msf5 depending on your installed version) is the msfconsole prompt. As you can see, no context is set here, so context-specific commands to set parameters and run modules can not be used here.

**Metasploit command prompt**

           
      msf6 >

        


A context prompt: Once you have decided to use a module and used the set command to chose it, the msfconsole will show the context. You can use context-specific commands (e.g. set RHOSTS 10.10.x.x) here.

**A context command prompt**

           
        msf6 exploit(windows/smb/ms17_010_eternalblue) >

        


The Meterpreter prompt: Meterpreter is an important payload we will see in detail later in this module. This means a Meterpreter agent was loaded to the target system and connected back to you. You can use Meterpreter specific commands here.

**A Meterpreter command prompt**

           
      meterpreter >

        

A shell on the target system: Once the exploit is completed, you may have access to a command shell on the target system. This is a regular command line, and all commands typed here run on the target system.

**A Meterpreter command prompt**

           
        C:\Windows\system32>

`You can use the setg command to set values that will be used for all modules. The setg command is used like the set command. The difference is that if you use the set command to set a value using a module and you switch to another module, you will need to set the value again. The setg command allows you to set the value so it can be used by default across different modules. You can clear any value set with setg using unsetg`


# Metasploit : Exploitation

?>

    search portscan

UDP service identificaiton     scanner/discovery/udp_sweep

SMB 
![image](https://github.com/user-attachments/assets/9036f27f-d96f-4ba8-b3cb-25cddb28bbf8)

_use smb_login for smb password enumeration_



![image](https://github.com/user-attachments/assets/2124fb65-a123-46be-9af4-fdb5a545d50a)
db_nmap saves map scans in the database

    hosts -h
    services -h
    hosts -R      add this value tothe RHOSTS parameter
      
![image](https://github.com/user-attachments/assets/3807bacf-23ae-4106-bf08-47fb747dc13a)
    services -S netnbios

## Vulnerability Scanning

![image](https://github.com/user-attachments/assets/86fd5190-4015-4949-a5f3-875b0bdf9c07)


##### migrate command in windows through meterpreter can allow us to migrate to different process and do privelege excalation. [3]

![image](https://github.com/user-attachments/assets/09ba097d-d0c7-481e-9eb4-e7da9d21e56e)

![image](https://github.com/user-attachments/assets/3082a903-e0cc-4569-91c7-98ccca5b0ecf)

![image](https://github.com/user-attachments/assets/3988fdcc-64ab-467b-b177-6e28cd2d8f38)

![image](https://github.com/user-attachments/assets/ec57629f-d343-4972-bbb7-705383a7eb94)

The hash is gained using murphy username and pass and upgrading tty shell using python and ohter command
![image](https://github.com/user-attachments/assets/4fbca69a-7b21-4187-a258-8923afbc1037)
![image](https://github.com/user-attachments/assets/9e902aa9-b9a3-43da-bc7e-7d34fff84c0c)
![image](https://github.com/user-attachments/assets/bff42c49-acfe-4b43-9763-ed36175ea9d7)
![image](https://github.com/user-attachments/assets/80a59c3a-c7ca-4bfe-b189-835c9252a468)

#### searching gtfobins for possible files that can be 
      sudo -l
**but sudoing cat /etc/shadow gives the hashes**



# Metasploit : Meterpreter

Meterpreter runs in RAM to avoid being detected
![image](https://github.com/user-attachments/assets/3a45626c-294b-46de-8fa6-79d771695798)

Not even DLL(Dynamic Link Libraries) will have meterpreter.dll
Meterpreter willl establish TLS 
![image](https://github.com/user-attachments/assets/672273c0-84c1-4e93-a9e6-3fdab4085567)
![image](https://github.com/user-attachments/assets/a58961ce-1057-43bc-abf0-9825892f1729)
![image](https://github.com/user-attachments/assets/53381c67-0966-4cde-8b5c-40ff4e802f11)
![image](https://github.com/user-attachments/assets/35ff2e14-2548-400f-8e57-7a54b0bd112b)
![image](https://github.com/user-attachments/assets/59c774cd-53a8-40a5-8f12-eefd9b679307)
![image](https://github.com/user-attachments/assets/9c831fd4-b95d-4e99-8bd2-7c1ed24c28f1)
![image](https://github.com/user-attachments/assets/9232ca73-44cc-4e64-8c07-91e41442b509)
![image](https://github.com/user-attachments/assets/f976cede-6e39-491f-b88b-ba5e2828aff8)





----------------------------------------------
###### 

**PostgreSQL** is a powerful, open-source relational database management system (RDBMS) known for its advanced features, robustness, and extensibility. It's often used in enterprise environments due to its support for complex queries, data integrity, and scalability.

### Key Features of PostgreSQL

1. **ACID Compliance**: PostgreSQL is fully ACID-compliant (Atomicity, Consistency, Isolation, Durability), ensuring reliable transactions and data integrity.

2. **Extensibility**: PostgreSQL supports custom data types, operators, and functions, and even allows users to write extensions in various programming languages.

3. **Support for SQL Standards**: PostgreSQL adheres closely to SQL standards, providing a comprehensive SQL implementation with advanced features like window functions, common table expressions (CTEs), and recursive queries.

4. **Procedural Languages**: Besides SQL, PostgreSQL supports procedural languages like PL/pgSQL (native), PL/Python, PL/Perl, and others, allowing for complex logic within the database.

5. **Concurrency Control**: PostgreSQL uses Multi-Version Concurrency Control (MVCC) to handle multiple transactions concurrently without locking the database, which enhances performance.

6. **Advanced Indexing Techniques**: It supports a variety of indexing methods, including B-tree, hash, GiST, SP-GiST, GIN, and BRIN, which are suitable for different types of queries and data.

7. **Full-Text Search**: PostgreSQL offers powerful full-text search capabilities, allowing users to search for text within columns efficiently.

8. **Replication and High Availability**: It supports streaming replication, logical replication, and various high-availability solutions like failover, backup, and point-in-time recovery.

9. **JSON and NoSQL Capabilities**: PostgreSQL has robust support for JSON data types and operations, enabling it to function as both a relational and a NoSQL database.

10. **Community and Ecosystem**: PostgreSQL has a strong community and a rich ecosystem of tools, extensions, and libraries.

### Use Cases
- **Web Applications**: Many large-scale web applications use PostgreSQL due to its performance and scalability.
- **Data Warehousing**: PostgreSQL's powerful querying and indexing features make it suitable for data warehousing.
- **Geospatial Data**: With the PostGIS extension, PostgreSQL is widely used for geographic information systems (GIS).
- **Enterprise Applications**: Its robustness and compliance with standards make it a popular choice for enterprise systems.

### Advantages
- **Open Source**: It's free to use and has a permissive open-source license (PostgreSQL License).
- **Cross-Platform**: Runs on various operating systems, including Linux, Windows, and macOS.
- **Strong Security**: PostgreSQL offers advanced security features like SSL, authentication methods, and row-level security.

### Conclusion
PostgreSQL is a versatile and powerful database system suitable for a wide range of applications, from small web apps to large-scale enterprise solutions. It’s known for its stability, extensibility, and strong support for SQL standards.




###### 2 SMTP servers for open relay
An **open relay** is a misconfigured SMTP (Simple Mail Transfer Protocol) server that allows anyone on the internet to send emails through it, without authentication. This means that the server will relay email messages from any sender to any recipient, regardless of whether the sender is authorized to use the server.

### What Does This Mean?

1. **SMTP Basics:**
   - SMTP is the protocol used to send emails across the internet. When you send an email, your email client connects to an SMTP server, which then forwards the message to the recipient's email server.

2. **Normal SMTP Behavior:**
   - Typically, an SMTP server is configured to only allow authenticated users to send emails. This means that to send an email through the server, you must provide valid credentials (e.g., a username and password).
   - Additionally, SMTP servers often restrict email sending to specific domains or IP addresses to prevent unauthorized use.

3. **Open Relay Behavior:**
   - In an **open relay**, the SMTP server is configured to allow email relaying without authentication or restriction. This means that anyone, anywhere, can connect to the server and use it to send emails to anyone else.
   - For example, an attacker could connect to an open relay SMTP server and send out spam or phishing emails, making it look like the emails came from a legitimate source.

### Risks and Consequences of an Open Relay:

1. **Spam and Abuse:**
   - Open relay servers are often exploited by spammers to send massive amounts of unsolicited emails. This can lead to the server's IP address being blacklisted by spam filters, which can prevent legitimate emails from being delivered.

2. **Phishing and Scams:**
   - Attackers can use open relays to send phishing emails that appear to come from trusted sources, increasing the likelihood that recipients will fall for the scam.

3. **Reputation Damage:**
   - Organizations that inadvertently run open relay servers risk damaging their reputation if their server is used for malicious purposes. They may be seen as complicit in the abuse, even if it was unintentional.

4. **Legal and Regulatory Issues:**
   - Some jurisdictions have regulations against operating open relay servers due to the potential for abuse. Organizations that fail to secure their SMTP servers may face legal consequences.

### Detecting and Preventing Open Relay:

1. **Testing for Open Relay:**
   - You can test whether an SMTP server is an open relay by attempting to send an email through it without providing authentication. There are also online tools and services that can check for open relays.

2. **Securing SMTP Servers:**
   - **Authentication:** Ensure that the SMTP server requires authentication (e.g., SMTP-AUTH) before allowing email sending.
   - **Access Control:** Restrict email relaying to trusted IP addresses or networks.
   - **Proper Configuration:** Regularly audit the server's configuration to ensure it is not inadvertently allowing open relays.

3. **Monitoring:**
   - Continuously monitor SMTP logs for unusual activity, such as a large number of emails being sent from unknown or unauthorized users.

### Summary:

An open relay is an SMTP server that allows anyone to send emails through it without authentication, which can lead to misuse, such as spamming and phishing. This type of misconfiguration poses significant risks, including damage to reputation, legal issues, and the potential for the server to be blacklisted. Properly securing and configuring SMTP servers is essential to prevent them from becoming open relays.

###### 3 
The `migrate` command in Meterpreter is a powerful feature that allows you to move the Meterpreter session from the currently compromised process to another process running on the target system. This can be useful for a variety of reasons, including privilege escalation, stability, and stealth.

### How the `migrate` Command Works

1. **Initial Compromise:**
   - When you first exploit a target system, Meterpreter often runs in the context of the process that was initially exploited. This process may not have the privileges or stability needed for certain post-exploitation activities.

2. **Using the `migrate` Command:**
   - The `migrate` command allows you to move the Meterpreter session into another process on the target system. This is done by injecting the Meterpreter payload into the memory space of the chosen process.
   - The process you migrate to could be more stable (e.g., a system service that is unlikely to be closed) or could have higher privileges (e.g., a process running as the SYSTEM user).

### Why Use the `migrate` Command?

1. **Privilege Escalation:**
   - If you initially compromise a process running with low privileges, you can use the `migrate` command to move to a process that is running with higher privileges, such as `SYSTEM`. This can allow you to execute commands with higher permissions, effectively escalating your privileges on the target system.

2. **Stability:**
   - Some processes are more stable and less likely to be terminated by the operating system or the user. By migrating to such a process, you reduce the risk of losing your session if the original process is closed.

3. **Stealth:**
   - Migrating to a legitimate system process can help you blend in with regular system activity, making it less likely for your presence to be detected by antivirus software, intrusion detection systems (IDS), or a vigilant system administrator.

### Example of Privilege Escalation Using `migrate`

1. **Compromise a Low-Privilege Process:**
   - Suppose you exploit a web application vulnerability, and your Meterpreter session is running in the context of a low-privileged user process, like `iexplore.exe` (Internet Explorer).

2. **Identify a Higher Privileged Process:**
   - Use the `ps` command in Meterpreter to list all running processes on the target system. Look for a process running as `SYSTEM` or with higher privileges than your current process. For example, `lsass.exe` (Local Security Authority Subsystem Service) typically runs with SYSTEM privileges.

3. **Migrate to the Higher Privileged Process:**
   - Use the `migrate` command to move your Meterpreter session to the higher privileged process.
   - Example:
     ```
     migrate 1234
     ```
     Here, `1234` is the Process ID (PID) of the target process you want to migrate to, such as `lsass.exe`.

4. **Gain SYSTEM Privileges:**
   - Once successfully migrated, your Meterpreter session is now running with the privileges of the target process, which might be `SYSTEM`. You can confirm this by running the `getuid` command to check your current user context.

5. **Execute Privileged Actions:**
   - With elevated privileges, you can now perform actions that were previously restricted, such as dumping password hashes, disabling security mechanisms, or installing persistent backdoors.

### Potential Risks:

- **Process Stability:** Migrating to a critical system process (like `lsass.exe`) can be risky because crashing or disrupting this process can cause system instability or even a crash.
- **Detection:** If the process you migrate to is being actively monitored (e.g., by an IDS or antivirus), the migration might trigger alarms.

### Summary:

The `migrate` command in Meterpreter allows you to move your session to another process on the target system, which can help with privilege escalation, maintaining a stable session, and improving stealth. By migrating to a process with higher privileges, such as a SYSTEM-level process, you can gain more control over the compromised system and perform a wider range of post-exploitation activities.
