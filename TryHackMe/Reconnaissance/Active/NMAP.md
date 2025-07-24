#reconnaissance #thm 

---

# Nmap Scan Types

## 🔹 Basic Scans

### TCP Connect Scan `-sT`
- **What it does:** Lets the OS do a full TCP connection (`SYN → SYN/ACK → ACK`).
- **Pros:** Always works (no root needed).
- **Cons:** Easy for target to log (complete handshake).
  
![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-2.png)

![[Pasted image 20250723023252.png]]


### SYN “Half‑open” Scan `-sS`
- **What it does:** Sends `SYN`, waits for `SYN/ACK`, then sends `RST` instead of `ACK`.
- **Pros:** Faster; stealthier (no full handshake). 
	- Old firewalls look for complete 3-way handshake, which is why this -sS type scan is stealthy. 
	- SYN scans are often not logged by applications listening on open ports, as standard practice is to log a connection once it's been fully established.
	  
- **Cons:** Requires root/admin privileges. Newer IDS and IPS systems can detect this type of scanning.
  
- When using a SYN scan to identify closed and filtered ports, the exact same rules as with a TCP Connect scan apply. If a port is closed then the server responds with a RST TCP packet. If the port is filtered by a firewall then the TCP SYN packet is either dropped, or spoofed with a TCP reset.

![[Pasted image 20250723170136.png]]

![[Pasted image 20250723170143.png]]


### 🔍 UDP Scan `-sU`

- **What it does:** Sends raw (often empty) UDP packets to target ports.
  
- **How it works:**
    - **No handshake** (UDP is stateless).
    - **No response** usually = `open|filtered` (could be open or firewalled).
    - **ICMP "port unreachable"** = port is closed.
      
- **Pros:** Detects services like **DNS**, **SNMP**, **NTP** on UDP ports.
  
- **Cons:**
    - **Slow** – no responses = longer timeouts + retries.
    - **Unreliable** – many firewalls drop UDP silently.

- **Tip:** Use `--top-ports <n>` to speed up scans:
    `nmap -sU --top-ports 20 <target>`


---

## 🔹 Less Common TCP Scans (Stealthy / Firewall Evasion)

These scans are based on **sending unusual TCP packets** that don’t follow the normal connection rules. They're mostly used for:
- Evading simple firewalls or intrusion detection systems (IDS)
- OS fingerprinting
- Detecting open ports **without completing a connection**

They all rely on how different operating systems (especially Unix-based ones) respond to unexpected TCP packets.

---

### 🔸 Null Scan `-sN`

- **Flags:** No TCP flags set at all.
- **How it works:**  
  Sends a “blank” TCP packet. Normal traffic would always include at least one flag (like SYN, ACK, etc.), so this is intentionally strange.

![[Pasted image 20250723172058.png]]


- **Expected Response (on Unix-like systems):**  
  - If the port is **closed** → the target sends back a **RST** (reset) packet.  
  - If the port is **open** → the system **ignores** it (no response).

- **Nmap Output Meaning:**  
  - **No response** → `open|filtered`  
  - **RST** → `closed`

- **Use case:** Stealthy scans to avoid detection by simple firewalls or logging systems.

---

### 🔸 FIN Scan `-sF`

- **Flags:** Only the **FIN** flag is set.  
- **FIN** is normally used to gracefully end a TCP connection.

- **How it works:**  
  Sends a TCP packet with the FIN flag **without a prior connection**.

![[Pasted image 20250723172135.png]]


- **Expected Response (on Unix-like systems):**  
  - **Closed port** → replies with **RST**  
  - **Open port** → silently **ignores** the packet

- **Nmap Output Meaning:**  
  - **No response** → `open|filtered`  
  - **RST** → `closed`

- **Use case:** Useful for bypassing stateless firewalls or hiding scans.

---

### 🔸 Xmas Scan `-sX`

- **Flags:** FIN, PSH, and URG are all set  
  (makes the packet look "lit up like a Christmas tree" — hence the name 🎄)

- **How it works:**  
  Sends an odd-looking TCP packet that shouldn't normally appear in traffic.

![[Pasted image 20250723172206.png]]


- **Expected Response (on Unix-like systems):**  
  - **Closed port** → responds with **RST**  
  - **Open port** → no response

- **Nmap Output Meaning:**  
  - **No response** → `open|filtered`  
  - **RST** → `closed`

- **Use case:** Same as above — stealth and firewall evasion.

---

## ⚠️ Important Notes

- These scan types **only work reliably** on **Unix-based targets** (like Linux, BSD, etc.).  
  
- **Windows systems** do **not follow** the same rules — they usually respond with **RST** to *any* unexpected TCP packet, whether the port is open or closed. So these scans won’t work well against Windows.

- Firewalls may also drop these packets entirely, which is why Nmap often reports ports as `open|filtered` — it can’t be sure whether the lack of response means the port is open, or if a firewall is filtering the packet.

---

## 🧠 Summary Table

