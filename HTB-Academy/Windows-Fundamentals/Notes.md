# Notes for Windows Fundamentals

```powershell
# General System Information
Get-WmiObject -Class Win32_OperatingSystem | Select Version, BuildNumber

# File System Exploration
dir c:\ /a
tree c:\ /f | more

# Security Identifiers (SIDs)
Get-WmiObject -Class Win32_UserAccount
whoami /user

# Creating a User 'Jim'
New-LocalUser -Name "Jim" -Password (ConvertTo-SecureString "Password123!" -AsPlainText -Force) -FullName "Jim"
Set-LocalUser -Name "Jim" -PasswordNeverExpires $true

# Creating a Security Group 'HR'
New-LocalGroup -Name "HR" -Description "HR Security Group"

# Adding 'Jim' to the 'HR' Security Group
Add-LocalGroupMember -Group "HR" -Member "Jim"

# Querying Service Details
Get-Service -Name "wuauserv" | Format-List *

# Registry Queries
reg query HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

# NTFS and Share Permissions
# Set permissions via GUI (no CLI example for this task, use Windows Explorer)
# Disable inheritance and configure specific permissions in the 'Security' tab.

# Retrieve Execution Policy
Get-ExecutionPolicy -List

# Modify Execution Policy for Current Session
Set-ExecutionPolicy Bypass -Scope Process

# Windows Defender Status
Get-MpComputerStatus | findstr "True"
