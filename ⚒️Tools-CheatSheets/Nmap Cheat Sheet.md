#reconnaissance #enumeration 

---

# 📥 Installation & Updating

```bash
# Debian/Ubuntu
sudo apt update && sudo apt install nmap

# RedHat/CentOS
sudo yum install nmap

# macOS (Homebrew)
brew install nmap

# Update NSE scripts
sudo nmap --script-updatedb
```

---

## 🎯 Host Discovery

|Option|Description|
|---|---|
|`-sn`|Ping scan (no port scan)|
|`-Pn`|Treat all hosts as online (skip host discovery)|
|`-PR`|ARP ping (local LAN only; root)|
|`-PE` / `-PP`|ICMP echo / timestamp ping|
|`-PS` / `-PA`|TCP SYN / ACK ping to specified ports|

```bash
# Discover live hosts in subnet (skip port scan)
nmap -sn 10.0.0.0/24

# Ping with SYN to 443 & 80 (if ICMP is blocked)
nmap -PS443,80 192.0.2.0/24
```

---
## 🔌 Port Scan Types

| Scan Type           | Flag           | Privileged? | Notes                                     |
| ------------------- | -------------- | ----------- | ----------------------------------------- |
| TCP SYN (“Stealth”) | `-sS`          | yes         | Fast; doesn’t complete handshake          |
| TCP Connect         | `-sT`          | no          | Full handshake; easy to detect            |
| UDP                 | `-sU`          | yes         | Slow; many filtered ports                 |
| SCTP INIT           | `-sY`          | yes         | SCTP equivalent of SYN scan               |
| SCTP COOKIE-ECHO    | `-sZ`          | yes         | Full SCTP handshake                       |
| Null                | `-sN`          | yes         | No flags set; stealthy on some OS         |
| FIN                 | `-sF`          | yes         | Only FIN flag; stealthy                   |
| Xmas                | `-sX`          | yes         | FIN, PSH, URG flags                       |
| ACK scan            | `-sA`          | yes         | Window size analysis; map firewall rules  |
| Window scan         | `-sW`          | yes         | Like ACK but checks window field          |
| Maimon              | `-sM`          | yes         | FIN+ACK; rare                             |
| Idle (“Zombie”)     | `-sI <zombie>` | yes         | Uses idle host to probe target stealthily |
```bash
# Stealthy SYN scan + top 100 ports
nmap -sS --top-ports 100 192.0.2.10

# UDP scan of critical ports
nmap -sU -p 53,67-69,161 192.0.2.0/28
```

---

# 🔍 Service & Version Detection

```bash
# Probe open ports to identify services + versions
nmap -sV 192.0.2.10

# Intense version scan (all probes, slower)
nmap -sV --version-all target.example.com
```

---

# 🕸️ Nmap Scripting Engine (NSE)

|Mode|Example|Use‑Case|
|---|---|---|
|Default|`-sC`|run “default” category scripts|
|All|`--script=all`|run every script|
|Category|`--script=vuln,auth`|vuln‑ & auth‑related scripts|
|Specific|`--script=http-vuln-cve2017-5638`|single NSE script|

```bash
# List available scripts
ls /usr/share/nmap/scripts/*.nse

# Get help for a script
nmap --script-help http-brute

# Run HTTP PUT exploit script with args
nmap -p 80 --script http-put \
  --script-args=http-put.url='/dav/shell.php',http-put.file='./shell.php' \
  target.com

```

---

# ⏱️ Timing & Performance

| Template | Speed      | Notes               |
| -------- | ---------- | ------------------- |
| `-T0`    | Paranoid   | very slow           |
| `-T1`    | Sneaky     | slow                |
| `-T2`    | Polite     | reduced load        |
| `-T3`    | Normal     | default             |
| `-T4`    | Aggressive | faster, more noise  |
| `-T5`    | Insane     | fastest, very noisy |

```bash
# Aggressive timing + minimal retries
nmap -T4 --max-retries 2 target.net

# Slow scan to evade IDS
nmap -T1 --scan-delay 500ms 10.0.0.0/24
```

---

# 🛡️ Firewall / IDS Evasion

```bash
# Packet fragmentation
nmap -f target.com

# Custom MTU
nmap --mtu 24 target.com

# Obfuscate source with decoys
nmap -D RND:10 192.0.2.20

# Fake source port
nmap --source-port 53 target.com

# Invalid checksum
nmap --badsum target.com
```

> **Tip:** Using several techniques together can help bypass basic filters, but may also trigger more advanced IDS.

---

## 💾 Output Formats

| Option | File                       |
| ------ | -------------------------- |
| `-oN`  | normal output (plain text) |
| `-oX`  | XML                        |
| `-oG`  | grepable                   |
| `-oA`  | all of the above (prefix)  |

---

## 🔧 Miscellaneous Tips

- `--open`: show only open/filtered ports.
    
- `--reason`: display why a port is flagged (e.g., RST response).
    
- `--packet-trace`: debug raw packet send/receive.
    
- `--traceroute`: perform traceroute at end of scan.
    
- `--data-length <bytes>`: pad packets, evade signature‑based IDS.
    
- `--min-rate` / `--max-rate`: packets per second control.
    
- `--script-updatedb`: update local NSE script database.

---

# 🚀 Example Workflows

## **Quick Recon (stealthy)**

```bash
nmap -sn -PS80,443 10.0.0.0/24
nmap -sS --top-ports 50 -T4 10.0.0.0/24
```

## Full UDP + TCP Sweep

```bash
nmap -sS -sU -p- -T3 192.168.1.0/24
```

## Vulnerability Scan

```bash
nmap -sV --script vuln -oA vuln_scan 203.0.113.0/28
```

## Firewall Evasion

```bash
nmap -sS -f --mtu 16 -D RND:5 --source-port 53 target.com
```

---

# Nmap resources

- Official Nmap book & docs: [Nmap documentation](https://nmap.org/book/)
- NSE script directory: [Scripts](https://nmap.org/nsedoc/)