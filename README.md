# Password-audit-lab

## Purpose
The purpose of this lab was to perform a password audit to examine
the strength of passwords and understand why it can be a vulnerable
access point for hackers.

## Lab Setup
- Kali Linux and Metasploitable installed inside VirtualBox
- Running on my personal laptop in a controlled and safe home lab
  environment

## Tools Used
- nmap
- SSH
- SCP
- cat and sudo cat
- unshadow
- rockyou wordlist
- John the Ripper

## Methodology

### Step 1 - Discovering the Target IP
The ifconfig command was run on the target machine to discover
its IP address.

### Step 2 - Port Scanning
The command nmap -sV with the target IP was run on Kali Linux
to find the available ports on the target machine and their version
numbers. This was done to identify how broad the attack surface is.
It was found that port 22 was open.

### Step 3 - Establishing a Connection
A connection was established between Kali Linux and Metasploitable
using port 22 via an SSH connection with the target username and
IP address.

### Step 4 - Extracting Credential Files
Once the connection was established, the following commands were
run to extract the credential files from the target machine:
- cat /etc/passwd
- sudo cat /etc/shadow

### Step 5 - Transferring Files to Kali Linux
A second terminal was opened and the SCP command was used to
transfer the extracted files onto Kali Linux.

### Step 6 - Merging the Files
The transferred files were merged using the unshadow command:

unshadow passwd.txt shadow.txt > hashes.txt

This format is required by John the Ripper to process and crack
the passwords.

### Step 7 - Cracking the Passwords
The rockyou wordlist was used alongside John the Ripper. The
rockyou wordlist contains a large collection of real passwords.
John the Ripper ran through the wordlist, matched the hashes,
and the cracked passwords were revealed.

## Findings
- Open ports are entry points for attackers
- Strong passwords are critical for organisations
- Regular password audits should be conducted to identify
  weak credentials before attackers do

## What I Learned
This lab taught me how important it is to have strong passwords
and how one should not settle with default passwords. It showed
me how important credentials are, especially root credentials.
It also demonstrated how a simple wordlist attack can reveal
weak passwords and why organisations must enforce strong
password policies.

## Disclaimer
This was conducted in a controlled home lab environment using
intentionally vulnerable software for educational purposes only.
No real systems were involved.
