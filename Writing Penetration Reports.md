
#thm #pentest #reporting 

---

# **Anatomy of a Pentest Report**

## Audience

Every good report presents findings in the way that makes sense to both business and technical specialists. The report aims to different audiences: 

- **Technical Stakeholders** - the report aims to help technical specialist in understanding the root cause of discovered vulnerabilities and what steps to take to remediate them. `70-90%` of the report aims to this audience

- **Security Stakeholders** - although Security specialists won't be directly responsible for remediating vulnerabilities, they will work very closely to developers and technical specialists, which will remediate and fix the problems. Security specialists, reading the report, will structure the process and prioritize remediation efforts. `10-20%` of report for this audience

- **Business Stakeholders** - a piece of the audience doesn't have a technical background and not always understand some moments, so you should simply explain the problems. These guys should know what they pay for when securing their business. `5-10%` of the report is aimed to this audience.


## Sections of the Report

| Section                 | Target Audience                  | Description                                                                                                                                                                                                                                       |
| ----------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Summary                 | Business & Security Stakeholders | It is a high-level view of the assessment.  It explains what was tested, what was found, and why it matters - all in business terms. Sometimes you will be more focused on Business Stakeholders, so you will write everything in business terms. |
| Vulnerability Write-Ups | Technical Stakeholders           | Each issue found during the test gets its own write-up, which will include details in vulnerability, how it can be replicated, and the actions of remediation.                                                                                    |
| Appendices              | Security Stakeholders            | Appendices contain supporting details not included in the main report, like testing scope, methodology, or leftover artefacts. Security stakeholders use them to understand coverage and plan post-remediation steps.                             |


---

# Report Section: Summary

Summary section typically appears at the start of the report and should allow the reader, even without technical background, answer the following questions:

- What did we test?
- What did we find?
- What does it mean for our business or system?
- What should we do next?


## Summary of a Summary

- **Executive Summary** - Written for business stakeholders, this version avoids technical jargon and focuses on business risks. It helps business stakeholders understand the impact of the findings and the actions that should be taken immediately.

- **Finding && Recommendations** - This section, aimed at the security team, highlights common vulnerability themes and attack chains. While vulnerabilities are rated individually, combining lower-risk issues can still pose a high business impact. Here, you can emphasize these connections to help reprioritize remediation and address systemic problems, guiding developers to prevent future errors.


## Summary Structure

- **Overview** - What was tested? What type of system or application is it? What were the goals of the assessment? What was the scope, and how much coverage could be achieved?
  
- **Results** - What did the assessment uncover? Was the system secure? If not, what categories of issues were found?
  
- **Impact** - What is the real-world impact if the issues remain unaddressed? How could the system be exploited by a real-life threat actor?
  
- **Remediation Direction** - At a high level, what actions should the organization take next? Does this require major investment, or are the issues mostly quick fixes?


---

# Report Section 2: Vulnerability Write-Ups

## Vulnerability Write-Up Template

> **Title**  
Short and descriptive (e.g. _Unauthenticated SQL Injection in Login Form_).

> **Risk Rating**  
Use CVSS or the client's risk matrix. Rate each issue _in isolation_.

> **Summary**  
One or two sentences explaining what the vuln is and why it matters.

> **Background**  
Explain the issue simply, assuming the reader may not be a security expert. Help devs understand the root cause.

> **Technical Details & Evidence**  
Where and how you found it. Include:

- Endpoint, parameter, request/response
- Payloads
- Screenshots or code snippets


> **Impact**  
What a real attacker could _actually_ do with this vuln _in this specific system_.

> **Remediation**  
Actionable fix. Prioritize _root cause_, not just mitigation.

- E.g. for SQLi, recommend parameterized queries over just input sanitization.
- Tailor advice to the client’s tech stack. 

> **References** _(optional)_  
Links to relevant docs, vendor guidance, etc.

## Tips for Great Reports

- **Context is key:** Be specific to the system tested.
- Avoid generic, copy-paste advice.
- Answer:
    
    - Where exactly was the issue?
    - What does an attacker need?
    - How does this affect _this_ system?
    - How _should_ this client fix it?

---

# Report section: Appendices

Appendices are valuable for security teams and future testers to verify what was done, confirm scope, and follow up post-remediation. While formats vary, two key appendices should always be included:

### 1. **Assessment Scope**

This appendix shows how closely the testing matched the original scope in the Rules of Engagement. It should note any changes, limitations, or gaps in coverage. For example, if only 80% of the scope was tested, a reassessment may be needed for the remaining 20%.

### 2. **Assessment Artifacts**

Use this section to list any test-related artifacts left behind, such as uploaded files or changes made during testing. Even with cleanup, some items may remain and could be mistaken for real threats later. Document these with removal recommendations to avoid future confusion.