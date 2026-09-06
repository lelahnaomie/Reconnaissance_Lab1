# Lab 1 – Network and Service Reconnaissance with Nmap and WhatWeb

**Course:** WADF104 – Cybersecurity Foundations
**Student:** Lelah Nde Ide Naomie
**Platform:** Kali Linux + Metasploitable2 (VirtualBox, Host-only isolated network)
**Target:** 192.168.56.104 (Metasploitable2)
**Attacker host:** 192.168.56.105 (Kali)

## Objective

Perform authorised reconnaissance against Metasploitable2: identify the host, enumerate
open TCP/UDP services, determine service versions, fingerprint the operating system,
run safe NSE enumeration scripts, and fingerprint the exposed web service with WhatWeb.

## Contents of this repository

| File | Description |
|---|---|
| `Lab1_Network_Service_Reconnaissance_Report.docx` | Full report: methodology, 14 embedded evidence screenshots, final service inventory table, OS fingerprint, and answers to all 14 Part 8 questions. |

## Summary of findings

- **28 open TCP ports** and **4 open UDP ports** identified via full-range scanning (`-p-`).
- **OS fingerprint:** Linux kernel 2.6.9–2.6.33 (general-purpose device).
- Key services: vsftpd 2.3.4 (anonymous login allowed), OpenSSH 4.7p1, Postfix smtpd,
  ISC BIND 9.4.2, Apache httpd 2.2.8 (Ubuntu) DAV/2, Samba 3.0.20-Debian, MySQL 5.0.51a,
  PostgreSQL 8.3.x, UnrealIRCd, distccd, and several RPC/Java-RMI services on
  high-numbered ports only visible via the full port scan.
- **WhatWeb** confirmed the web stack: Apache 2.2.8, PHP 5.2.4-2ubuntu5.10, WebDAV v2;
  aggression level 4 additionally (and speculatively) flagged a possible Matomo install.

## Commands used (see report for full sequence and output)

```bash
nmap -sn 192.168.56.0/24
nmap 192.168.56.104
nmap -sV 192.168.56.104
sudo nmap -O 192.168.56.104
sudo nmap -A 192.168.56.104
sudo nmap -p- -sV 192.168.56.104
sudo nmap -sU 192.168.56.104
nmap -sC -sV 192.168.56.104
whatweb -a 4 -v http://192.168.56.104
```

## Authorisation

All testing was performed exclusively against Metasploitable2 VM
on an isolated VirtualBox Host-only network, with no external or production systems
involved at any point.
