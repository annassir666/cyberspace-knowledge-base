#thm #active-directory #windows 

---

So far, we have discussed how to manage a single domain, the role of a Domain Controller and how it joins computers, servers and users.

![[Pasted image 20250805192837.png]]


As companies grow, so do their networks. Having a single domain for a company is good enough to start, but in time some additional needs might push you into having more than one.

---

# Trees

Suppose your company expands to a new country with different laws and regulations. You’ll need to update your Group Policy Objects (GPOs) to stay compliant. Now, you also have IT teams in both countries, and each team needs to manage their own resources without interfering with the other. While you could build a complex Active Directory (AD) structure with **delegations**, it can become difficult to manage and increase the risk of mistakes.


Fortunately, Active Directory lets you split your network into separate domains that can be managed independently. If two domains share the same namespace (like thm.local), they can be part of a Tree.

For example, if thm.local is divided into UK and US branches, you can create a Tree with a root domain (thm.local) and two subdomains: uk.thm.local and us.thm.local. Each subdomain would have its own AD, users, and computers.

![[Pasted image 20250805193246.png]]

- The IT people in the U.S. will have their own **DC** that manages the U.S. resources only.
	- For instance, a U.S. user wouldn't be able to manage UK users.
	- In this way, the Domain Administrators of each branch will have complete control over their respective DCs, but not the other's branch's DCs.
	- Policies can also be configured independently for each domain in the tree.

- **_Enterprise Admins_** group will grant a user administrative privileges over all of an enterprise's domains.
-  Each domain would still have its Domain Admins with administrator privileges over their single domains and the Enterprise Admins who can control everything in the enterprise.


---

# Forests

- The domain we manage can also be configured in different namespaces.

- Suppose your company continues growing and eventually acquires another company called `MHT Inc.`
  
	 - When both companies merge, you will probably have different domain trees for each company, each managed by its own IT department.
	   
	 - The union of several trees with different namespaces into the same network is known as a **forest**.

![[Pasted image 20250805194025.png]]


---


# Trust Relationships

- Organizing multiple domains into trees and forests helps keep your network well-structured and easier to manage. 
- However, sometimes users in one domain (like THM UK) need to access resources in another (like MHT ASIA). To allow this, domains in trees and forests are connected through **_trust relationships_**.
	- In simple terms, having a trust relationship between domains allows you to authorise a user from domain `THM UK` to access resources from domain `MHT EU`.

- The simplest trust relationship that can be established is a **one-way trust relationship**.
	- In a one-way trust, if `Domain AAA` trusts `Domain BBB`, this means that a user on BBB can be authorised to access resources on AAA:
	- ![[Pasted image 20250805194254.png]]


- **Two-way trust relationships** can also be made to allow both domains to mutually authorise users from the other. 
	- By default, joining several domains under a tree or a forest will form a two-way trust relationship.