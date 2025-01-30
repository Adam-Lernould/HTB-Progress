# Managing Services with SC
```
# Query service configuration
sc qc wuauserv

# Stop a service (requires admin privileges)
sc stop wuauserv

# Modify the binary path of a service
sc config wuauserv binPath= C:\Windows\UpdatedProgram.exe

# Show detailed permissions for a service
sc sdshow wuauserv
```
# Registry Management
```
# Query critical Run and RunOnce keys
reg query HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
```

# SID Management
```
# Retrieve all user SIDs
Get-WmiObject -Class Win32_UserAccount | Select Name, SID

# Retrieve SID for a specific user (e.g., 'Jim')
Get-WmiObject -Class Win32_UserAccount | Where-Object {$_.Name -eq "Jim"} | Select SID

# WMI Operations
# Retrieve operating system details
Get-WmiObject -Class Win32_OperatingSystem | Select SystemDirectory, BuildNumber, SerialNumber, Version

# Invoke a WMI method (example: renaming a file)
Invoke-WmiMethod -Path "CIM_DataFile.Name='C:\users\public\spns.csv'" -Name Rename -ArgumentList "C:\Users\Public\renamed_file.csv"
```