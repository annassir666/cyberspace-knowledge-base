#pentest

The steps of penetration testing:

1. **Pre-engagement** → The first step is to create all the necessary documents in the pre-engagement phase, discuss the assessment objectives, and clarify any questions.
2. **Information Gathering** → once pre-engagement step is done, we start exploring website of the company, discover any technology used, understand how the web app works and etc
3. **Vulnerability Assessment** → with this information, we can look for known vulnerabilities and investigate questionable features that may allow for unintended actions.
4. **Exploitation** → Once we have found potential vulnerabilities, we prepare our exploit code, tools, and environment and start exploiting the web-server
5. **Post-Exploitation** → once we’re in, we try to move around the environment and try to get higher privileges like admin
6. **Lateral Movement** → If other servers and hosts in the internal network are in scope, we then try to move through the network and access other hosts and servers
7. Proof-of-concept → We create a proof-of-concept that proves that these vulnerabilities exist and potentially even automate the individual steps that trigger these vulnerabilities.
8. Post-engagement → Finally, the documentation is completed and presented to our client as a formal report deliverable. Afterward, we may hold a report walkthrough meeting to clarify anything about our testing or results and provide any needed support to personnel tasked with remediating our findings.