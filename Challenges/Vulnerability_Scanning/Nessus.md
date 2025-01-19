# HTB Challenge - Nessus Skills Assessment

## Description
You have been contracted by Inlanefreight to perform a basic internal vulnerability assessment on a Windows Server development host. The goal is to identify significant vulnerabilities using Nessus and provide a report that can justify additional funding for more comprehensive penetration tests.

---

## Target Information
- **IP Address**: `172.16.16.100`
- **Server Type**: Windows Server (Development environment)

---

## Steps Performed

### 0. SSH to the academy acount 
- **SSH Connection**: 
   - ID : `ssh htb-student@10.129.202.116`
   - Password : `HTB_@cademy_student!`

### 1. Nessus Configuration
- **Access Nessus**:
  - URL: `https://<IP>:8834` (https://10.129.202.116:8834 here)
  - Credentials: `htb-student:HTB_@cademy_student!`

- **Basic Network Scan**:
  - Create new template `Basic Network Scan`.
  - SSH *Credentials* authentication configured with:
    - Username: `administrator`
    - Password: `Academy_VA_adm1!`
  - Setup `172.16.16.100` as *Targets*
  - Setup `Port scan (all ports)` in *Discovery*
  - Save it, select it and launch it


- **Setup Notes**:
  - Allowed up to **60 minutes** for scan completion.
  - Ensured the target instance (`172.16.16.100`) was spawned before starting the scan.

---

## Results and Findings

### a. SMB Share
- **Accessible Share Name**: `wsus`

### b. Target Information
- **Authenticated Scan Target**: `172.16.16.100`

### c. Critical Vulnerabilities
- **Highest Criticality Plugin ID**: `156032`

---

## Lessons Learned
1. **Importance of Authentication**:
   - Adding valid credentials provided deeper insights into the system's vulnerabilities.

2. **VNC Server Vulnerability**:
   - Exposed unauthenticated access on port 5900, posing a significant risk for attackers.

3. **SMB Shares**:
   - Identified accessible share `wsus`, which could expose sensitive data or configurations.

4. **Nessus Configuration**:
   - Adjusting scan templates (e.g., all ports) and providing authentication enhances the depth of results.

---

## Tools Used
- **Nessus**:
  - Performed network vulnerability assessment.
- **SSH**:
  - Configured Nessus on the target VM when necessary.

---

## Recommendations
1. **Secure VNC Server**:
   - Require authentication for access.
   - Disable if not in use.

2. **Restrict SMB Shares**:
   - Limit access to `wsus` to authorized users only.
   - Review permissions to prevent unintended exposure.

3. **Perform Full-Scale Penetration Testing**:
   - Allocate budget for comprehensive testing to uncover additional vulnerabilities.

---

## Notes
- **Plugin ID 156032** highlights a critical vulnerability that should be addressed immediately.
- Using authenticated scans significantly increases the value of results compared to unauthenticated scans.
- Time management is key when running long Nessus scans, especially in lab environments.

---

## Questions and Answers

| Question                                    | Answer                         |
|---------------------------------------------|--------------------------------|
| SMB Share Name                              | `wsus`                         |
| Target for the authenticated scan           | `172.16.16.100`                |
| Plugin ID of highest criticality            | `156032`                        |
| Name of vulnerability for Plugin ID 26925   | `VNC Server Unauthenticated Access` |
| Port of the VNC Server                      | `5900`                         |

---

**Challenge Status**: Completed ✅