| Scan Type | TCP Flags | Closed Port Response | Open Port Response | Reliable on Windows? |
|-----------|------------|----------------------|--------------------|-----------------------|
| Null (`-sN`) | None        | RST                  | No response         | ❌ No                  |
| FIN (`-sF`)  | FIN         | RST                  | No response         | ❌ No                  |
| Xmas (`-sX`) | FIN, PSH, URG | RST                | No response         | ❌ No                  |


> **Note:** Windows hosts generally ignore these and always reply with RST, so they’re less useful against Windows targets.

---

## 🔹 ICMP Scan (Ping)

### Goal
Identify which IPs in a network have active hosts (network mapping).
**Nmap** with the `-sn` option.

### What does `-sn` do?
- Tells Nmap to **skip port scanning**.
- Only checks if hosts are **up** (alive), not which ports are open.

### How does it detect live hosts?
Nmap tries multiple methods to provoke a response from a host:

- **ICMP echo request (ping)**
- **ARP requests** (on local network when run as root)
- **TCP SYN to port 443**
- **TCP ACK to port 80** (or TCP SYN if not run as root)

> 🧠 **Why use TCP packets to ports 80 and 443?**
Some hosts or firewalls:
- **Block ICMP traffic** (so pings are ignored).
- But **respond to TCP traffic** on common ports like **80 (HTTP)** and **443 (HTTPS)**.

By sending TCP packets to these well-known ports:
- Nmap increases the chance of getting a **response** (e.g., TCP RST).
- This helps confirm a host is **alive**, even when ICMP is blocked.

### 🧪 Examples
```bash
nmap -sn 192.168.0.1-254
nmap -sn 192.168.0.0/24

```

---

> **Tip:**  
> - Use **TCP Connect** (`-sT`) if you’re unprivileged or want simplicity.  
> - Use **SYN Scan** (`-sS`) for speed and stealth (requires root).  
> - Mix **UDP** (`-sU`) and **TCP** scans to cover both transport layers.  
> - Only use **Null/FIN/Xmas** scans when you need to sneak past simple filters and know your target OS behavior.  


---


# NSE Scripts

## Overview

Nmap Scripting Engine extends nmap's functionality incredibly. Nmap is now able not only to do simple scans, but also check services for vulnerabilities and even automating exploits for them.

There are many categories available. Some useful categories include:

- `safe`:- Won't affect the target
- `intrusive`:- Not safe: likely to affect the target  
- `vuln`:- Scan for vulnerabilities
- `exploit`:- Attempt to exploit a vulnerability
- `auth`:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
- `brute`:- Attempt to brute force credentials for running services
- `discovery`:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

A more exhaustive list can be found [here](https://nmap.org/book/nse-usage.html).

---

## Working with NSE

Multiple scripts can be run simultaneously in this fashion by separating them by a comma. For example: `--script=smb-enum-users,smb-enum-shares`.


- Some scripts require arguments (for example, credentials, if they're exploiting an authenticated vulnerability). These can be given with the `--script-args`Nmap switch. An example of this would be with the `http-put` script (used to upload files using the PUT method). This takes two arguments: the URL to upload the file to, and the file's location on disk.  For example:
	- `nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'`
	  
- A full list of scripts and their corresponding arguments (along with example use cases) can be found [here](https://nmap.org/nsedoc/).

- Nmap scripts come with built-in help menus, which can be accessed using `nmap --script-help <script-name>`. This tends not to be as extensive as in the link given above, however, it can still be useful when working locally.


---

## Searching For Scripts

We have two options to find nmap scripts. They are:
- The first is the page on the [Nmap website](https://nmap.org/nsedoc/)
-  The second is the local storage on your attacking machine. Nmap stores its scripts on Linux at `/usr/share/nmap/scripts`.

- There are two ways to search for installed scripts. One is by using the `/usr/share/nmap/scripts/script.db` file. 

![[Pasted image 20250724184457.png]]

---
### Installing New Scripts

 It's possible to install the scripts manually by downloading the script from Nmap org
	(`sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`). 
This must then be followed up with `nmap --script-updatedb`, which updates the `script.db` file to contain the newly downloaded script.


---

# Firewall Evasion

- Most Windows systems block ICMP (ping) by default. This is a problem because tools like Nmap use ping to check if a host is online. If pings are blocked, Nmap may think the host is offline and skip scanning it.

- To fix this, you can use the `-Pn` option in Nmap. This tells Nmap to skip the ping check and assume the host is up. It helps bypass the ICMP block, but can slow down the scan—especially if the host really is offline.

- Also, if you’re on the same local network, Nmap can use ARP (instead of ping) to see if a host is active.

There are a variety of other switches which Nmap considers useful for firewall evasion. We will not go through these in detail, however, they can be found [here](https://nmap.org/book/man-bypass-firewalls-ids.html).

- The following switches are of particular note:

	- `-f`:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS. 
	- An alternative to `-f`, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This _must_ be a multiple of 8.
	- `--scan-delay <time>ms`:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
	- `--badsum`:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.