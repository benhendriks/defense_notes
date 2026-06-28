````markdown
# Blue Team Reference Cheatsheet

> Kompakte Lern- und Referenzübersicht für DFIR, Threat Hunting und Incident Response.

---

# Wireshark Display Filter

## Netzwerk

```text
ip.addr == 192.168.1.10
ip.src == 192.168.1.10
ip.dst == 8.8.8.8
````

## TCP

```text
tcp
tcp.port == 80
tcp.port == 443
tcp.flags.syn == 1
tcp.flags.reset == 1
tcp.analysis.retransmission
```

## HTTP

```text
http
http.request
http.response
http.host contains "google"
http.request.method == POST
```

## DNS

```text
dns
dns.qry.name contains "evil"
dns.flags.response == 0
```

## SMB

```text
smb
smb2
```

## Kerberos

```text
kerberos
```

## ICMP

```text
icmp
icmp.type == 8
```

---

# CyberChef

## Base64 Decode

```
From Base64
```

## Base64 Encode

```
To Base64
```

## URL Decode

```
URL Decode
```

## URL Encode

```
URL Encode
```

## Hex Dump

```
To Hex
```

## XOR Brute Force

```
XOR Brute Force
```

## Extract URLs

```
Extract URLs
```

## Extract IPs

```
Regular Expression
```

Regex

```
(?:[0-9]{1,3}\.){3}[0-9]{1,3}
```

---

# Volatility3

```bash
vol.py -f memory.raw windows.info
vol.py -f memory.raw windows.pslist
vol.py -f memory.raw windows.pstree
vol.py -f memory.raw windows.psscan
vol.py -f memory.raw windows.cmdline
vol.py -f memory.raw windows.netscan
vol.py -f memory.raw windows.dlllist
vol.py -f memory.raw windows.handles
vol.py -f memory.raw windows.filescan
vol.py -f memory.raw windows.dumpfiles
vol.py -f memory.raw windows.hashdump
vol.py -f memory.raw windows.malfind
vol.py -f memory.raw windows.registry.hivelist
```

---

# Linux Commands

## Dateien

```bash
ls -lah
pwd
cd
cp
mv
rm
mkdir
touch
```

## Suchen

```bash
find / -name file
grep "text" file
grep -Ri password .
locate file
```

## Netzwerk

```bash
ip a
ss -tulnp
netstat -ano
tcpdump -i eth0
```

## Prozesse

```bash
ps aux
top
htop
kill PID
```

## Hash

```bash
md5sum file
sha1sum file
sha256sum file
```

---

# CMD One-Liner

## This command will get network configuration information from the local system, including the assigned IP address and the device’s MAC address

```cmdline
ipconfig /all
```  

## This command will check running processes and programs and print a list to the terminal.

```cmdline
tasklist
``` 

## This command will display running processes and the associated binary file that was executed to create the process.

```cmdline
wmic process get description, executablepath
```

### This command will print a list of all system users to the terminal.

```cmdline
net user  
```

## This command will list all users that are in the administrators user group.

```cmdline
net localgroup administrators
```

## This command will list all services and detailed information about each one.

```cmdline
sc query | more 
```

## This command will list open ports on a system, which could show the presence of a backdoor.

```cmdline
netstat -ab 
```

--- 

# PowerShell One-Liner

## Prozesse

```powershell
Get-Process
```

## Dienste

```powershell
Get-Service
```

## Netzwerk

```powershell
Get-NetTCPConnection
```

## Eventlogs

```powershell
Get-WinEvent -LogName Security
```

## Dateien

```powershell
Get-ChildItem -Recurse
```

## Hash

```powershell
Get-FileHash file.exe -Algorithm SHA256
```

## Similar to ifconfig in CMD, we can use the two above commands to get network-related information from the system.

```powershell
Get-NetIPConfiguration 
```
```powershell
Get-NetIPAddress 
```

## Using the above command we can list all local users on the system.

```powershell
Get-LocalUser 
```

## We can provide a specific user to the command to only get information about them. Piping ( | ) the results to a “select” with a wildcard ( * ) will give us all of the properties for the command, providing us with valuable information about the account. This can be extremely useful for us as incident responders, especially when we find local accounts that do not expire or have passwords that don’t expire.

```powershell
Get-LocalUser -Name BTLO | select *
```

## The above command let’s us quickly identify running services on the system. By piping ( | ) the command to Out-GridView, we are telling PowerShell to show us the results in a nice windows, which is much easier to work with than outputting the results to the PowerShell window.

```powershell
Get-Service | Where Status -eq "Running" | Out-GridView 
```

## Another great command is the ability to group running processes by their priority value. Using the above command we can see the process name, the process ID (PID), and other information, where different priority ratings are grouped into tables.

```powershell
Get-Process | Format-Table -View priority 
```

## We can collect specific information from a service by including the name in the command (-Name ‘namehere’) or the Id, as shown above and below. Piping to Select * provides us with all the properties.

```powershell
Get-Process -Id 'idhere' | Select * 
``` 

## Similar to Services, Scheduled Tasks are often abused and utilized a common persistence technique. With the above command we can list tasks that are set to run after certain conditions are met.

```powershell

