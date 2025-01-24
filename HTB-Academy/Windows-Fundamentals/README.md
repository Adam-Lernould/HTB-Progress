# Windows Fundamentals - Comprehensive Write-up

## Overview
This module explores Windows operating system fundamentals, including structure, file systems, permissions, services, security practices, and administrative tools. It serves as a foundation for IT professionals and penetration testers to effectively manage, assess, and secure Windows environments.

---

## Key Questions and Answers
1. **What is the Build Number of the target workstation?**
   - **Answer**: `19041`

2. **Which Windows NT version is installed on the workstation?**
   - **Answer**: `Windows 10`

3. **Find the non-standard directory in the C drive. Submit the contents of the flag file saved in this directory.**
   - **Answer**: `c8fe8d977d3a0c655ed7cf81e4d13c75`

4. **What protocol discussed in this section is used to share resources on the network using Windows?**
   - **Answer**: `SMB`

5. **What is the name of the utility that can be used to view logs made by a Windows system?**
   - **Answer**: `Event Viewer`

6. **What is the full directory path to the Company Data share we created?**
   - **Answer**: `C:\Users\htb-student\Desktop\Company Data`

7. **Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName).**
   - **Answer**: `FoxitReaderUpdateService.exe`

8. **Find the Execution Policy set for the LocalMachine scope.**
   - **Answer**: `Unrestricted`

9. **Find the SID of the bob.smith user.**
   - **Answer**: `S-1-5-21-2614195641-1726409526-3792725429-1003`

10. **What 3rd party security application is disabled at startup for the current user?**
    - **Answer**: `NordVPN`

11. **What is the name of the group that is present in the Company Data Share Permissions ACL by default?**
    - **Answer**: `Everyone`

12. **What is the name of the tab that allows you to configure NTFS permissions?**
    - **Answer**: `Security`

13. **What is the name of the service associated with Windows Update?**
    - **Answer**: `wuauserv`

14. **List the SID associated with the user account Jim you created.**
    - **Answer**: `S-1-5-21-2614195641-1726409526-3792725429-1006`

15. **List the SID associated with the HR security group you created.**
    - **Answer**: `S-1-5-21-2614195641-1726409526-3792725429-1007`

---

## Key Insights and Learnings

### **File Systems**
- **NTFS**:
  - Provides robust security and journaling.
- **FAT32**:
  - Simple and widely compatible but limited in file size.

### **Permissions**
- NTFS permissions offer granular control over access.
- Share permissions are configured separately for network shares.

### **Services and Processes**
- Use `sc` and PowerShell to manage services and monitor potential tampering.

### **Security Practices**
- **Registry Keys**:
  - `Run` and `RunOnce` keys are critical for persistence and should be audited regularly.
- **Windows Defender**:
  - Built-in antivirus with real-time protection and ransomware defenses.

### **Practical Applications**
- **Creating Secure Shares**:
  - Separate NTFS permissions from share permissions.
- **SIDs**:
  - Essential for identifying users and groups uniquely.
