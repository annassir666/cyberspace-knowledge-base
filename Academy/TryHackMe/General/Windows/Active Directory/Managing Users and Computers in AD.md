
#thm #windows #active-directory 

---

# Managing Users
## Deleting extra OUs and users

- If we try to delete any of OUs, there might appear such problem:
  
	 ![[Pasted image 20250805133414.png]]


- By default, OUs are protected against accidental deletion. To delete the OU, we need to enable the **Advanced Features** in the View menu:
	 ![[Pasted image 20250805133443.png]]


- This will show you some additional containers and enable you to disable the accidental deletion protection. To do so, right-click the OU and go to Properties. You will find a checkbox in the Object tab to disable the protection:
	![[Pasted image 20250805133520.png]]


---

## Delegation

In Active Directory, we can give specific users some control over OUs. This process is knows as **Delegation**, and allows us to grant users specific privileges to perform advanced tasks on OUs **without Domain Administrator (DC)**.

One of the most common use cases for this is granting `IT support` the privileges to reset other low-privilege users' passwords.


To delegate control over an OU, you can right-click it and select **Delegate Control**:
![[Pasted image 20250805134053.png]]



> **Note:** To avoid mistyping the user's name, write "phillip" and click the **Check Names** button. Windows will autocomplete the user for you.


![[Pasted image 20250805134228.png]]



Click OK, and on the next step, select the following option to let him be able to reset passwords:

![[Pasted image 20250805134326.png]]


Suppose Sophie has forgotten her password. Now we can log in as Phillip. Even though Phillip was assigned to be able to change password, he only can do it using PowerShell.

```shell-session

PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

New Password: *********

VERBOSE: Performing the operation "Set-ADAccountPassword" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

Since we wouldn't want Sophie to keep on using a password we know, we can also force a password reset at the next logon with the following command:

```shell-session

PS C:\Users\phillip> Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose 

VERBOSE: Performing the operation "Set" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```


---



# Managing Computers

- By default, all the machines that join a domain (except for the DCs) will be put in the container called "Computers".
	 ![[Pasted image 20250805150536.png]]


- We can see some servers, some laptops and some PCs corresponding to the users in our network. Having all of our devices there is not the best idea since it's very likely that you want different policies for your servers and the machines that regular users use on a daily basis.
  
- In general, you'd expect to see devices divided into at least the three following categories:
	1. **Workstations**:
		- Each user in the domain will likely be logging into a workstation. This is the device they will use to do their daily jobs and general activities. These devices should never have a privileged user signed into them.
		
	2. **Servers**:
		- Servers are used to provide services to users or other servers.
		  
	3. **Domain Controllers**:
		- Domain Controllers allow us to control Active Directory Domain. 
		- Domain Controllers are deemed to be the most sensitive devices within the network because they contain hashed passwords for all users within the environment.