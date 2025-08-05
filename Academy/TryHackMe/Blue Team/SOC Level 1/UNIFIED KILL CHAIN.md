#thm #framework #fundamentals #SOC [[CYBER KILL CHAIN]]

---

`In the realm of cybersecurity, a “Kill Chain” is used to describe the methodology/path attackers such as hackers or APTs use to approach and intrude a target.`

---

Threat modeling is about identifying risk and it breaks down into:

- Identifying what systems and applications need to be secured and what function they serve in the environment.
- Assessing what vulnerabilities these applications have and how they can be exploited.
- Creating a plan of action to secure these applications from the vulnerabilities.
- Putting in policies to prevent these vulnerabilities from occuring where possible

The UKC can encourage threat modelling as the UKC framework helps identify potential attack surfaces and how these systems may be exploited.


---

The UKC states that there are 18 phases to an attack: Everything from reconnaissance to data exfiltration and understanding an attacker's motive.

![[Pasted image 20250416222409.png]]

| **Benefits of the Unified Kill Chain (UKC) Framework**                                                                                                                                                | **How do Other Frameworks Compare?**                                                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Modern (released in 2017, updated in 2022).                                                                                                                                                           | Some frameworks, such as MITRE’s were released in 2013, when the cybersecurity landscape was very different.                      |
| The UKC is extremely detailed (18 phases).                                                                                                                                                            | Other frameworks often have a small handful of phases.                                                                            |
| The UKC covers an entire attack - from reconnaissance, exploitation, post-exploitation and includes identifying an attacker's motivation.                                                             | Other frameworks cover a limited amount of phases.                                                                                |
| The UKC highlights a much more realistic attack scenario. Various stages will often re-occur. For example, after exploiting a machine, an attacker will begin reconnaissance to pivot another system. | Other frameworks do not account for the fact that an attacker will go back and forth between the various phases during an attack. |

---

# **IN (INITIAL FOOTHOLD)**

﻿The main focus of this series of phases is for an attacker to gain access to a system or networked environment.
﻿
An attacker will employ numerous tactics to investigate the system for potential vulnerabilities that can be exploited to gain a foothold in the system.

![[Pasted image 20250417085050.png]]


## Reconnaissance **([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))** [[CYBER KILL CHAIN#Reconnaissance]]

## Weaponization **([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))**  [[CYBER KILL CHAIN#Weaponization]]

## Social Engineering **([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))**

- Getting a user to open a malicious attachment;
- Impersonating a webpage and make user enter their credentials

## Exploitation ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/)) [[CYBER KILL CHAIN#Exploitation]]

This phase of the UKC describes how an attacker takes advantage of weaknesses or vulnerabilities present in a system.

- Uploading and executing a reverse shell to a web application.
- Interfering with an automated script on the system to execute code.
- Abusing a web application vulnerability to execute code on the system it is running on.

## Persistence ([MITRE Tactic TA0003](https://attack.mitre.org/tactics/TA0003/)) 

Specifically, this phase of the UKC describes the techniques an adversary uses to maintain access to a system they have gained an initial foothold on.

- Creating a service on the target system that will allow the attacker to regain access (backdoor).
- Adding the target system to a Command & Control server where commands can be executed remotely at any time.
- Leaving other forms of backdoors that execute when a certain action occurs on the system (i.e. a reverse shell will execute when a system administrator logs in).


## Defence Evasion ([MITRE Tactic TA0005](https://attack.mitre.org/tactics/TA0005/))

This phase specifically is used to understand the techniques an adversary uses to evade defensive measures put in place in the system or network.

- Web application firewalls.
- Network firewalls.
- Anti-virus systems on the target machine.
- Intrusion detection systems.


## Command & Control ([MITRE Tactic TA0011](https://attack.mitre.org/tactics/TA0011/)) [[CYBER KILL CHAIN#Command & Control]]

The "Command & Control" phase combines the efforts an adversary made during the "Weaponization" stage to establish communications between the adversary and target system.

An adversary can establish command and control of a target system to achieve its action on objectives. For example, the adversary can:

- Execute commands.
- Steal data, credentials and other information.
- Use the controlled server to pivot to other systems on the network.


## Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

"Pivoting" is the technique an adversary uses to reach other systems within a network that are not otherwise accessible (for example, they are not exposed to the internet). For example, an adversary can gain access to a web server that is publically accessible to attack other systems that are within the same network.

---

# THROUGH (NETWORK PROPAGATION)

![[Pasted image 20250417110014.png]]

An attacker would seek to gain additional access and privileges to systems and data to fulfil their goals. The attacker would set up a base on one of the systems to act as their pivot point and use it to gather information about the internal network.


## Pivoting 

Once the attacker has access to the system, they would use it as their staging site and a tunnel between their command operations and the victim’s network. The system would also be used as the distribution point for all malware and backdoors at later stages.


## Discovery ([MITRE Tactic TA0007](https://attack.mitre.org/tactics/TA0007/))

The attacker would gather information about the system and the network it’s connected to. This includes details like user accounts, permissions, software and applications, browser activity, files, folders, shared network resources, and system settings.


## **Privilege Escalation** ([MITRE Tactic TA0004](https://attack.mitre.org/tactics/TA0004/))

- _SYSTEM/ ROOT._
- _Local Administrator._
- _A user account with Admin-like access._
- _A user account with specific access or functions._


## **Execution** ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))

This is when the attacker installs their malicious code on the system they’ve taken over. They use things like remote trojans, command-and-control (C2) scripts, harmful links, and scheduled tasks to stay on the system and keep their access over time.


## **Credential Access** ([MITRE Tactic TA0006](https://attack.mitre.org/tactics/TA0006/))

Alongside the Privilege Escalation stage, the attacker tries to steal usernames and passwords using methods like keylogging and credential dumping. By using real login details, it becomes harder to spot their activity.


## **Lateral Movement** ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

With the credentials and elevated privileges, the adversary would seek to move through the network and jump onto other targeted systems to achieve their primary objective. The stealthier the technique used, the better.


---

# **Out (Action on Objectives)**

## Collection [MITRE Tactic (TA0009)](https://attack.mitre.org/tactics/TA0009/)

After gaining access, the attacker collects valuable data from drives, browsers, emails, and even audio or video sources. This compromises confidentiality and sets the stage for exfiltration, where the stolen data is encrypted and sent out through hidden channels.


### **Exfiltration** ([MITRE Tactic TA0010](https://attack.mitre.org/tactics/TA0010/)) 

To escalate the attack, the adversary steals data, encrypts and compresses it to avoid detection, and uses the previously established C2 channel or tunnel to exfiltrate it securely.


## Impact ([MITRE Tactic TA0040](https://attack.mitre.org/tactics/TA0040/))

If the attacker wants to damage the integrity or availability of data, they might change, block, or destroy it. This could include removing user access, wiping files, using ransomware to lock data, defacing websites, or launching DoS attacks—all meant to disrupt business and operations.


## Objectives

With full access to the systems and network, the attacker moves to achieve their main goal. If the motive is financial, they might use ransomware to lock files and demand payment. If the goal is to harm the business’s reputation, they could leak private or confidential information to the public.

