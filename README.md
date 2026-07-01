# Active Directory Home Lab and Jira IT Help Desk Workflow

## Project Overview

This project demonstrates the creation and administration of a Windows Active Directory home lab combined with a realistic Jira Service Management help desk workflow.

The lab documents how I:

- Installed and configured Active Directory Domain Services
- Joined a Windows client computer to the domain
- Organized users and computers with Organizational Units
- Created test users and security groups
- Configured shared folders and NTFS permissions
- Mapped network drives
- Tested authorized and unauthorized access
- Reset user passwords
- Created and tested Group Policy
- Diagnosed SMB connectivity using TCP port 445
- Created and resolved an IT support ticket in Jira Service Management
- Documented troubleshooting steps and the final resolution

---

# Lab Environment

The environment included:

- Windows Server
- Active Directory Domain Services
- Windows client workstation
- VirtualBox networking
- DNS
- Group Policy Management
- Windows Defender Firewall
- SMB file sharing
- Jira Service Management

---

# 1. Domain Client and Active Directory Structure

## 1.1 Domain-Joined Computer Verification

The Windows client computer was successfully joined to the Active Directory domain.

This confirms that the client could communicate with the domain controller, locate the domain through DNS, and authenticate against Active Directory.

![Proof of domain-joined computer](AD%20Documentation%20Github/Proof%20of%20computer.png)

---

## 1.2 Client Computer Moved to the Workstations OU

The domain-joined client computer was moved into the Workstations Organizational Unit.

Using a dedicated Workstations OU helps administrators organize computers and apply workstation-specific Group Policies.

![Active Directory client moved to Workstations OU](AD%20Documentation%20Github/ad-client-moved-to-workstations.png)

---

## 1.3 Active Directory Organizational Unit Structure

Organizational Units were created to separate users, computers, and departments.

This structure makes Active Directory easier to manage and allows administrators to target Group Policies and permissions to specific departments.

![Active Directory OU structure](AD%20Documentation%20Github/ad-ou-structure.png)

---

## 1.4 Test Users Created

Test user accounts were created to simulate employees working in different departments.

These accounts were later used to test authentication, group membership, shared-folder permissions, and Group Policy.

![Active Directory test users created](AD%20Documentation%20Github/test-users-created.png)

---

## 1.5 User Group Membership Configured

Users were added to the appropriate Active Directory security groups.

Security groups allow permissions to be assigned by job role or department rather than individually assigning permissions to every employee.

![Active Directory user group membership](AD%20Documentation%20Github/ad-user-group-membership.png)

---

# 2. Shared Folders and Access Permissions

## 2.1 Sales Folder NTFS Permissions

NTFS permissions were configured on the Sales department folder.

The permissions were designed to allow approved Sales users to access the folder while preventing unauthorized users from opening it.

![Sales folder NTFS permissions](AD%20Documentation%20Github/sales-folders-ntfs-permissions.png)

---

## 2.2 Shared Folders Accessed from the Client

The client workstation connected to the server and displayed the available network shares.

This confirmed that:

- The client could communicate with the server
- DNS resolution was functioning
- SMB file sharing was available
- The server share path was reachable

![Client accessing network shares](AD%20Documentation%20Github/client-access-shares.png)

---

## 2.3 Diagnosing the Shared-Folder Problem

The shared-folder path was investigated after the client experienced difficulty locating or opening the folder.

This troubleshooting step helped identify whether the problem involved the network path, DNS, SMB connectivity, drive mapping, or permissions.

![Diagnosing problem with finding folder](AD%20Documentation%20Github/diagnosing-problem-with-finding%20-folder.png)

---

## 2.4 Sales Drive Mapped on the Client

The Sales shared folder was successfully mapped as a network drive on the Windows client.

Mapping the drive gives the user a consistent drive letter and provides easier access to department resources.

![Client mapped Sales drive](AD%20Documentation%20Github/client-mapped-sales-drive.png)

---

## 2.5 Authorized Sales User Access Verified

An authorized Sales user successfully accessed the Sales folder.

This confirmed that the Active Directory group membership, share permissions, and NTFS permissions were working correctly.

![Sales user authorized folder access](AD%20Documentation%20Github/sales-user-authorized-folder-access.png)

---

## 2.6 HR User Denied Access to the Sales Folder

An HR account attempted to access the Sales folder and was denied.

This confirmed that the permissions followed the principle of least privilege by limiting access to approved Sales users.

![HR user denied Sales folder access](AD%20Documentation%20Github/hr-user-denied-sales-folder.png)

---

# 3. Active Directory Password Reset

## 3.1 User Password Reset

A user password was reset through Active Directory Users and Computers.

The account was configured to require the user to change the temporary password during the next sign-in.

![Active Directory password reset](AD%20Documentation%20Github/ad-password-reset-change-required.png)

---

## 3.2 User Must Change Password at Next Logon

The **User must change password at next logon** option was enabled.

