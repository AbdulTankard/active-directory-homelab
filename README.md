# Active Directory Home Lab and Jira IT Help Desk Workflow

## Project Overview

This project demonstrates a simulated IT help desk environment using:

- Windows Server
- Active Directory Domain Services
- Windows client workstation
- Group Policy
- Shared folders and permissions
- Network troubleshooting
- Jira Service Management
- IT ticket documentation and resolution

The Jira ticket follows a realistic help desk workflow involving a user who cannot access an HR shared folder. The issue is investigated, tested, documented, and resolved using Active Directory permissions and Windows networking tools.

---

# Jira Service Management Setup

## 1. Jira Service Collection

I accessed the existing Atlassian site and began creating a Jira Service Management help desk environment.

![Jira service collection existing site setup](AD%20Documentation%20Github/01-jira-service-collection-existing-site-setup.png)

---

## 2. Selecting the IT Service Management Template

I selected the Basic IT Service Management template to create a service desk for receiving, tracking, investigating, and resolving technical support tickets.

![Select Basic IT Service Management template](AD%20Documentation%20Github/02-select-basic-it-service-management-template.png)

---

## 3. Reviewing the IT Service Management Template

I reviewed the template details before creating the project. This template provides queues, ticket workflows, request categories, and tools used by IT support teams.

![Basic IT Service Management template details](AD%20Documentation%20Github/03-basic-it-service-management-template-details.png)

---

## 4. Creating the IT Help Desk Space

I configured and created the IT Help Desk service project that would be used to document the Active Directory support issue.

![Create IT Help Desk space configuration](AD%20Documentation%20Github/04-create-it-help-desk-space-configuration.png)

---

# IT Help Desk Ticket Workflow

## Ticket: HR Shared Folder Access Issue

A support ticket was created after an HR employee reported that they could not access the HR shared folder from their workstation.

The ticket was documented and processed through the following stages:

1. Ticket received
2. Ticket assigned
3. Investigation started
4. Network connectivity tested
5. SMB access tested
6. Active Directory permissions verified
7. Shared drive mapped
8. Unauthorized access tested
9. Ticket resolved

---

## 5. Ticket Received in the Agent Queue

The ticket appeared in the Jira Service Management agent queue and was ready to be reviewed.

![ITHD-1 ticket received in agent queue](AD%20Documentation%20Github/07-ithd-1-ticket-received-in-agent-queue.png)

---

## 6. Ticket Assigned and Investigation Started

I assigned the ticket and moved it into the investigation stage. This indicates that an IT technician has taken ownership of the issue and begun troubleshooting.

![ITHD-1 assigned and investigation started](AD%20Documentation%20Github/08-ithd-1-assigned-and-investigation-started.png)

---

## 7. Client Connectivity and SMB Diagnostics

I performed network troubleshooting from the Windows client workstation.

The troubleshooting process included:

- Confirming connectivity to the domain controller
- Testing the domain controller IP address
- Confirming DNS resolution
- Testing access to the shared folder
- Confirming that SMB communication was functioning
- Verifying that TCP port 445 was available

These tests helped determine whether the issue was caused by networking, name resolution, SMB communication, or permissions.

![ITHD-1 client connectivity and SMB diagnostics](AD%20Documentation%20Github/09-ithd-1-client-connectivity-and-smb-diagnostics.png)

---

# Active Directory Investigation

## 8. HR User Access Verified

I reviewed the HR user account and verified that the user had the correct Active Directory group membership and permission to access the HR shared folder.

This step confirmed that authorized HR users were properly configured.

![ITHD-1 HR user access verified](AD%20Documentation%20Github/11-ithd-1-hr-user-access-verified.png)

---

## 9. HR Shared Drive Successfully Mapped

After confirming the permissions, I mapped the HR shared folder as a network drive on the client workstation.

The successful drive mapping confirmed that:

- The client could communicate with the server
- SMB file sharing was working
- The HR user had the correct permissions
- The shared folder path was correct

![ITHD-1 HR drive mapped](AD%20Documentation%20Github/12-ithd-1-hr-drive-mapped.png)

---

## 10. Unauthorized Sales User Denied Access

I tested the shared folder using a Sales department account.

The Sales user was denied access to the HR folder, confirming that the permissions followed the principle of least privilege.

Only approved HR users were allowed to access the HR department’s shared resources.

![ITHD-1 Sales user denied HR share](AD%20Documentation%20Github/13-ithd-1-sales-user-denied-hr-share.png)

---

# Ticket Resolution

## 11. Jira Ticket Resolved

After confirming that the HR user could access the shared drive and that unauthorized users were blocked, I documented the troubleshooting process and resolved the Jira ticket.

The resolution included:

- Confirming network connectivity
- Confirming SMB availability
- Verifying Active Directory group membership
- Confirming folder permissions
- Mapping the HR shared drive
- Testing access with an authorized HR user
- Testing denial with an unauthorized Sales user
- Documenting the final resolution in Jira

![Jira ticket resolved](AD%20Documentation%20Github/15-jira-ticket-resolved.png)

---

# Additional Active Directory Documentation

## Client Computer Verification

The Windows client computer was joined to the Active Directory domain and verified within the lab environment.

![Proof of computer](AD%20Documentation%20Github/Proof%20of%20computer.png)

---

## Client Moved to the Workstations Organizational Unit

The domain-joined client computer was moved into the Workstations Organizational Unit.

Using a dedicated Workstations OU allows administrators to apply workstation-specific Group Policies and keep Active Directory organized.

![Active Directory client moved to Workstations OU](AD%20Documentation%20Github/ad-client-moved-to-workstations.png)

---

# Troubleshooting Summary

The issue was resolved by following a structured IT troubleshooting process:

1. Identified the reported problem
2. Assigned and reviewed the support ticket
3. Confirmed client-to-server network connectivity
4. Verified DNS and SMB communication
5. Reviewed Active Directory user and group membership
6. Confirmed shared-folder and NTFS permissions
7. Mapped the network drive
8. Tested access with an authorized user
9. Tested access with an unauthorized user
10. Documented the solution
11. Resolved the Jira ticket

---

# Skills Demonstrated

- Active Directory administration
- User and group management
- Organizational Unit management
- Windows domain administration
- Shared-folder configuration
- NTFS and share permissions
- Principle of least privilege
- Network-drive mapping
- SMB troubleshooting
- TCP port 445 troubleshooting
- Windows client support
- Jira Service Management
- Ticket triage
- Incident investigation
- Technical documentation
- Issue resolution and closure

---

# Final Result

The authorized HR employee successfully accessed the HR shared drive, while the unauthorized Sales employee was correctly denied access.

The issue was fully documented and resolved through Jira Service Management, demonstrating an end-to-end IT help desk and Active Directory troubleshooting workflow.
