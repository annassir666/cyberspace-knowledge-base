#thm  #active-directory #windows 

---

We need to deploy different policies for each OU individually. This way, we can push different configurations and security baselines to users depending on their department.


- Windows manages such policies through **Group Policy Objects (GPO)**. 
	- In simples terms, GPOs are simply a collection of settings that can be applied to OUs.
	- GPOs can contain policies aimed at either users or computers, allowing us to set a baseline on specific machines or identities.
	  
	- _To configure GPOs, you can use the **Group Policy Management** tool, available from the start menu_

- To configure Group Policies, you first create a GPO under **Group Policy Objects** and then link it to the OU where you want the policies to apply.
	![[Pasted image 20250805163327.png]]


- Let's examine the `Default Domain Policy` to see what's inside a GPO. The first tab you'll see when selecting a GPO shows its **scope**, which is where the GPO is linked in the AD. For the current policy, we can see that it has only been linked to the `thm.local` domain:
	 ![[Pasted image 20250805163836.png]]
	
	- As you can see, you can also apply **Security Filtering** to GPOs so that they are only applied to specific users/computers under an OU. By default, they will apply to the **Authenticated Users** group, which includes all users/PCs.

- The **Settings** tab includes the actual contents of the GPO and lets us know what specific configurations it applies. Each GPO has configurations that ==apply to computers only and configurations that apply to users only==. In this case, the `Default Domain Policy` only contains Computer Configurations:
	 ![[Pasted image 20250805164047.png]]

---

> If more information on any of the policies is needed, you can double-click them and read the **Explain** tab on each of them:
> ![[Pasted image 20250805164351.png]]


---

# GPO Distribution

- GPOs are distributed to the network via a network share called `SYSVOL`, which is stored in the DC. 
	- All users in a domain should typically have access to this share over the network to sync their GPOs periodically.
	- The SYSVOL share points by default to the "`C:\Windows\SYSVOL\sysvol\`" directory on each of the DCs in our network.
	  
- Once a change has been made to any GPOs, it might take up to 2 hours for computers to catch up. 
	- If you want to force any particular computer to sync its GPOs immediately, you can always run the following command on the desired computer:

```shell-session
PS C:\> gpupdate /force
```
