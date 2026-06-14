# Active Directory Home Lab

## Lab Goal
The goal of this lab is to practice Windows Server, Active Directory, domain joins, users, groups, shared folders, Group Policy, ports, remote logins, and basic network troubleshooting.

## Lab Environment
- **Domain Controller:** Windows Server
- **Client Machine:** Windows 10/11
- **Hypervisor:** VirtualBox
- **Domain Name:** 
- **Network Type:** 
- **Admin Account:** 

## Skills Practiced
- Installed and configured a Windows Server domain controller
- Joined a Windows client to a domain
- Verified the client inside Active Directory
- Created Organizational Units
- Created test domain users
- Created groups
- Practiced shared folder access
- Planned Group Policy testing
- Practiced basic networking commands
- Planned remote access testing with RDP, SSH, VNC, ports, and port forwarding

## Lab Notes

### 1. Domain Join

**What I did:**  
I joined a Windows client machine to my Active Directory domain.

**Why this matters:**  
Joining a computer to a domain allows centralized login, management, and security through Active Directory.

**Tools/commands used:**

```powershell
sysdm.cpl
ipconfig /all
whoami