Get-ScheduledTask 
```

## We can dig deeper by specifying the task we’re interested in, and retrieving all properties for it.

```powershell
Get-ScheduledTask -TaskName 'PutANameHere' | Select * 
```


---

# Base64

## Linux

```bash
echo TEXT | base64
```

Decode

```bash
echo SGVsbG8= | base64 -d
```

PowerShell

```powershell
[Convert]::ToBase64String(...)
```

Decode

```powershell
[System.Text.Encoding]::UTF8.GetString(...)
```

---

# URL Encoding

Leerzeichen

```
%20
```

/

```
%2F
```

:

```
%3A
```

?

```
%3F
```

=

```
%3D
```

&

```
%26
```

---

# Hash Recognition

| Hash   | Länge |
| ------ | ----- |
| MD5    | 32    |
| SHA1   | 40    |
| SHA256 | 64    |
| SHA512 | 128   |

---

# MITRE ATT&CK

| Tactic               | Beispiele          |
| -------------------- | ------------------ |
| Initial Access       | Phishing           |
| Execution            | PowerShell         |
| Persistence          | Registry Run Keys  |
| Privilege Escalation | Token Manipulation |
| Defense Evasion      | Obfuscation        |
| Credential Access    | LSASS              |
| Discovery            | whoami             |
| Lateral Movement     | PsExec             |
| Collection           | Clipboard          |
| Exfiltration         | HTTPS              |
| Impact               | Ransomware         |

---

# Sysmon Event IDs

| ID | Bedeutung          |
| -- | ------------------ |
| 1  | Process Creation   |
| 2  | File Creation Time |
| 3  | Network Connection |
| 5  | Process Terminated |
| 6  | Driver Loaded      |
| 7  | DLL Loaded         |
| 8  | CreateRemoteThread |
| 10 | Process Access     |
| 11 | File Created       |
| 12 | Registry Object    |
| 13 | Registry Value Set |
| 22 | DNS Query          |

---

# Windows Security Event IDs

| Event | Beschreibung             |
| ----- | ------------------------ |
| 4624  | Successful Logon         |
| 4625  | Failed Logon             |
| 4634  | Logoff                   |
| 4648  | Explicit Credentials     |
| 4672  | Admin Privileges         |
| 4688  | Process Creation         |
| 4698  | Scheduled Task           |
| 4720  | User Created             |
| 4726  | User Deleted             |
| 4728  | Group Member Added       |
| 4732  | Local Group Member Added |
| 4740  | Account Locked           |
| 4768  | Kerberos TGT             |
| 4769  | Kerberos Ticket          |
| 4771  | Kerberos Failure         |
| 4776  | NTLM                     |
| 5140  | Share Access             |
| 7045  | Service Installed        |

---

# Windows Artefakte

## Registry

```
Run Keys
UserAssist
RecentDocs
MUICache
ShellBags
```

## Dateien

```
Prefetch
LNK
Jump Lists
Amcache
ShimCache
SRUM
Recycle Bin
```

## Browser

```
History
Downloads
Cookies
Cache
```

## Event Logs

```
Security
System
Application
Sysmon
PowerShell
```

## USB

```
USBSTOR
setupapi.dev.log
MountedDevices
```

---

# IOC Checkliste

* IP-Adresse
* Domain
* URL
* Hash
* Dateiname
* Registry Key
* Mutex
* Prozessname
* User-Agent
* Command Line
* Scheduled Task
* Service
* DLL
* Pipe
* Zertifikat

---

# Nützliche Tools

* Wireshark
* CyberChef
* Volatility3
* Autopsy
* FTK Imager
* KAPE
* PECmd
* Registry Explorer
* Process Explorer
* Process Monitor
* TCPView
* Sysinternals Suite
* VirusTotal
* Any.Run
* Hybrid Analysis

```
```

