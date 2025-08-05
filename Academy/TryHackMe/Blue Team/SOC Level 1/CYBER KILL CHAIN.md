#fundamentals #models #thm #framework #SOC 

---

![[Screenshot 2025-04-16 at 20.10.24.png]]

The framework "Cyber Kill Chain" defines the steps used by adversaries or malicious actors in cyberspace. To succeed, the adversary needs to go through all the phases from this framework.

We should know *Cyber Kill Chain* to understand and protect against ransomware attacks, security breaches as well as Advanced Persistent Threats (APTs)

---

# Reconnaissance

- Reconnaissance is the process of discovering and collecting information about victim. It is the planning phase for the adversaries.
	- One of the reconnaissance tools is `OSINT`
	- Active Reconnaissance
	- `Email Harvesting` - the process of obtaining email addresses from public, paid, or free services. It later may be used for phishing attacks.
	
- [theHarvester](https://github.com/laramies/theHarvester) - other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources 
  
- [Hunter.io](https://hunter.io/) - this is  an email hunting tool that will let you obtain contact information associated with the domain
  
- [OSINT Framework](https://osintframework.com/) - OSINT Framework provides the collection of OSINT tools based on various categories

---

# Weaponization

- On this stage, the adversary works on crafting a weapon.
  
- `Malware` - is a program that is designed to damage, disrupt, or gain unauthorized access to a computer;
- `Exploit` - a code that takes advantage of the vulnerability or flaw in the application system;
- `Payload` - a malicious code that the attacker runs on the system.

- **Exploit** is the _break-in method_.
    
- **Malware** is the _burglar_.
    
- **Payload** is the _stuff the burglar does once inside_.

---

# Delivery

- On this stage, the adversary looks for the ways to deliver the malware to the victim's system.
- It can be achieved through:
	- `Phishing Attack`
	- `Distributing Infected USB`
	- `Watering Hole Attack`
		- Watering hole attack is when a hacker infects a website that a specific group visits often. When people go to that site, their computers secretly download malware — sometimes through fake pop-ups or links.

---

# Exploitation

These are examples of how an attacker carries out exploitation:

- The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
- Using a zero-day exploit.
- Exploit software, hardware, or even human vulnerabilities. 
- An attacker triggers the exploit for server-based vulnerabilities.

---

# Installation

Immediately following the exploitation phase, the installation phase is **when the attacker attempts to install malware and other cyber-weapons onto the target's systems**. This stage involves setting up tools that allow the attacker to take control of the system and obtain valuable data.

---

# Command & Control

A Command and Control attack is **a type of attack that involves tools to communicate with and control an infected machine or network**. To profit for as long as possible from a malware attack, a hacker needs a covert channel or backdoor between their server and the compromised network or machine.