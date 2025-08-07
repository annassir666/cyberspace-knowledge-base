#thm #active-directory #enumeration

---

# Breaching Active Directory

- Before we can exploit AD misconfigurations for privilege escalation, lateral movement, and goal execution, ==we need to acquire an initial set of valid AD credentials==.

- When looking for that first set of credentials, we don't focus on the permissions associated with the account; thus, even a low-privileged account would be sufficient.
	- We are  looking for a way to authenticate to AD, allowing us to do further enumeration on AD itself.

- DNS will be a part of Active Directory testing whether you like it or not. 
	- This is because one of the two major AD authentication protocols, Kerberos, relies on DNS to create tickets. 
	- Tickets cannot be associated with IPs, so DNS is a must.

---

# NTLM Authenticated Services

## NTLM and NetNTLM

**NTLM (New Technology LAN Manager)** is a set of security protocols used in Active Directory (AD) to verify user identities. It works using a **challenge-response method** called **NetNTLM**, commonly used by network services.

However, if these services are exposed to the internet, they can become vulnerable. Common examples include:

- Internal mail servers with public Outlook Web App (OWA) login pages
    
- Remote Desktop Protocol (RDP) services exposed online
    
- VPN endpoints connected to AD
    
- Public-facing web apps using NetNTLM for login

These exposures can be exploited if not properly secured.


**NetNTLM**, also known as **Windows Authentication** or **NTLM Authentication**, allows an application to act as a **middleman** between the user and Active Directory (AD).

Instead of the app checking the user's credentials directly, it **forwards a challenge** to the Domain Controller. If the user passes the challenge, they’re authenticated.

This way, the app **doesn’t store or handle passwords**—only the Domain Controller does. 
The app simply passes along the authentication data and logs the user in if AD approves.


![[Pasted image 20250806104242.png]]

---

## Brute-Force Login Attacks

- If we recovered information such as valid email addresses during our initial red team recon, we could perhaps try to use these for brute force attacks.

- Since most AD environments have account lockout configured, we won't be able to run a full brute-force attack. Instead, we need to perform a password spraying attack.
	
	- Instead of trying different passwords, which may trigger the account lockout mechanism, we choose and use one password and attempt to authenticate with all the usernames we have acquired.
	  
	- However, it should be noted that these types of attacks can be detected due to the amount of failed authentication attempts they will generate.
	  


---

# LDAP Bind Credentials


## LDAP

- **_LDAP (Lightweight Directory Access Protocol)_** is another method of AD authentication.
  
- LDAP authentication is similar to NTLM authentication. However, unlike with NTLM, with LDAP, applications directly verify user's credentials.
	- The application has a pair of AD credentials that it can use first to query LDAP and then verify the AD user's credentials.

- LDAP authentication is a popular mechanism with third-party (non-Microsoft) applications that integrate with AD:
	- Gitlab
	- Jenkins
	- Custom-developed web applications
	- Printers
	- VPNs

-  If any of these applications or services are exposed on the internet, the same type of attacks as those leveraged against NTLM authenticated systems can be used.

- Since services using LDAP authentication need Active Directory (AD) credentials, they can become targets for attacks. An attacker might try to steal these credentials to gain access to AD. The LDAP authentication process is shown below:

![[Pasted image 20250807035831.png]]

> If you can access the right server, like a GitLab server, you might be able to find Active Directory (AD) credentials just by reading configuration files. These files often store credentials in plain text, relying on the file's security—not encryption—to keep them safe.

---

## LDAP Pass-back Attacks

- **LDAP Pass-back attack** is a common attack against network devices, such as printers, when you have gained initial access to the internal network, such as plugging in a rogue device in a boardroom.

- **LDAP Pass-back attacks** happen when an attacker gains access to a device’s settings that include LDAP configuration—like the web interface of a network printer. 
	- These interfaces often still use default login credentials (e.g., admin:admin). Even if the LDAP password is hidden, the attacker can change the LDAP server’s IP address to their own. 
	  
	- Then, when the device tries to test the LDAP connection, it sends the credentials to the attacker’s fake server. The attacker can then capture these credentials.


---


# Authentication Relays


## Server Message Block ( SMB )

