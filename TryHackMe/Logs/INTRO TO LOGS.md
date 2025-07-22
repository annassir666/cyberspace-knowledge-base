#SOC #forensics #fundamentals #thm 

---

# Log Types

- **Application Logs**: Messages about specific applications, including status, errors, warnings
- **Audit Logs**: A list of actions taken, used to follow rules and stay compliant (for example, the log is made when an employee logs into a system or changes a file.)
- **Security Logs**: Events such as logins, permission changes, firewall activity, etc
- **Server Logs**: Logs a server generates, including system, event, error, and access logs
- **System Logs**: Kernel activities, system errors, boot sequences, and hardware status
- **Network Logs**: Network traffic, connections, and other network-related events
- **Database Logs**: database activities, such as queries and updates
- **Web Server Logs**: Requests processed by a web server, including URLs, response codes, etc



# Log Formats

- **Semi-structured Logs**: These logs may contain structure and unstructured data  with predictable components accommodating free-form text:
	- **Syslog Message Format:** A widely adopted logging protocol for system and network logs.
		- `May 31 12:34:56 WEBSRV-02 CRON[2342593]: (root) CMD ([ -x /etc/init.d/anacron ] && if [ ! -d /run/systemd/system ]; then /usr/sbin/invoke-rc.d anacron start >/dev/null; fi)`
		  
	  - **Windows Event Log (EVTX) Format:** Proprietary Microsoft log for Windows systems.
		  - `Get-WinEvent -Path "C:\Windows\System32\winevt\Logs\Application.evtx"`
		    
		    
- **Structured Logs:** Following a strict and standardized format, these logs are conducive to parsing and analysis. Typical structured log formats include:
	- **Field Delimited Formats:** Comma-Separated Values (CSV) and Tab-Separated Values (TSV) are formats often used for tabular data.
	  
	- **JavaScript Object Notation (JSON):** Known for its readability and compatibility with modern programming languages.
	  
	- **W3C Extended Log Format (ELF):** Defined by the World Wide Web Consortium (W3C), customizable for web server logging. It is typically used by Microsoft Internet Information Services (IIS) Web Server.
	  
	- **eXtensible Markup Language (XML):** Flexible and customizable for creating standardized logging formats.
	  
	  
- **Unstructured Logs:** Comprising free-form text, these logs can be rich in context but may pose challenges in systematic parsing. Examples include:
	- **NCSA Common Log Format (CLF):** A standardized web server log format for client requests. It is typically used by the Apache HTTP Server by default.
	  
	- **NCSA Combined Log Format (Combined):** An extension of CLF, adding fields like referrer and user agent. It is typically used by Nginx HTTP Server by default.



# Log Standards

- **[**Common Event Expression (CEE):](https://cee.mitre.org/)** This standard, developed by MITRE, provides a common structure for log data, making it easier to generate, transmit, store, and analyze logs.
- **[OWASP Logging Cheat Sheet:](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)** A guide for developers on building application logging mechanisms, especially related to security logging.
- **[Syslog Protocol:](https://datatracker.ietf.org/doc/html/rfc5424)** Syslog is a standard for message logging, allowing separation of the software that generates messages from the system that stores them and the software that reports and analyses them.
- **[NIST Special Publication 800-92:](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-92.pdf)** This publication guides computer security log management.
- **[Azure Monitor Logs:](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/data-platform-logs)** Guidelines for log monitoring on Microsoft Azure.
- **[Google Cloud Logging:](https://cloud.google.com/logging/docs)** Guidelines for logging on the Google Cloud Platform (GCP).
- **[Oracle Cloud Infrastructure Logging:](https://docs.oracle.com/en-us/iaas/Content/Logging/Concepts/loggingoverview.htm)** Guidelines for logging on the Oracle Cloud Infrastructure (OCI). 
- **[Virginia Tech - Standard for Information Technology Logging:](https://it.vt.edu/content/dam/it_vt_edu/policies/Standard_for_Information_Technology_Logging.pdf)** Sample log review and compliance guideline.