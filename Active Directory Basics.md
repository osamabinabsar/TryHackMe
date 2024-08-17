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
   -
3. Domain Controllers
    - These devices are often deemed the most sensitive devices within the network as they contain hashed passwords for all user accounts within the environment.
  

###  Task 6 Group Policies
Group Policy Objects (GPO). GPOs are simply a collection of settings that can be applied to OUs. GPOs can contain policies aimed at either users or computers, allowing you to set a baseline on specific machines and identities.

To configure Group Policies, you first create a GPO under Group Policy Objects and then link it to the OU where you want the policies to apply. 

The Settings tab includes the actual contents of the GPO and lets us know what specific configurations it applies. As stated before, each GPO has configurations that apply to computers only and configurations that apply to users only. I

Editing GPO
![b71d8de9e74d129d0ad4142863deadc4](https://github.com/user-attachments/assets/d8e12106-0f9c-4cfa-b4eb-56b7516ae1e3)
![bd3665c2569aa8fbe4f7482a5750f018](https://github.com/user-attachments/assets/6d3c08ec-0adf-40b7-954c-e310da7cd27d)








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

