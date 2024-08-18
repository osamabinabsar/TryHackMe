# Active Directory Basics

- The server that runs the Active Directory services is known as a Domain Controller (DC).
The main advantages of having a configured Windows domain are:

Centralised identity management: All users across the network can be configured from Active Directory with minimum effort.
Managing security policies: You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

### Task 3 -  Active Directoryu

The core of any Windows Domain is the Active Directory Domain Service (AD DS). This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others.


Users are one of the objects known as security principals, meaning that they can be authenticated by the domain and can be assigned privileges over resources like files or printers. You could say that a security principal is an object that can act upon resources in the network.

##### Security Principals in Active Directory: 
Security principals in Active Directory (AD) refer to the entities that can be authenticated and granted access to resources within a Windows environment. These entities include users, groups, computers, and service accounts, each with a unique security identifier (SID). Here's a detailed explanation of each type of security principal in Active Directory:

###### 1. **User Accounts**
   - **Description:** User accounts represent individuals who need access to resources in the network. Each user account has a unique SID that identifies the user within the domain.
   - **Purpose:** 
     - Authenticate users to grant access to domain resources.
     - Define permissions and access control to various resources, such as files, folders, and applications.
   - **Example:** An employee's user account (e.g., `jdoe`) in an organization.

###### 2. **Group Accounts**
   - **Description:** Groups are collections of user accounts, computer accounts, and other groups. Groups simplify the management of permissions by allowing administrators to assign access rights to a group rather than individual users.
   - **Types:**
     - **Security Groups:** Used to assign permissions to resources. Members of a security group inherit the permissions granted to the group.
     - **Distribution Groups:** Used for email distribution lists and cannot be used to assign permissions.
   - **Purpose:** 
     - Simplify permissions management by grouping multiple users and computers.
     - Facilitate role-based access control.
   - **Example:** A security group like `HR_Managers` might have permissions to access HR documents.

###### 3. **Computer Accounts**
   - **Description:** Computer accounts represent computers that are joined to the domain. Each computer in the domain has its own account, with a unique SID, used for authentication and security.
   - **Purpose:** 
     - Authenticate computers as they join the domain.
     - Apply Group Policies to computers for configuration management.
   - **Example:** A computer named `Workstation-01` in the domain might have a computer account `WORKSTATION-01$`.

###### 4. **Service Accounts**
   - **Description:** Service accounts are special types of accounts used by services and applications to interact with the operating system and network resources. They can be managed by administrators or managed automatically by the system.
   - **Types:**
     - **Local Service Account:** A predefined local account used by the operating system for running services.
     - **Network Service Account:** Similar to the Local Service account but with network credentials.
     - **Managed Service Accounts (MSAs):** Domain accounts that are automatically managed by the domain controller for services.
     - **Group Managed Service Accounts (gMSAs):** Similar to MSAs, but they can be used by multiple servers.
   - **Purpose:** 
     - Run applications and services with specific security contexts.
     - Securely manage service credentials and permissions.
   - **Example:** A web service running under a `gMSA` that accesses a SQL database.

###### 5. **Built-in Accounts**
   - **Description:** These are default accounts created automatically when Active Directory is installed. They have predefined roles and privileges.
   - **Common Built-in Accounts:**
     - **Administrator:** The default account with full control over the domain.
     - **Guest:** A limited access account for temporary users.
     - **krbtgt:** A service account used by the Kerberos Key Distribution Center (KDC) for ticket-granting services.
   - **Purpose:** 
     - Provide essential administrative capabilities and system functions.
   - **Example:** The `Administrator` account used to manage the domain.

###### 6. **Foreign Security Principals**
   - **Description:** Foreign security principals represent security principals from external trusted domains or forests. They are used when users or groups from one domain need to access resources in another domain.
   - **Purpose:** 
     - Enable cross-domain or cross-forest resource access in trusted environments.
   - **Example:** A user from a trusted external domain who needs access to resources in your domain.

###### **Key Concepts Related to Security Principals:**

- **Security Identifier (SID):** A unique identifier assigned to each security principal, used internally by Windows to manage permissions and access control.
  
- **Access Control Lists (ACLs):** Lists of permissions attached to objects in the directory. These specify which security principals have what type of access to the object.

