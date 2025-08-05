#thm #windows #active-directory 

---

- All credentials are **stored** in the **Domain Controllers**.
  
- Whenever a user tries to authenticate to a service using domain credentials, the service will need to ask the Domain Controller to verify if they are correct. 
	  Two protocols can be used for network authentication in windows domains:
	  
	- **Kerberos:** Used by any recent version of Windows. This is the default protocol in any recent domain.
	  
	- **NetNTLM:** Legacy authentication protocol kept for compatibility purposes.

---

# Kerberos Authentication

- Kerberos authentication protocol is the default authentication protocol in any recent Windows versions.
  
- Users who log into a service using Kerberos will be assigned **_tickets_**.
	- Think of tickets as proof of a previous authentication.
	- Users with tickets can present them to a service to demonstrate they have already authenticated into the network before and are therefore enabled to use it.

## Process of authenticating with Kerberos

1. The user sends their username and a timestamp to the Key Distribution Center (KDC), encrypted with a key based on their password. The KDC, usually on the Domain Controller, creates and returns a **Ticket Granting Ticket (TGT)** and a **Session Key**.
   
   The TGT lets the user request other tickets to access network services, without sending their password each time. The TGT is encrypted using a special account's password (krbtgt), so the user can’t read it. However, it contains a copy of the Session Key, allowing the KDC to recreate it later without storing it.
   
   ![[Pasted image 20250805174914.png]]


2.  When a user wants to access something on the network—like a file share, website, or database—they use their TGT to ask the KDC for a special ticket called a TGS. This ticket is made for the specific service they want to use.
   
	   To get the TGS, the user sends their TGT, a timestamp encrypted with their session key, and the name of the service they want to access (called the SPN).
	   
	   The KDC then sends back the TGS and a session key to talk to the service. The TGS is locked (encrypted) using the service’s password hash, so only that service can read it and get the session key inside.

![[Pasted image 20250805175311.png]]


3. The TGS can then be sent to the desired service to authenticate and establish a connection. The service will use its configured account's password hash to decrypt the TGS and validate the Service Session Key.

![[Pasted image 20250805175337.png]]


---

# NetNTLM Authentication

NetNTLM works using a challenge-response mechanism. The entire process is as follows:

![[Pasted image 20250805175405.png]]


1. The client sends an authentication request to the server they want to access.
2. The server generates a random number and sends it as a challenge to the client.
3. The client combines their NTLM password hash with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.
4. The server forwards the challenge and the response to the Domain Controller for verification.
5. The domain controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If they both match, the client is authenticated; otherwise, access is denied. The authentication result is sent back to the server.
6. The server forwards the authentication result to the client.


> **Note:** This process is for domain accounts. If a local account is used, the server doesn’t need to contact the domain controller because it already has the password hash stored locally.


---

# Other resources for deeper understanding


-   Authentication fundamentals: The basics | Microsoft Entra ID
	- https://www.youtube.com/watch?v=fbSVgC8nGz4

- Kerberos vs. LDAP: What’s the Difference?
	- https://www.youtube.com/watch?v=Xjpi8xYqPcY

- How Kerberos works:
	- https://www.youtube.com/watch?v=1yWW7VQUX0A&pp=ygUQa2VyYmVyb3MgdnMgbnRsbQ%3D%3D
