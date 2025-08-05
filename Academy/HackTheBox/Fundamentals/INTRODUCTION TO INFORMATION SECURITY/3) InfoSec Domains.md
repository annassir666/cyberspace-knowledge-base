#htb_academy #fundamentals

---

![[Pasted image 20250323233726.png]]

--- 
# **Network Security**

Several key elements work together to form a comprehensive protection strategy in network security. These are but not limited to:

| **Element**                                               | **Description**                                                                                                                                                                               |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Firewalls`                                               | Act as barriers between trusted internal networks and untrusted external networks, filtering traffic based on predetermined security rules.                                                   |
| `Intrusion Detection and Prevention Systems`(`IDS`/`IPS`) | Monitor network traffic for suspicious activities and take automated actions to detect or block potential threats.                                                                            |
| `Virtual Private Networks`(`VPNs`)                        | Provide secure, encrypted connections over public networks, ensuring data privacy and integrity during transmission. For example, used by employees to connect to internal network resources. |
| `Access control mechanisms`                               | Include authentication and authorization protocols to ensure only legitimate users can access network resources.                                                                              |
| `Encryption technologies`                                 | Protect sensitive data both in transit and at rest, rendering it unreadable to unauthorized parties.                                                                                          |
### **Who Handles Network Security?**

Network security is managed by the **IT department**, specifically the **network security team**, led by a **Network Security Manager** who reports to the **CISO** or equivalent executive. Their key tasks include:

- Configuring and managing security devices
    
- Enforcing security policies
    
- Monitoring network traffic for threats
    
- Responding to security incidents

### **Testing Network Security**

Security professionals like **penetration testers** or **ethical hackers** assess network security by simulating real-world attacks to identify vulnerabilities.

- **Larger companies** → Have dedicated internal teams
    
- **Smaller companies** → Hire external security consultants

### **Key Stakeholders in Network Security**

- **CISO (Chief Information Security Officer)** → Sets strategy & aligns security with business goals
    
- **CIO / IT Director** → Allocates resources & integrates security into IT infrastructure
    
- **Network Administrators & Security Analysts** → Handle daily security operations
    
- **Compliance Officers** → Ensure regulatory compliance
    
- **Risk Management Teams** → Prioritize security investments

### **Why It Matters**

Network security is a **continuous process** that protects an organization’s digital assets from cyber threats. It requires **constant vigilance, expertise, and collaboration** to stay ahead of evolving risks.


               ┌──────────────────────────────────────────────┐
               │     Executive-Level Roles                    │
               ├──────────────────────────────────────────────┤
               │ Chief Information Security Officer (CISO)    │
               │ Chief Security Officer (CSO)                 │
               │ Chief Information Officer (CIO) (Broader IT) │
               └──────────────────────────────────────────────┘
                            ▲
                            │
               ┌────────────────────────────────┐
               │    Senior-Level Roles          │
               ├────────────────────────────────┤
               │ Security Architect             │
               │ Threat Intelligence Analyst    │
               │ Red Team/Blue Team Lead        │
               └────────────────────────────────┘
                            ▲
                            │
               ┌─────────────────────────────────────┐
               │   Mid-Level Roles                   │
               ├─────────────────────────────────────┤
               │ Penetration Tester (Ethical Hacker) │
               │ Incident Response Specialist        │
               │ Forensic Analyst                    │
               │ Security Engineer                   │
               └─────────────────────────────────────┘
                            ▲
                            │
               ┌────────────────────────────────┐
               │    Entry-Level Roles           │
               ├────────────────────────────────┤
               │ Security Analyst               │
               │ SOC Analyst                    │
               │ IT Support with Security Focus │
               └────────────────────────────────┘

---

# **Application Security**

**Goal:**  
Protect the confidentiality, integrity, and availability (CIA Triad) of data and systems.

## Key Concepts

- **Built-In Security:**  
  Security should be part of the design, development, and maintenance process.

- **Secure Code:**  
  Write code that avoids vulnerabilities (e.g., SQL injection, XSS).

- **Testing:**  
  Regularly test your application—through penetration tests, code reviews, and vulnerability scanning.

- **Ongoing Monitoring:**  
  Continuously monitor for new threats and update security measures.

## House Analogy

Imagine building a secure house:
- **Locks on Doors:** Secure authentication (only the right people can enter).
- **Strong Walls:** Solid code that resists attacks.
- **Waterproof Roof:** Data encryption to protect information.
- **Inspections & Maintenance:** Regular tests and updates to fix vulnerabilities.


In software development, Security by Design works the same way. When creating an app, developers think about security right from the planning stage. This can include:

- `Threat modeling`: Like imagining all the ways someone might break into your house, threat modeling helps developers figure out potential risks to the app early on.
    
- `Secure code reviews`: After writing the code, developers carefully check it to make sure there are no weak spots, similar to inspecting the house’s foundation for cracks before finishing construction.
    
- `Servers and databases`: These are like the land your house sits on and the water supply it uses. If they aren’t secure, the whole system is at risk.
    
- `Authentication and authorization`: Think of these as high-quality locks on your doors. Authentication ensures only the right people can get in, while authorization makes sure they can only access the rooms (data) they’re allowed to.


--- 

# **Operational Security**

Operational Security's (*OpSec*) primary goal is to maintain a secure environment for an organization's day-to-day operations, ensuring that sensitive information remains confidential, intact, and available only to authorized individuals.

## Process of OpSec

### 🔍 **1. Identify Critical Assets**

What’s most valuable? Your heirloom, console, or jewelry? Similarly, organizations identify sensitive data that needs protection.

### ⚠️ **2. Identify Threats**

What could go wrong? A guest could knock over your console, wander into your room, or misplace your valuables. In OpSec, this means assessing potential risks.

### 🛑 **3. Find Vulnerabilities**

How can you prevent problems? You might lock valuables away, restrict access, or keep an eye on guests. In OpSec, this is about fixing weaknesses—like using passwords or security badges.

### 🔑 **4. Control Access**

Who gets in? Maybe only your best friend gets the key to your room. Companies do the same—limiting access to sensitive information to trusted individuals.

### 👀 **5. Monitor & Adapt**

During the party, you stay alert. If guests enter restricted areas, you step in. OpSec is a continuous process, adapting to new threats to keep everything secure.

💡 **Bottom Line:** Just like you'd safeguard your valuables at a party, OpSec helps organizations protect their critical information.


## OpSec: A Continuous Security Process

At its core, **Operational Security (OpSec)** is about:

- Identifying critical information
- Analyzing threats
- Assessing vulnerabilities
- Implementing protective measures

This is an ongoing, adaptive process that protects both **physical** (facilities, access) and **digital** (passwords, permissions) assets.

## **1. Access Control**

**Who gets access to what, and when?**

- Uses authentication (e.g., multi-factor authentication) to verify identities
    
- Implements authorization systems to restrict access based on roles
    
- Conducts regular access audits to remove unnecessary permissions (e.g., when an employee changes roles or leaves)

## **2. Asset Management**

**Know what you have and where it is.**

- Maintains an inventory of hardware, software, and data
    
- Identifies high-priority assets to apply stronger security
    
- Helps spot and fix vulnerabilities efficiently

## **3. Change Management**

**Secure changes, prevent new risks.**

- Ensures controlled system updates with testing and approval
    
- Reduces risk of introducing new security flaws during modifications

## **4. Security Awareness Training**

**Employees are the first line of defense.**

- Trains staff on phishing attacks, strong passwords, and data handling
    
- Promotes a security-first mindset across the organization


## InfoSec VS OpSec

| **Aspect**       | **InfoSec (Information Security)**    | **OpSec (Operational Security)**                         |
| ---------------- | ------------------------------------- | -------------------------------------------------------- |
| **Primary Goal** | Protect digital and physical data     | Prevent adversaries from exploiting critical information |
| **Focus**        | Cybersecurity, IT security            | Risk assessment, adversary intelligence                  |
| **Methods**      | Encryption, firewalls, authentication | Threat analysis, restricted access, monitoring           |
| **Used By**      | IT departments, cybersecurity teams   | Military, intelligence, businesses                       |
| **Example**      | Securing passwords and network access | Preventing employees from oversharing sensitive info     |

- **InfoSec stops hackers from stealing your data.**
    
- **OpSec stops people from finding and using your secrets against you.**

## OpSec Responsibility

The responsibility for OpSec typically falls on the Information Security team, led by the Chief Information Security Officer (`CISO`), who works closely with other departments such as IT, HR, and Legal to ensure that security measures are aligned with business needs and regulatory requirements, or an equivalent role. However, it's important to note that OpSec is not solely the domain of the security team. It requires cooperation and commitment from all levels of the organization, from front-line employees to top-level executives.