This is a common help desk security practice because the technician does not continue controlling the employee’s permanent password.

![Password must change at next logon](AD%20Documentation%20Github/ad-password-reset-must-change-next-logon.png.png)

---

# 4. Group Policy Configuration and Testing

## 4.1 Sales Control Panel Restriction Configured

A Group Policy Object was configured to prevent Sales users from accessing the Windows Control Panel.

This demonstrates how administrators can centrally control workstation settings for specific departments.

![Sales Control Panel restriction configured](AD%20Documentation%20Github/gpo-sales-block-control-panel-configured.png)

---

## 4.2 Group Policy Verified with GPResult

The `gpresult` command was used on the client to confirm that the Sales Group Policy was applied to the signed-in user.

This command helps administrators determine which user and computer policies are currently active.

![Sales Group Policy applied through GPResult](AD%20Documentation%20Github/gpo-sales-applied-gpresult.png)

---

## 4.3 Control Panel Successfully Blocked

The Sales user attempted to open Control Panel and received a restriction message.

This confirmed that the Group Policy was successfully applied and enforced.

![Sales Control Panel blocked](AD%20Documentation%20Github/gpo-sales-control-panel-blocked.png)

---

# 5. SMB and TCP Port 445 Troubleshooting

## 5.1 TCP Port 445 Confirmed Open

TCP port 445 was tested before making any firewall changes.

Port 445 is used by SMB for Windows file sharing, mapped drives, and access to shared folders.

![TCP port 445 open before firewall block](AD%20Documentation%20Github/port-445-open-before-firewall-block.png)

---

## 5.2 Firewall Rule Created to Block Port 445

A Windows Defender Firewall rule was created to block TCP port 445.

This simulated an SMB connectivity problem that an IT support technician may encounter.

![Firewall rule blocking TCP port 445](AD%20Documentation%20Github/block-port-445-rule.png)

---

## 5.3 TCP Port 445 Blocked on the Client

After the firewall rule was applied, the client could no longer successfully communicate with the server over TCP port 445.

This demonstrated how a firewall rule can prevent shared-folder access even when the server is otherwise reachable.

![TCP port 445 blocked on client](AD%20Documentation%20Github/port-445-blocked-in-client.png)

---

## 5.4 Ping Still Worked While SMB Was Blocked

The client could still ping the server while TCP port 445 was blocked.

This demonstrated that a successful ping does not prove that every network service is working.

Ping uses ICMP, while Windows file sharing uses SMB over TCP port 445.

![Port 445 blocked while ping still works](AD%20Documentation%20Github/port-445-blocked-ping-still-works.png)

---

## 5.5 Port 445 Firewall Rule Removed

The firewall rule blocking TCP port 445 was removed as part of the troubleshooting and restoration process.

![Firewall port 445 rule removed](AD%20Documentation%20Github/firewall-445-removed.png)

---

## 5.6 SMB Connectivity Restored

TCP port 445 was tested again after removing the firewall rule.

The successful test confirmed that SMB communication and access to the shared folders had been restored.

![TCP port 445 restored](AD%20Documentation%20Github/port-445-restored.png)

---

# 6. Jira Service Management Setup

## 6.1 Existing Atlassian Site Selected

The existing Atlassian site was selected as the location for the Jira Service Management project.

![Jira Service Collection existing site setup](AD%20Documentation%20Github/01-jira-service-collection-existing-site-setup.png)

---

## 6.2 Basic IT Service Management Template Selected

The Basic IT Service Management template was selected.

This template provides tools for receiving, assigning, investigating, documenting, and resolving IT support requests.

![Basic IT Service Management template selected](AD%20Documentation%20Github/02-select-basic-it-service-management-template.png)

---

## 6.3 Template Details Reviewed

The details of the Basic IT Service Management template were reviewed before creating the project.

The template includes request queues, ticket statuses, workflows, and service management tools.

![Basic IT Service Management template details](AD%20Documentation%20Github/03-basic-it-service-management-template-details.png)

---

## 6.4 IT Help Desk Space Created

The IT Help Desk project was configured and created.

This project was used to document the Active Directory shared-folder support issue from the initial report through final resolution.

![IT Help Desk space configuration](AD%20Documentation%20Github/04-create-it-help-desk-space-configuration.png)

---

# 7. Jira IT Help Desk Ticket Workflow

## Ticket Scenario

An employee reported that they could not access an HR shared folder from their Windows workstation.

The ticket was processed through the following workflow:

1. Ticket received
2. Ticket assigned
3. Investigation started
4. Client connectivity tested
5. SMB communication tested
6. Active Directory access verified
7. Network drive mapped
8. Unauthorized access tested
9. Troubleshooting documented
10. Ticket resolved

---

## 7.1 Ticket Received in the Agent Queue

The support request appeared in the Jira Service Management agent queue.

The queue allows support technicians to review incoming incidents and determine their priority, assignment, and current status.

