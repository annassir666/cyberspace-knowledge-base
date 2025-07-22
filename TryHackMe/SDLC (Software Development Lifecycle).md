#thm #methodology

---

# **What is Software Development Lifecycle (SDLC)?**

Software Development Life Cycle (SDLC) is a software engineering concept which is the structured process of developing an application.

SDLC defines the tasks to perform at each software development stage. 

This methodology is used to improve the quality of software development, and meet deadlines and cost estimates.

SDLC provides guidance required to create a software application by splitting these tasks into phases that form the Software Development Lifecycle. Standardizing the tasks within each phase increases the efficiency of the development process. Each phase divides into granular tasks that can be measured and tracked. This increases the capability of monitoring to ensure projects stay on track.


>[!AIM]
>The aim of SDLC is to establish repeatable processes and predictable outcomes from which future projects can benefit.


## Phases

![[Pasted image 20250326012752.png]]

- **Planning**: encompasses all aspects of project and product management. This includes resource allocation, project scheduling, cost estimation etc.
  
- **Requirements** **Definition**: is considered part of planning to determine what the application is supposed to do and its requirements. For example, a social media application would require the ability to connect with a friend.  
  
- **Design** **& Prototyping**: establishing how the software application will work, programming language, methods to communicate with each other, architecture, and etc.
  
- **Software Development:** building the program, writing code and documentation.
  
- **Testing:** In this phase, we ensure components work and can interact with each other. For example, each function works correctly, different parts of the application work seamlessly together, and performance-wise, there are no lags in processing, and etc. 
  
- **Deployment:** in this stage, the application or project is made available to users.
  
- **Operations & Maintenance:** this is where engineers respond to issues in the application or bugs and flaws reported by users and sometimes plan additional features in future releases.


==Companies can choose to rearrange by splitting or unifying these into 6-8 phases. SDLC models include Waterfall, Agile, and DevOps, amongst others.==



---

# **SDLC PHASE 1**

## 1️⃣ Planning (Feasibility Stage)

🔹 **Purpose & Scope** → Define the application's goals and boundaries.  
🔹 **Identify Problems & Needs** → Ensure the project remains focused.  
🔹 **Resource Allocation** → List the necessary tools, team members, and timeline.  
🔹 **Feasibility Check** → Spot potential issues early.

## 2️⃣ Requirements Definition

🔹 **Gather all necessary details** → What must the system do?  
🔹 **Define User Needs** → Research and analyze target users.  
🔹 **Evaluate Prototypes & Alternatives** → Compare different solutions.  
🔹 **List Technical Requirements** → Hardware, software, integrations, etc.

📌 _Example:_
- A social media app must enable users to connect with friends.
- An inventory system requires a search feature.

📜 **Key Document:** Software Requirement Specification (SRS).

## 3️⃣ Design & Prototyping

🔹 **System Structure** → Define components like:

- **User Interface (UI)** → How users interact with the software.
- **System Interfaces** → Connections with other apps or services.
- **Network & Database Requirements** → Storage and communication setup.  
    🔹 **Create a Logical Blueprint** → Convert SRS into a structured design.  
    🔹 **Define Security Measures** → Encryption, authentication, and secure data handling.

📜 **Key Document:** Architecture Design Review (ADR) created by engineers and developers at this stage to ensure that all teams working in different areas are on the same page.  
	🔹 Ensures alignment between developers, designers, and security teams.

## 4️⃣ Software Development

🔹 **Write the Code** → Based on the design specifications.  
🔹 **Use Development Tools** → Compilers, debuggers, version control.  
🔹 **Follow Best Practices** → Code hygiene, security protocols, and documentation.  
🔹 **Create Playbooks & Guides** → Help developers maintain consistency.

⚡ _Why It Matters?_  
Clean, well-documented code ensures maintainability and security.


---

# **SDLC PHASE 2**

## ✅ **5. Testing**

### 🔹 **Key Testing Phases:**

#### 📌 Test Case Design & Development

- Testers create **structured, repeatable test cases** to validate core functionalities.
  
- Test cases should be:
    - **Simple** and easy to understand.
    - **Unique** to avoid redundancy.
    - **Identifiable & Repeatable** for future updates.

- Automated test scripts may also be created and reviewed.    

#### 🏗 **Test Environment Setup**
- A controlled environment is created to mimic real-world conditions.

- It includes:
    - **Hardware & Software Configurations**
    - **Test Data & Network Conditions**
    - **Bug Reporting Tools**

#### 🚀 **Test Execution**

- All test cases are executed, including:
    - **Functional & Non-functional Tests**
    - **Regression Testing** (to ensure new changes don’t break existing features).
    
