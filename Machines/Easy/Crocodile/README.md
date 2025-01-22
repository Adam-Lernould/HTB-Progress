# Crocodile - HackTheBox Write-up

## Overview
The **Crocodile** machine challenges us to exploit a misconfigured FTP server and perform directory brute-forcing to find hidden resources. This write-up covers enumeration, FTP exploration, and gaining access to an administrative panel.

---

## Enumeration
1. **Nmap Scan**:
   - **Command**: `nmap -sC -sV <IP>`
   - **Results**:
     - **Port 21**: FTP (vsftpd 3.0.3) with anonymous login allowed.
     - **Port 80**: HTTP (Apache httpd 2.4.41).

2. **Anonymous FTP Login**:
   - **Command**: `ftp <IP>`
   - **Credentials**:
     - Username: `anonymous`
     - No password required.
   - Files found:
     - `allowed.userlist`
     - `passwords.txt`

---

## Exploitation
1. **FTP File Exploration**:
   - **Command to list files**: `dir`
   - **Command to download files**: `get <filename>`
   - Files analyzed using `cat` revealed potential usernames and passwords.

2. **Directory Brute-forcing**:
   - **Command**:
     ```bash
     gobuster dir --url http://<IP>/ --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,html
     ```
   - Found the `login.php` page.

3. **Admin Panel Access**:
   - Navigated to: `http://<IP>/login.php`
   - Used credentials from FTP to log in successfully.
   - Admin panel displayed the **root flag**.

---

## Flag
- **Root Flag**: `c7110277ac44d78b6a9fff2232434d16`

---

## Key Learnings
- Misconfigured FTP servers can reveal sensitive information.
- Directory brute-forcing is essential for discovering hidden resources.
- Combining multiple vectors can lead to administrative access.
