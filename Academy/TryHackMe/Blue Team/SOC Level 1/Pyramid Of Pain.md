#fundamentals #SOC #models #thm #SOC 

---

[![What is the Pyramid of Pain? - Cymulate](https://cymulate.com/uploaded-files/2024/09/pyramid-of-pain-1.png)

---
# What is the Pyramid of Pain

The **Pyramid of Pain** is a cybersecurity concept that shows how hard it is for an attacker when you detect and block certain types of information (called "indicators") they use during an attack.

It’s shaped like a pyramid because **the higher you go, the more pain you cause to the attacker** when you detect or block that thing.

## Levels of the Pyramid (from bottom to top):

1. **Hash Values** – Unique digital fingerprints of files. Easy to block. Easy for attackers to change.
    
2. **IP Addresses** – Where the attack is coming from. Also easy to block and change.
    
3. **Domain Names** – Websites used in the attack. A bit harder to change than IPs, but still not too hard.
    
4. **Network/Host Artifacts** – Clues left on the system (like strange processes or registry keys). Harder to change.
    
5. **Tools** – Software the attacker uses (like malware or hacking frameworks). Even harder to swap out.
    
6. **Tactics, Techniques, and Procedures (TTPs)** – The attacker’s behavior, methods, and strategies. **Very hard to change** – if you can detect and defend against these, you cause the most pain.

## How to use the Pyramid of Pain?

- When hunting threats or creating detection rules, try to **move up the pyramid**.
    
- Focus on detecting **tools** and **techniques**, not just IPs or file names.
    
- Use threat intelligence to understand an attacker’s methods and build smarter defenses.

---
# Hashing Values (Trivial)

- MD5 (Message Digest) - was designed in 1992. MD is a widely used cryptographic hash function with a 128-bit hash value. MD5 hashes are **NOT** considered **cryptographically secure**.
  
- SHA-1 (Secure Hash Algorithm 1). When data is fed to SHA-1 Hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number. NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3 families.
  
- **The SHA-2 (Secure Hash Algorithm 2)**. SHA-2 has many variants, and arguably the most common is SHA-256. The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number.


Security professionals use hash to identify and track malware or suspicious files. Various online tools can be used to do hash lookups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).


---
# IP Address (Easy)

An **IP address** identifies any device on a network, like desktops, servers, or CCTV cameras. In the **Pyramid of Pain**, IP addresses are shown in **green**. Knowing an attacker’s IP address can help block their access, but it’s easy for them to change it.

Attackers use **Fast Flux** to hide their activities. This technique involves constantly changing IP addresses linked to a single domain, making it hard for defenders to block the malicious connections.

---

# **Domain Names (Simple)**

Domain names map IPs to human-readable strings, like:

- `evilcorp.com` (domain + TLD)
- `tryhackme.evilcorp.com` (subdomain + domain + TLD)

## 🎯 Why Domain Names Matter

- Harder for attackers to change than IPs
- Requires registration + DNS setup
- Some DNS providers are too lenient and offer APIs that simplify abuse

## 🧨 Punycode Attacks

> **Punycode** encodes Unicode characters into ASCII — attackers use this to spoof legit domains.

### 🧬 Example

- **Looks like:** `adıdas.de`
- **Actually:** `http://xn--addas-o4a.de/`
- **Goal:** Trick users into thinking it’s `adidas.de`

### ⚠️ Why It Works
- Hard to spot visually
- Used in phishing, malware delivery, and fake login pages
- Most browsers now show Punycode if the domain seems suspicious

## 🔍 Detecting Suspicious Domains

Use:

- Proxy logs
- Web server logs
- Look for weird characters or redirections

- URL Shortens: `bit.ly, goo.gl, ow.ly, s.id, smarturl.it, tiny.pl, tinyurl.com, x.co`


---

# **Host Artifacts (Annoying)**

At this level, if you can detect the attack, the attacker will likely get annoyed and frustrated. They’ll have to go back and change their tools and methods, which takes a lot of time and effort. This also means they might need to spend more resources on better tools to keep going.

Host artifacts are the traces attackers leave on a system. These can include things like changes to the registry, suspicious processes, known attack patterns or IOCs (Indicators of Compromise), and files created by malware. Basically, anything that’s specific to the threat and shows the system was targeted.

**Suspicious process execution from Word:**
![[Pasted image 20250416095416.png]]

**Suspicious events followed by opening a malicious application:**
![[Pasted image 20250416095523.png]]

---

# **Network Artifacts (Annoying)**

 If you can detect a threat early, the attacker has to go back and change their tools or methods, which slows them down and gives you more time to react and fix things. One way to do this is by spotting **network artifacts**, which are unusual signs in network traffic—like strange User-Agent strings, weird patterns in web requests (like HTTP POSTs), or details about how the attacker tries to control the system (C2 info). These can be found by analyzing network data using tools like **Wireshark**, **TShark**, or looking at alerts from systems like **Snort**.
 ![[Pasted image 20250416101233.png]]


If you can detect the custom User-Agent strings that the attacker is using, you might be able to block them, creating more obstacles and making their attempt to compromise the network more annoying.


---

# **Tools (Challenging)**

The **Tools** level refers to the **software and malware** attackers use — like backdoors, stealers, droppers, or even legit tools like Nmap and Mimikatz.

When you detect or block these, it really **hurts the attacker**. They’ll need to:

- Rebuild or reconfigure their tools
- Buy or develop new ones
- Learn how to use something else

### 🧰 Examples of Tools

- Malicious macros (in phishing docs)
- RATs and backdoors (e.g., Remcos, njRAT)
- Custom `.exe` / `.dll` files
- Password dumpers (Mimikatz, LaZagne)
- C2 frameworks (Cobalt Strike, Sliver)    
- Hacking tools (Impacket, Nmap, BloodHound)

### 🛡️ How to Detect Tools

- **Antivirus signatures**
- **YARA rules** – for pattern-matching
- **Fuzzy hashing (SSDeep)** – to find _similar_ files
- **Threat detection rules** – from SOC Prime
- **Malware samples & feeds** – from:
    - MalwareBazaar
    - [Malshare](https://malshare.com/)
    - [VirusTotal](https://virustotal.com/)

- Use **SSDeep** to compare files for similarity — great for catching repacked or modified malware:

### ⚔️ Why This Matters

If you detect their tools:

- They lose access
    
- Their payload fails
    
- They need to retool


---

# **TTPs – Tactics, Techniques & Procedures**

TTPs are how attackers **actually operate**:  
Their behaviors, methods, and goals.  
This includes everything in the MITRE ATT&CK Matrix:

- Phishing
- Privilege escalation
- Lateral movement
- Data exfiltration  

### 🧠 Why TTPs Matter

If you can detect **what** an attacker is doing (not just their tools), you can:

- Spot _new or unknown_ threats
- Shut down attacks early
- Stop them before they get what they want

Example:  
💡 Detecting a **Pass-the-Hash** attack via Windows Event Logs lets you:

- Find the compromised host
- Stop lateral movement
- Kick the attacker out **fast**

### ⚔️ What Happens When You Stop TTPs?

The attacker now has two options:

1. Go back to square one — retrain, retool, rethink
2. Give up and move on to an easier target