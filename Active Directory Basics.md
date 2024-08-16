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
___________________________________________________
| Domain Admins	|  Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
----
| Server Operators	| Users in this group can administer Domain Controllers. They cannot change any administrative group memberships. |
----
| Backup Operators |	Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers. |
----
| Account Operators	| Users in this group can create or modify other accounts in the domain. |
----
| Domain Users	 | Includes all existing user accounts in the domain. |
----
| Domain Computers	| Includes all existing computers in the domain. |
-----
| Domain Controllers	| Includes all existing DCs on the domain. |
--------------------------------------------------------------------------