![ITHD-1 ticket received in agent queue](AD%20Documentation%20Github/07-ithd-1-ticket-received-in-agent-queue.png)

---

## 7.2 Ticket Assigned and Investigation Started

The ticket was assigned, and its status was moved into the investigation stage.

Assigning the ticket establishes ownership and shows that a technician is actively troubleshooting the problem.

![ITHD-1 assigned and investigation started](AD%20Documentation%20Github/08-ithd-1-assigned-and-investigation-started.png)

---

## 7.3 Client Connectivity and SMB Diagnostics

Network diagnostics were performed from the client workstation.

The investigation included:

- Testing connectivity to the domain controller
- Confirming the server IP address
- Checking DNS resolution
- Testing the shared-folder path
- Testing SMB connectivity
- Checking TCP port 445
- Separating network problems from permission problems

![ITHD-1 client connectivity and SMB diagnostics](AD%20Documentation%20Github/09-ithd-1-client-connectivity-and-smb-diagnostics.png)

---

## 7.4 HR User Access Verified

The HR user account, group membership, and shared-folder permissions were reviewed.

This confirmed that the authorized HR employee had the correct access rights.

![ITHD-1 HR user access verified](AD%20Documentation%20Github/11-ithd-1-hr-user-access-verified.png)

---

## 7.5 HR Shared Drive Successfully Mapped

The HR shared folder was successfully mapped as a network drive on the client workstation.

The successful drive mapping confirmed that:

- The client could reach the server
- The shared-folder path was correct
- SMB was functioning
- The HR user was properly authorized
- The share and NTFS permissions were working

![ITHD-1 HR drive successfully mapped](AD%20Documentation%20Github/12-ithd-1-hr-drive-mapped.png)

---

## 7.6 Unauthorized Sales User Denied Access

A Sales department user attempted to access the HR shared folder and was denied.

This test confirmed that only authorized HR users could access the department’s resources.

![ITHD-1 Sales user denied HR share](AD%20Documentation%20Github/13-ithd-1-sales-user-denied-hr-share.png)

---

## 7.7 Jira Ticket Resolved

After the HR user’s access was restored and unauthorized access was tested, the troubleshooting steps and final resolution were documented in Jira.

The ticket was then marked as resolved.

![Jira ticket resolved](AD%20Documentation%20Github/15-jira-ticket-resolved.png)

---

# Troubleshooting Process

The issue was resolved using a structured troubleshooting process:

1. Identified the user’s reported problem
2. Reviewed and assigned the Jira ticket
3. Confirmed client-to-server connectivity
4. Verified DNS resolution
5. Tested the shared-folder path
6. Tested SMB communication over TCP port 445
7. Reviewed Active Directory user and group membership
8. Checked share and NTFS permissions
9. Mapped the network drive
10. Tested access with an authorized user
11. Tested access with an unauthorized user
12. Documented the troubleshooting process
13. Confirmed the final resolution
14. Closed the Jira ticket

---

# Security Principles Demonstrated

## Principle of Least Privilege

Users were only granted access to resources required for their department.

- Sales users could access the Sales folder
- HR users could access the HR folder
- HR users were denied access to the Sales folder
- Sales users were denied access to the HR folder

## Group-Based Access Control

Permissions were assigned using Active Directory security groups instead of configuring every user individually.

## Temporary Password Security

Users were required to change temporary passwords during their next sign-in.

## Centralized Policy Management

Group Policy was used to centrally control Windows settings for department users.

## Firewall and Service Troubleshooting

TCP port testing was used to identify the difference between basic network connectivity and application-specific connectivity.

---

# Skills Demonstrated

- Active Directory Domain Services
- Windows Server administration
- Active Directory Users and Computers
- User-account creation
- Password resets
- Security-group management
- Organizational Unit management
- Domain joining
- DNS troubleshooting
- Group Policy creation
- Group Policy verification
- `gpupdate`
- `gpresult`
- Shared-folder configuration
- Share permissions
- NTFS permissions
- Network-drive mapping
- Principle of least privilege
- SMB troubleshooting
- TCP port 445 testing
- Windows Defender Firewall
- Ping and ICMP testing
- Windows client support
- Jira Service Management
- Ticket assignment
- Ticket triage
- Incident investigation
- Troubleshooting documentation
- Ticket resolution and closure

---

# Final Results

The Active Directory environment was successfully configured and tested.

The project confirmed that:

- The Windows client was joined to the domain
- Users and computers were organized in Active Directory
- Test users and department security groups were created
- Shared folders were accessible to authorized users
- Unauthorized users were denied access
- Network drives were successfully mapped
- Password resets were completed securely
- Group Policy was successfully applied
- SMB problems were simulated and resolved
- TCP port 445 connectivity was restored
- The support issue was documented and resolved through Jira Service Management

This project demonstrates an end-to-end IT support workflow involving Active Directory administration, Windows troubleshooting, access control, networking, security, and help desk ticket management.