- The Server Message Block (SMB) protocol allows clients (like workstations) to communicate with a server (like a file share).
	- In networks using Microsoft Active Directory, SMB handles tasks like file sharing and remote management. Even simple alerts—like your computer saying a printer is out of paper—are sent using SMB.


- Older versions of the **SMB protocol** (used for sharing files and printers in Windows networks) had **security problems**. Hackers found ways to:

	- **Steal usernames and passwords**, 
	- **Run their own programs on other people's computers** using these weaknesses.

- Even though newer versions of SMB fixed many of these issues, **some organizations still use the old versions** because they have old systems (called **legacy systems**) that don’t work with the updated versions.

- We’ll talk about **two ways hackers can attack NetNTLM authentication** using SMB:
	1. **Offline Cracking**
		- Hackers can **intercept the login challenge** (the NTLM challenge) and try to **guess the password later**, without being connected to the network.
		    
		- This guessing process is **slower** than directly cracking normal NTLM password hashes, but it can still work.
	  
	2. **Relay Attack (Man-in-the-Middle)**
		- A hacker can set up a **fake device** on the network. When a user tries to connect, the fake device **pretends to be the real server** and captures the login attempt.
		    
		- Then, the hacker **forwards this login to the real server** and gains access – basically **logging in as the user without knowing the password**.

---
## LLMNR, NBT-NS, and WPAD

We're going to look at how authentication works with SMB and use a tool called **Responder** to try to intercept and capture **NetNTLM hashes**, which we can then try to crack.

On busy networks, there are often many of these authentication attempts flying around. Sometimes, because of outdated DNS records or network scans, these attempts might get misdirected to our rogue device.

**Responder** lets us perform **Man-in-the-Middle (MitM)** attacks by tricking devices into thinking our machine is the server they're looking for. It does this by responding to certain local network name requests like:

- **LLMNR** (Link-Local Multicast Name Resolution)
    
- **NBT-NS** (NetBIOS Name Service)
    
- **WPAD** (Web Proxy Auto-Discovery Protocol)

These are used by Windows machines to find other devices on the local network when DNS doesn't give an answer.

Instead of ignoring these broadcast requests like normal devices, **Responder listens for them and replies with fake (poisoned) responses**, claiming to be the server the client is looking for. When the client tries to connect, it actually connects to our machine.

Responder then uses fake services like SMB, HTTP, and SQL to capture the client’s authentication data — specifically the **NetNTLM hash**, which we can later try to crack.


---

# Microsoft Deployment Toolkit

Large organizations need tools to manage their IT systems. It's not practical for IT staff to install software manually on every computer using DVDs or USB drives. Fortunately, Microsoft provides tools to handle this. However, if these tools are misconfigured, attackers can use them to break into Active Directory (AD).


## MDT and SCCM

**_Microsoft Deployment Toolkit (MDT)_** is a Microsoft service that assists with automating the deployment of Microsoft Operating Systems (OS).

- Usually, MDT is integrated with Microsoft's System Center Configuration Manager (SCCM)
  
- **_System Center Configuration Manager (SCCM)_** manages all updates for all Microsoft applications, services, and operating systems.
  
- **MDT** is used for new deployments. Essentially it allows the IT team to preconfigure and manage boot images.
	- Hence, if they need to configure a new machine, they just need to plug in a network cable, and everything happens automatically.

---

## PXE Boot

- Large organizations use **_Preboot Execution Environment (PXE)_** boot to allow new devices that are connected to the network to load and install the OS directly over a network connection.

- **MDT** can be used to create, manage, and host **PXE** boot images.
	- **PXE** boot is usually integrated with DHCP, which means that if DHCP assigns an IP lease, the host is allowed to request the **PXE** boot image and start the network OS installation process.

![[Pasted image 20250807193910.png]]



- Once the process is performed, the client will use a TFTP connection to download the PXE boot image. We can exploit the PXE boot image for two different purposes:
	
	- Inject a privilege escalation vector, such as a Local Administrator account, to gain Administrative access to the OS once the PXE boot has been completed.
	  
	- Perform password scraping attacks to recover AD credentials used during the install.


---

# Configuration Files

## Exploring Configuration Files for Credential Recovery

Once you've gained access to a host in a network, a good next step is to search for credentials stored in **configuration files**. These can include:

- Web application config files
- Service configuration files
- Registry keys
- Centrally deployed applications

You can use tools like **Seatbelt** to automate this process.