- **Group Policy:** A feature that allows centralized management and configuration of operating systems, applications, and users' settings. It can be applied to users and computers based on their security principal type.

###### **Summary:**

Security principals in Active Directory encompass all the entities that can be authenticated and granted permissions within a domain. They include user accounts, groups, computer accounts, service accounts, and built-in accounts, each playing a distinct role in managing security and access control within an organization.

*Machine Account*
- has limited rights
- local admisnistrators on the assigned computer
- Note: Machine Account passwords are automatically rotated out and are generally comprised of 120 random characters.
- The machine account name is the computer's name followed by a dollar sign. For example, a machine named DC01 will have a machine account called DC01$.

*Security Groups* 
-----------------------------------
| Security Group |	Description | 
|-----------------|--------------------|
| Domain Admins	|  Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
| Server Operators	| Users in this group can administer Domain Controllers. They cannot change any administrative group memberships. |
| Backup Operators |	Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers. |
| Account Operators	| Users in this group can create or modify other accounts in the domain. |
| Domain Users	 | Includes all existing user accounts in the domain. |
| Domain Computers	| Includes all existing computers in the domain. |
| Domain Controllers	| Includes all existing DCs on the domain. |
--------------------------------------------------------------------------



Organizational Units (OUs) which are container objects that allow you to classify users and machines. OUs are mainly used to define sets of users with similar policing requirements. The people in the Sales department of your organisation are likely to have a different set of policies applied than the people in IT, for example. Keep in mind that a user can only be a part of a single OU at a time.



