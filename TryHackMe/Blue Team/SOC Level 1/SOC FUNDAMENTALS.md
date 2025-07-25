#thm #SOC #fundamentals 

---

- Security Operations Center's main responsibilities are **`DETECT`** and **`RESPOND`**.

- There are 3 main pillars of SOC teams:
	- People
	- Process
	- Technology


## People

- Hierarchy of a SOC Team
  ![[Pasted image 20250509222526.png]]

	- **SOC Analyst (Level 1):** Anything detected by the security solution would pass through these analysts first. These are the first responders to any detection. SOC Level 1 Analysts perform basic alert triage to determine if a specific detection is harmful. They also report these detections through proper channels.
	  
	- **SOC Analyst (Level 2)**: While Level 1 does the first-level analysis, some detections may require deeper investigation. Level 2 Analysts help them dive deeper into the investigations and correlate the data from multiple data sources to perform a proper analysis.
	  
	- **SOC Analyst (Level 3)**: Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities. The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts’ experience helps.
	  
	- **Security Engineer:** All analysts work on security solutions. These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.
	  
	- **Detection Engineer:** Security rules are the logic built behind security solutions to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.
	  
	- **SOC Manager:** The SOC Manager manages the processes the SOC team follows and provides support. The SOC Manager also remains in contact with the organization’s CISO (Chief Information Security Officer) to provide him with updates on the SOC team’s current security posture and efforts.



## Process

### Alert Triage

The alert triage is the basis of the SOC team. The triage is focused on analyzing the specific alert. This determines the severity of the alert and helps us prioritize it. The alert triage is all about ==answering the 5 Ws==. What are these 5 Ws?

![[Pasted image 20250509223236.png]]


## Technology

Technology minimizes manual effort proving solution for automating repeating job for **detection and response**

As a security team, individually detecting and responding to threats in each device or application ( there are tons of them in networks ) require significant effort and resources. Security solutions centralize of the information from devices or applications present in the network and automate the detection and response capabilities.

These solutions include:

- **`SIEM`** - Security Information and Event Management is a popular tool in SOC teams. It collects all the logs across the network. It checks the *Detection* rules that are configured in SIEM solution, which recognized suspicious activity. SIEM Provides us with detections and alerts us in case the matches are found.

- **`EDR`** - Endpoint Detection and Response provides the SOC team with detailed real-time and historical visibility of the devices’ activities. It operates on the endpoint level and can carry out automated responses. EDR has detection capabilities for endpoints, allowing you to investigate them in detail and respond with a few clicks.

- **`FIREWALL`** -  It monitors incoming and outgoing network traffic and filters any unauthorized traffic. The firewall also has some detection rules deployed, which help us identify and block suspicious traffic before it reaches the internal network.

- Several other security solutions play unique roles in a SOC environment, such as Antivirus, EPP, IDS/IPS, XDR, SOAR, and more.