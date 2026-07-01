# Active Directory Home Lab

## Project Overview

This repository documents a Windows Server and Active Directory home lab built to practice common help desk, desktop support, and junior system administration tasks.

The lab includes experience with:

- Active Directory Domain Services
- Domain-joined Windows clients
- User and computer account administration
- Organizational Units
- Security groups
- Password resets
- Shared folders and NTFS permissions
- Network drive mapping
- Group Policy
- Windows Defender Firewall
- SMB and TCP port 445 troubleshooting
- Jira Service Management ticket documentation

## Lab Environment

- **Domain Controller:** Windows Server
- **Client Machine:** Windows 10/11
- **Hypervisor:** VirtualBox
- **Domain Controller IP:** `192.168.56.10`
- **Client IP:** `192.168.56.20`
- **Primary Services:** Active Directory Domain Services, DNS, Group Policy, SMB file sharing, and Jira Service Management

## Skills Demonstrated

- Windows Server administration
- Active Directory Users and Computers
- Domain joins and computer accounts
- Organizational Unit management
- Domain user creation
- Security-group membership
- Password resets
- Password change at next logon
- Share and NTFS permissions
- Department-based access control
- Network drive mapping
- Group Policy creation and linking
- `gpupdate` and `gpresult`
- Windows Defender Firewall
- SMB and TCP port 445 troubleshooting
- ICMP and ping testing
- PowerShell network diagnostics
- Principle of least privilege
- Jira Service Management
- Ticket queues and assignment
- Incident investigation
- Troubleshooting documentation
- Resolution notes and ticket closure

## Useful Commands

```powershell
ipconfig /all
ping 192.168.56.10
nslookup server-name
whoami
whoami /groups
gpupdate /force
gpresult /r
Test-NetConnection 192.168.56.10 -Port 445
net use
net use H: \\SERVER\HR
net use S: \\SERVER\Sales
```

## What I Learned

This lab helped me understand how a Windows domain environment is organized, secured, supported, and documented. I practiced managing users, groups, computers, Organizational Units, passwords, network shares, NTFS permissions, mapped drives, Group Policy, and Windows Firewall rules.

I also practiced structured help desk work by documenting a shared-folder incident in Jira Service Management. I received and assigned the ticket, performed connectivity and SMB diagnostics, verified authorized and unauthorized access, mapped the network drive, documented the resolution, and closed the incident.

These tasks reflect common responsibilities performed by help desk technicians, service desk analysts, desktop support technicians, and junior Windows administrators.