Creating new Organizational Unit in AD
![image](https://github.com/user-attachments/assets/a897dfc0-4c3d-4c20-8650-60b836fa6f0c)

These containers are created by Windows automatically and contain the following:

 **Builtin**: Contains default groups available to any Windows host.
 
 **Computers**: Any machine joining the network will be put here by default. You can move them if needed.
 
 **Domain** Controllers: Default OU that contains the DCs in your network.
 
 **Users**: Default users and groups that apply to a domain-wide context.
 
 **Managed** Service Accounts: Holds accounts used by services in your Windows domain.

Security Groups vs OUs

You are probably wondering why we have both groups and OUs. While both are used to classify users and computers, their purposes are entirely different:

- OUs are handy for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user.
- Security Groups, on the other hand, are used to grant permissions over resources. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be a part of many groups, which is needed to grant access to multiple resources.


**Os are protected from accidental deletion, to delete those, option have to be enabled from view menu > Advanced Features**
![image](https://github.com/user-attachments/assets/d4bbfcf3-0638-4167-830f-e9032101c10c)
![image](https://github.com/user-attachments/assets/2f2b5ec1-8c88-4222-a7a2-a89113857c08)
![image](https://github.com/user-attachments/assets/18920f62-384b-421b-9197-11b521589a9a)
Remove the option of protect object... from properties > Object tab.
![image](https://github.com/user-attachments/assets/6e36cac1-3366-4ff5-b8af-3f5c32bba054)


#### Delegation

One of the nice things you can do in AD is to give specific users some control over some OUs. This process is known as delegation and allows you to grant users specific privileges to perform advanced tasks on OUs without needing a Domain Administrator to step in.
![image](https://github.com/user-attachments/assets/8a21ebdb-2aa0-4da9-9fc1-26da61bccf0d)
_Note that we right click on the OU for which we want to delegate_

##### When a user does not have the privelege of opening Active Directory control panel, PowerShell can be sued to do the tasks.
![image](https://github.com/user-attachments/assets/edebb782-9878-4047-8558-7eb6faa8604e)

**Below Image shows the error when Phillip does not have the requited privileges to change the passowrd**
![image](https://github.com/user-attachments/assets/f76c0ab0-0ba3-45b6-996c-7c44f4dc09a7)

**After permissions granted**


###  Task 5 Managing Computers in AD

devices divided into at least the three following categories:
1. devices divided into at least the three following categories:
   - These devices should never have a privileged user signed into them.
2. Servers
3. Domain Controllers
    - These devices are often deemed the most sensitive devices within the network as they contain hashed passwords for all user accounts within the environment.
  

###  Task 6 Group Policies
Group Policy Objects (GPO). GPOs are simply a collection of settings that can be applied to OUs. GPOs can contain policies aimed at either users or computers, allowing you to set a baseline on specific machines and identities.

To configure Group Policies, you first create a GPO under Group Policy Objects and then link it to the OU where you want the policies to apply. 

The Settings tab includes the actual contents of the GPO and lets us know what specific configurations it applies. As stated before, each GPO has configurations that apply to computers only and configurations that apply to users only. I

Editing GPO
![b71d8de9e74d129d0ad4142863deadc4](https://github.com/user-attachments/assets/d8e12106-0f9c-4cfa-b4eb-56b7516ae1e3)
![bd3665c2569aa8fbe4f7482a5750f018](https://github.com/user-attachments/assets/6d3c08ec-0adf-40b7-954c-e310da7cd27d)


#### GPO distribution
GPOs are distributed to the network via a network share called SYSVOL, which is stored in the DC. All users in a domain should typically have access to this share over the network to sync their GPOs periodically. The SYSVOL share points by default to the C:\Windows\SYSVOL\sysvol\ directory on each of the DCs in our network.
Once a change has been made to any GPOs, it might take up to 2 hours for computers to catch up. If you want to force any particular computer to sync its GPOs immediately, you can always run the following command on the desired computer:
Windows PowerShell          PS C:\> gpupdate /force

### If we want to change anything specific to user, we should look for the settings under User Configuration

For the first GPO, regarding screen locking for workstations and servers, we could directly apply it over the Workstations, Servers and Domain Controllers OUs we created previously.

While this solution should work, an alternative consists of simply applying the GPO to the root domain, as we want the GPO to affect all of our computers. Since the Workstations, Servers and Domain Controllers OUs are all child OUs of the root domain, they will inherit its policies.

**Note: You might notice that if our GPO is applied to the root domain, it will also be inherited by other OUs like Sales or Marketing. Since these OUs contain users only, any Computer Configuration in our GPO will be ignored by them.**
![44c0cde18837cb6333c78749356ac0ee](https://github.com/user-attachments/assets/c83052ad-5f5a-47d0-ace3-cb72442cb7fa)

###  Task 7 Athentication Methods
- Windows domains, all credentials are stored in the Domain Controllers.
- Two protocols can be used for network authentication in windows domains:
     - Kerberos: Used by any recent version of Windows. This is the default protocol in any recent domain.
     - NetNTLM: Legacy authentication protocol kept for compatibility purposes.
##### Kerberos Authenticaiton Process:
       1. Encrypted username and timestamp is sent using key derived form pass ot Key Distribution Center
       2. The KDC will create and send back a Ticket Granting Ticket (TGT), which will allow the user to request additional tickets to access specific services. The need for a ticket to get more tickets may sound a bit weird, but it allows users to request service tickets without passing their credentials every time they want to connect to a service. Along with the TGT, a Session Key is given to the user, which they will need to generate the following requests.
       3. When a user wants to connect to a service on the network like a share, website or database, they will use their TGT to ask the KDC for a Ticket Granting Service (TGS). TGS are tickets that allow connection only to the specific service they were created for. To request a TGS, the user will send their username and a timestamp encrypted using the Session Key, along with the TGT and a Service Principal Name (SPN), which indicates the service and server name we intend to access.
       4. As a result, the KDC will send us a TGS along with a Service Session Key, which we will need to authenticate to the service we want to access. The TGS is encrypted using a key derived from the Service Owner Hash. The Service Owner is the user or machine account that the service runs under. The TGS contains a copy of the Service Session Key on its encrypted contents so that the Service Owner can access it by decrypting the TGS.
         
![d36f5a024c20fb480cdae8cd09ddc09f](https://github.com/user-attachments/assets/3d0b562d-89a9-488c-ad2e-8f63c41c23a2)

![d36f5a024c20fb480cdae8cd09ddc09f](https://github.com/user-attachments/assets/0980de9f-02b8-4e1c-8ffa-b6c68505d064)
![d36f5a024c20fb480cdae8cd09ddc09f](https://github.com/user-attachments/assets/bc00e6b2-7b7a-4359-b10e-764da71001a8)
![d36f5a024c20fb480cdae8cd09ddc09f](https://github.com/user-attachments/assets/d5676718-54b3-47d2-b54e-54202a76a313)

#####  NetNTLM Authentication
NetNTLM works using a challenge-response mechanism. The entire process is as follows:
1. The client sends an authentication request to the server they want to access.
2. The server generates a random number and sends it as a challenge to the client.
3. The client combines their NTLM password hash with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.
4. The server forwards the challenge and the response to the Domain Controller for verification.
5. The domain controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If they both match, the client is authenticated; otherwise, access is denied.
6. The authentication result is sent back to the server.
7. The server forwards the authentication result to the client.
   **Note that the user's password (or hash) is never transmitted through the network for security.**
   
![2eab5cacbd0d3e9dc9afb86169b711ec](https://github.com/user-attachments/assets/fda6ebfc-f5df-4fb2-b570-7bf084607d90)

**Note: The described process applies when using a domain account. If a local account is used, the server can verify the response to the challenge itself without requiring interaction with the domain controller since it has the password hash stored locally on its SAM.**


         A new security group needs to be introduced when talking about trees and forests. The Enterprise Admins group will grant a user administrative privileges over all of an enterprise's domains. Each domain would still have its Domain Admins with administrator privileges over their single domains and the Enterprise Admins who can control everything in the enterprise.

**Trust Realtionships:**^2
When an object needs to access another object within a forest but different Tree, a proccess is set up by joining trees and forests known as trust relationships.
The simplest trust relationship that can be established is a one-way trust relationship. In a one-way trust, if Domain AAA trusts Domain BBB, this means that a user on BBB can be authorised to access resources on AAA:

Trusts![af95eb1a4b6c672491d8989f79c00200](https://github.com/user-attachments/assets/7c950b48-1b85-457e-855a-c7822ef99c91)


The direction of the one-way trust relationship is contrary to that of the access direction.

Two-way trust relationships can also be made to allow both domains to mutually authorise users from the other. By default, joining several domains under a tree or a forest will form a two-way trust relationship.

It is important to note that having a trust relationship between domains doesn't automatically grant access to all resources on other domains. Once a trust relationship is established, you have the chance to authorise users across different domains, but it's up to you what is actually authorised or not.




___________________________________________________
![AD Tree explanatioon](https://github.com/user-attachments/assets/77001d4e-e040-453d-bc60-acf7dcf490f2)
### What is `thm.local`?

In the image you provided, `thm.local` is the **domain name** in the Active Directory (AD) environment. A domain in AD is a logical grouping of objects such as users, computers, and other resources that are managed under a single namespace. It is the central point of management for all the objects within it.

### Understanding the Tree Structure:

The tree structure shown in your image represents the **Active Directory hierarchy** within the `thm.local` domain. Let's break down the different elements:

1. **thm.local**: 
   - This is the **root of the domain**. It's the top level of the AD hierarchy for your environment, under which all objects and organizational units (OUs) reside.

2. **Organizational Units (OUs)**:
   - **Built-in**: This OU contains default groups and accounts that are created automatically when the domain is set up. It includes groups like Administrators, Users, etc., which have specific roles and permissions.
   - **Computers**: This OU is where computer accounts are automatically placed when computers join the domain, unless they are manually moved to another OU.
   - **Domain Controllers**: This contains the accounts of the domain controllers, which are servers responsible for the authentication of users and managing the AD database.
   - **ForeignSecurityPrincipals**: This contains security principals (users or groups) from trusted external domains or forests.
   - **Managed Service Accounts**: This OU holds service accounts that are automatically managed by the system.
   - **Program Data**: This is a system container used for storing application-specific data.
   - **System**: This OU contains system-related information and objects that are necessary for AD's operation, like DNS-related records.
   - **THM**: This is a custom OU created for organizing objects. It has sub-OUs like IT, Management, Marketing, Sales, and Students.
     - Each of these sub-OUs (like IT, Management, etc.) may contain users, computers, and other objects relevant to that department.

3. **Users**: This OU contains user accounts and groups that are not placed in custom OUs. It is the default location for users and groups created in the domain.

4. **NTDS Quotas**: This is used for managing and limiting the number of objects that can be created by users within the domain.

5. **TPM Devices**: This OU is for managing Trusted Platform Module (TPM) information associated with computers in the domain.

### Referring to Entities in Active Directory:

Yes, you can refer to everything within the `thm.local` domain as **objects**. In Active Directory, the term "object" is a broad one and can refer to any of the following:

- **Users**: Accounts representing individuals in the domain.
- **Groups**: Collections of users, computers, or other groups.
- **Computers**: Accounts representing physical or virtual machines.
- **Organizational Units (OUs)**: Containers used to organize other objects within the domain.
- **Service Accounts**: Accounts used by services or applications.
- **Domain Controllers**: Servers that hold the AD database and perform authentication.

Each of these entities is indeed an **object** in Active Directory. The entire directory structure, including OUs, users, groups, computers, and even certain system components, are all considered objects in AD.

### Summary:

- **thm.local** is your domain.
- The tree structure represents the hierarchical organization of your AD objects.
- You can refer to any entity within the AD as an **object**, whether it's a user, computer, group, OU, or even domain controllers and built-in system containers. 

This object-oriented structure is fundamental to how Active Directory organizes and manages resources in a domain.

_______________________________________________________________________________________
###### 2 
In Active Directory (AD), **trust relationships** are connections between two domains or forests that allow users in one domain to access resources in another domain. Trust relationships facilitate resource sharing and user authentication across different domains, helping to extend security boundaries and streamline access management.

### Key Concepts of Trust Relationships:

1. **Trust Directions**:
   - **One-Way Trust**: In a one-way trust, one domain (the trusting domain) allows access to its resources by users from another domain (the trusted domain). However, the reverse is not true unless a separate trust is established.
   - **Two-Way Trust**: This is a bidirectional trust where both domains trust each other, allowing users from either domain to access resources in the other domain.

2. **Trust Types**:
   - **Parent-Child Trust**: Automatically established when a new child domain is created within a domain tree. It is a two-way, transitive trust.
   - **Tree-Root Trust**: Automatically established when a new tree is added to an existing forest. This trust is also two-way and transitive.
   - **External Trust**: A manually created trust between two domains in different forests or between a domain in an Active Directory environment and a domain in a Windows NT 4.0 environment. This is typically a one-way, non-transitive trust.
   - **Forest Trust**: A manually created trust between two forests that allows access to resources across all domains within those forests. This is a two-way, transitive trust.
   - **Shortcut Trust**: A manually created trust that optimizes the authentication process between two domains in the same forest but in different trees, reducing the time it takes to navigate the trust paths.
   - **Realm Trust**: A trust between an Active Directory domain and a non-Windows Kerberos realm, typically used for interoperability with UNIX/Linux environments. This can be one-way or two-way, transitive or non-transitive.

3. **Trust Attributes**:
   - **Transitive Trust**: A trust that can extend beyond two domains to include other trusted domains. For example, if Domain A trusts Domain B, and Domain B trusts Domain C, then Domain A can also trust Domain C through transitive trust.
   - **Non-Transitive Trust**: A trust that is limited to the two domains involved in the trust. It does not extend to other domains.

4. **Trust Authentication Levels**:
   - **Forest-Wide Authentication**: Users in the trusted forest can authenticate to resources in the trusting forest without needing explicit permissions on each resource.
   - **Selective Authentication**: Requires explicit permissions to be set for users from the trusted domain or forest to access resources in the trusting domain or forest. This is a more secure, restrictive option.

### Common Uses of Trust Relationships:
- **Mergers and Acquisitions**: Trust relationships can be established between domains of different companies to allow resource sharing during a merger or acquisition.
- **Resource Sharing**: Trusts enable users in one domain to access resources like files, printers, and applications in another domain without requiring separate credentials.
- **Cross-Forest Collaboration**: In environments with multiple forests, trust relationships enable seamless collaboration and resource access across different parts of the organization.

### Management and Security Considerations:
- **Trust Monitoring**: Regularly monitor and review trust relationships to ensure they are still required and properly secured.
- **Security**: Implement Selective Authentication when possible to limit access and reduce potential security risks.
- **Trust Verification**: Periodically verify trust relationships using tools like `nltest` or the Active Directory Domains and Trusts console to ensure they are functioning correctly.

Understanding and properly configuring trust relationships is crucial for maintaining secure and efficient cross-domain or cross-forest operations in an Active Directory environment.
