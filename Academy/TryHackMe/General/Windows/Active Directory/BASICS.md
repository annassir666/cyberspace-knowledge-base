#thm #windows #active-directory

---

## Windows Domains

**<u>Windows Domain</u>**  is a group of users and computers under the administration of a given business. The main idea behind a domain is to centralize the administration of common components of a Windows computer network in a single repository, which is called **<u>Active Directory</u>**

The server that runs _Active Directory_ services is called **<u>Domain Controller</u>** (DC).

![[Pasted image 20250608201019.png]]


Advantages of having a configured Windows Domain are:

- **Centralization**: every component, computer, or user can be configured from Active Directory with minimum effort.
- **Managing Security Policies**: security policies can be managed directly from Active Directory and later applied to all the users across the network as needed.

### In Summary:

| Term                  | What It Is                                            | Role                                              |
| --------------------- | ----------------------------------------------------- | ------------------------------------------------- |
| **Windows Domain**    | A network environment                                 | Groups users and computers for central management |
| **Domain Controller** | A server                                              | Runs AD and handles authentication and access     |
| **Active Directory**  | A directory service on the server (Domain Controller) | Stores user/computer info and policies            |

---

## Active Directory

The core of any Windows Domain is the **<u>Active Directory Domain Service</u> (AD DS)**. This service acts as a catalogue that holds the information of all the "objects" that exist on the network. Amongst the ==many objects supported by AD, we have users, groups, machines, printers, shares and many others.==


#### Users 

- Users are one of the objects known as **security principals**. 
	- It means that they can be authenticated by the domain and can be assigned privileges over **resources** like files or printers. 
	- You could say that a security principal is an object that can act upon resources in the network.

- Users can be used to represent two types of entities:
	- **People**: users will generally represent persons in your organization that need to access the network, like empoyees.
	  
	- **Services**:  you can also define users to be used by services like IIS or MSSQL.
		- Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service.


#### Machines

- For every computer that joins the Active Directory Domain, a **machine** object will be created.
  
- **Machines** are also considered "security principals" and are assigned an account just as any regular user. This account has somewhat limited rights within the domain itself.
  
- The **machine** accounts themeselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.

> **Note:** Machine Account passwords are automatically rotated out and are generally comprised of 120 random characters.

- Identifying machine accounts is relatively easy. They follow a specific naming scheme. The machine account name is the computer's name followed by a dollar sign. 
	- For example, a machine named `DC01` will have a machine account called `DC01$`.



#### Security Groups

- If you’ve used Windows, you might know that you can create user groups to manage access to files and resources more easily. 
	- Instead of giving each user permission one by one, you give access to the group, and anyone added to that group automatically gets the same rights. These security groups can also have their own permissions on the network. 
	  
	- Groups can have both users and machines as members. If needed, groups can include other groups as well.
	  
	  - You can obtain the complete list of default security groups from the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups)

- Several groups are created by default in a domain that can be used to grant specific privileges to users. As an example, here are some of the most important groups in a domain:

| **Security Group** | **Description**                                                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins      | Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
| Server Operators   | Users in this group can administer Domain Controllers. They cannot change any administrative group memberships.                                           |
| Backup Operators   | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.                    |
| Account Operators  | Users in this group can create or modify other accounts in the domain.                                                                                    |
| Domain Users       | Includes all existing user accounts in the domain.                                                                                                        |
| Domain Computers   | Includes all existing computers in the domain.                                                                                                            |
| Domain Controllers | Includes all existing DCs on the domain.                                                                                                                  |


### Active Directory Users and Computers

To configure users, groups or machines in Active Directory, we need to log in to the Domain Controller and run "Active Directory Users and Computers"

![[Pasted image 20250804222108.png]]

- This will open up a window where you can see the hierarchy of users, computers and groups that exist in the domain. These objects are organized in **Organizational Units (OUs)** which are container objects that allow you to classify users and machines.
	- OUs are mainly used to define sets of rules of users. The people in the Sales department are likely to have a different set of policies applied than the people in IT.
	  
	- ==Keep in mind that a user can only be a part of a single OU at a time.==

- If you open any OUs, you can see the users they contain and perform simple tasks like creating, deleting or modifying them as needed. You can also reset passwords if needed (pretty useful for the helpdesk):
	- ![[Pasted image 20250804235324.png]]


- There are other default containers apart from the THM OU. These containers are created by Windows automatically and contain the following:
  
	- **Builtin:** Contains default groups available to any Windows host.
	  
	- **Computers:** Any machine joining the network will be put here by default. You can move them if needed.
	  
	- **Domain Controllers:** Default OU that contains the DCs in your network.
	  
	- **Users:** Default users and groups that apply to a domain-wide context.
	  
	- **Managed Service Accounts:** Holds accounts used by services in your Windows domain.



#### Security Groups vs OUs


You are probably wondering why we have both groups and OUs. While both are used to classify users and computers, their purposes are entirely different:


- **Organizational Units (OUs):**

	- Think of OUs like folders in a filing cabinet.
	    
	- **Purpose:** Used to **organize** users and computers and apply **policies** (like desktop settings, software rules, etc.).
	    
	- **Example:** You put all Marketing users in one OU to give them specific settings.
	    
	- **Limit:** A user or computer can only be in **one OU** at a time.


 - **Security Groups:**

	- Think of Security Groups like access cards.
	    
	- **Purpose:** Used to **give access** to things (like files, folders, printers, etc.).
	    
	- **Example:** You create a group for "HR Share Access" and add all HR employees to it so they can access that shared folder.
	    
	- **Flexibility:** A user can be in **many groups** at once.