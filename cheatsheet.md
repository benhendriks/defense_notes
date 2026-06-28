# Blue Team / SOC Fundamentals Cheatsheet

> These notes will come handy in exam.
>
> Compact reference for SOC, DFIR, Threat Hunting, and Incident Response.

---

# Common Ports

| Port | Service | Description |
|---|---|---|
|20,21|FTP|File Transfer Protocol|
|22|SSH|Secure remote access|
|23|Telnet|Unencrypted remote access|
|25|SMTP|Email transfer|
|53|DNS|Domain resolution|
|67,68|DHCP|Automatic IP assignment|
|80|HTTP|Web traffic|
|443|HTTPS|Encrypted web traffic|
|514|Syslog|Centralized logging|

---

# Wireshark Filters

## Network

```text
ip.addr == 192.168.1.10
ip.src == 192.168.1.10
ip.dst == 8.8.8.8

---

# Phishing Analysis

## IOC Collection

### Email Artifacts

- Sender address
- Subject line
- Recipients
- Sending server IP
- Reverse DNS
- Reply-To
- Date/time

### Web Artifacts

- URL
- Domain
- IP address

### File Artifacts

- Filename
- MD5
- SHA1
- SHA256

---

# Reputation / Analysis Tools

## URL

- VirusTotal
- URLScan
- URLhaus
- AbuseIPDB

## Malware Sandbox

- Any.Run
- Hybrid Analysis
- Joe Sandbox

---

# Digital Forensics

## Data Representation

- Base64
- Hexadecimal
- Octal
- ASCII
- Binary

---

# File Carving

```bash
scalpel -b -o <output> <disk image>
