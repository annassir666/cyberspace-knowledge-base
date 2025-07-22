#fundamentals #htb_academy

---

![[Pasted image 20250323233726.png]]

- `Client`: This is a PC/Laptop through which you access resources and services "on the Internet".
    
- `Internet`: This is a vast, interconnected network of servers that offer different services and applications, such as Hack The Box.
    
- `Servers`: Servers provide various services and applications designed to perform specific tasks. For example, one type of server might be a "web server", allowing you and others to view the content of a website (such as this section you're reading currently) on your computer or smartphone.
    
- `Network`: When multiple servers or computers are connected and can communicate with each other, it's called a network.
    
- `Cloud`: Cloud refers to data centers that offer interconnected servers for companies and individuals to use.
    
- `Blue Team`: This team is responsible for the internal security of the company and defends against cyber attacks.
    
- `Red Team`: This team simulates an actual adversary/attack on the company.
    
- `Purple Team`: This team consists of both Blue Team and Red Team members working together to enhance the company's security.

---
## Areas of Information Security

InfoSec plays an integral role in safeguarding an organization's data from various threats, ensuring the ==`confidentiality`==, ==`integrity`==, and ==`availability`== of data.


Range of assets that fall under umbrella of InfoSec:

1. `Network Security`
2. `Application Security`
3. `Operational Security`
4. `Disaster Recovery and Business Continuity`
5. `Cloud Security`
6. `Physical Security`
7. `Mobile Security`
8. `Internet of Things (IoT) Security`

A **vulnerability** is a weakness (e.g., software bugs, misconfigurations, weak passwords) that a **threat** can exploit. **Risk** is the potential damage if the threat succeeds.


## **Vulnerability | Threat | Risk**
#### House Security Example

- **Threat** 🏴‍☠️ → A **burglar** wants to break into your house.
- **Vulnerability** 🔓 → You **forgot to lock your door**.
- **Risk** 💥 → Because the door is unlocked, the burglar **can enter and steal your stuff**.

#### Cybersecurity Version

- **Threat** → A hacker wants to steal your data.
- **Vulnerability** → You have a weak password.
- **Risk** → The hacker can guess your password and hack your account.


## **Roles in Information Security**

| **Role**                                                                    | **Description**                                         | **Relevance to Penetration Testing**                                                                                                              |
| --------------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span style="color:green;">Chief Information Security Officer (CISO)</span> | Oversees the entire information security program        | Sets overall security strategy that pen testers will evaluate                                                                                     |
| <span style="color:green;">Security Architect</span>                        | Designs secure systems and networks                     | Creates the systems that pen testers will attempt to breach                                                                                       |
| <span style="color:green;">Penetration Tester</span>                        | Identifies vulnerabilities through simulated attacks    | Actively looks for and exploits vulnerabilities within a system, legally and ethically. This is likely your target role.                          |
| <span style="color:green;">Incident Response Specialist</span>              | Manages and responds to security incidents              | Often works in tandem with pen testers by responding to their attacks, and sharing/collaborating with them afterwards to discuss lessons learned. |
| <span style="color:green;">Security Analyst</span>                          | Monitors systems for threats and analyzes security data | May use pen test results to improve monitoring                                                                                                    |
| <span style="color:green;">Compliance Specialist</span>                     | Ensures adherence to security standards and regulations | Pen test reports often support compliance efforts                                                                                                 |