- **Test Automation** helps improve speed and test coverage.
- **Developer Velocity** is tracked to measure efficiency.

## 🚀 **6. Deployment**

### 🔹 **Key Aspects of Deployment:**

- **Automated Deployment Tools** → Ensure smooth rollouts.
    - _Examples:_ Netlify, Argo CD

- **Feature Releases** → Updates for web apps, mobile apps, or cloud systems.
- **Rollback Capability** → Allows reverting to a previous version if issues arise.

📌 _Why Automate?_ It minimizes manual errors, speeds up deployment, and improves reliability.


## 🔄 **7. Operations & Maintenance**

### 🔹 **Key Responsibilities:**

#### 🛠 **Bug Fixes & Updates**

- Fix **residual bugs** missed during testing.
- Implement **new features or improvements** based on user feedback.

#### 🤝 **Collaboration Between Dev & Ops**

- **Self-Service for Developers** → DevOps enables teams to find solutions independently.
- **Standardized Tools & Processes** → Reduces friction between development & operations.
- **Extensible Automation** → Automate routine tasks for efficiency (e.g., Terraform for cloud infrastructure).

📌 _Example:_ Automating virtual machine creation with Terraform allows tracking & security alerts for compliance.


---

# **CALMS Framework in DevOps**

## Introduction

CALMS is a framework for assessing an organization's DevOps adoption. 

- **Culture**
- **Automation**
- **Lean**
- **Measurement**
- **Sharing**

Each element is crucial for a successful DevOps implementation.

## 1. Culture

**Culture** in DevOps means **how people work together** in a company. It’s about teamwork, communication, and shared responsibility.

In traditional software development, teams work separately:

- Developers write code
- QA testers check for bugs
- Operations teams manage the servers


A strong DevOps culture means:

- **Breaking work into smaller tasks** instead of big, slow releases
- **Encouraging feedback** and continuous improvement
- **Working as one team**, not separate groups

## 2. Automation

Automation ensures **reliability and efficiency** by streamlining tasks like:

- **Continuous Integration (CI)** – Automating code integration
- **Continuous Delivery (CD)** – Automating deployments
- **Configuration as Code** – Defining application settings in code

Automating these processes reduces errors and speeds up development.

## 3. Lean

**Lean** in DevOps means **doing more with less** and **working efficiently**. Instead of spending years building a "perfect" product:

- Allows for **early user feedback**
- Encourages **continuous improvement**
- Speeds up time-to-market

## 4. Measurement

Tracking key metrics helps teams improve. Important metrics include:

- **Deployment Frequency** – How often updates are released
- **Lead Time for Changes** – Time from commit to production
- **Mean Time to Recovery (MTTR)** – Time to fix failures

Measuring performance ensures teams can make **data-driven improvements**.

## 5. Sharing

DevOps fosters **collaboration and shared responsibility** across teams. Transparency in documentation, metrics, and processes helps:

- Break down silos
- Improve communication
- Ensure accountability for the final product


---

# DevOps Metrics in Simple Terms

## Key DevOps Metrics

### 1. **Mean Time to Production (MTTP)**

**How long does it take for new code to go live?**

- Measures the time from writing code to deploying it.
- Faster MTTP means quicker feature releases.
- Improved by **automated testing** and **small code updates**.

### 2. **Deployment Frequency**

**How often is new code released?**

- Measures how frequently updates are pushed to production.
- High deployment frequency means **faster innovation**.
- Enabled by **automated pipelines** and **on-demand deployments**.    

### 3. **Speed of Deployment**

**How quickly can a release be deployed?**

- Tracks how fast a new version reaches production.
- Faster deployment reduces delays and keeps systems up-to-date.

### 4. **Deployment Agility**

**How fast and how often can updates be deployed?**

- A combination of deployment **speed** and **frequency**.
- Higher agility means a team can react quickly to changes.

### 5. **Failure Rate**

**How often do code changes cause problems?**

- Tracks how many updates **fail and need fixes**.
- Lower failure rates mean **better code quality**.
- Reduced by **small releases, automated testing, and fast feedback loops**.

### 6. **Mean Time to Recovery (MTTR)**

**How long does it take to fix a failure?**

- Measures the time needed to **recover from errors**.
- Faster MTTR means **better system stability**.
- Improved by **real-time monitoring** and **automated rollbacks**.

## Understanding Risk

Different teams define **risk** differently:

- **DevOps teams** → Risk is a high **failure rate** or slow **recovery time**.
- **Security teams** → Risk is **vulnerabilities** being exploited.

## Conclusion

Tracking these metrics helps teams **deliver updates faster, reduce failures, and improve security**. Measuring progress over time also builds trust and ensures **continuous improvement**.