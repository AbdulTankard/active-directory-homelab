````markdown
---

# New Lab Documentation

This section documents the newer Active Directory, Group Policy, password reset, folder-access, drive-mapping, and Jira Service Management work completed in the lab.

---

# 8. Jira Service Management Help Desk Setup

## Existing Jira Site Selected

![Existing Jira Site Selected](screenshots/01-jira-service-collection-existing-site-setup.png)

I began the Jira Service Management setup by selecting my existing Jira site. This allowed me to add an IT service project without creating a separate Jira environment.

This step established the platform that I would use to document help desk tickets associated with my Active Directory lab.

---

## Basic IT Service Management Template Selected

![Basic IT Service Management Template Selected](screenshots/02-select-basic-it-service-management-template.png)

I selected the Basic IT Service Management template for the project.

This template includes features commonly used by service desk teams, including:

- Incident tracking
- User requests
- Ticket queues
- Ticket assignment
- Status tracking
- Resolution documentation
- Ticket closure

---

## IT Service Management Template Reviewed

![IT Service Management Template Reviewed](screenshots/03-basic-it-service-management-template-details.png)

Before creating the project, I reviewed the details of the Basic IT Service Management template.

This helped me understand the available workflows and confirmed that the template would support the help desk scenarios performed in the lab.

---

## IT Help Desk Project Configured

![IT Help Desk Project Configured](screenshots/04-create-it-help-desk-space-configuration.png)

I configured the Jira project as an IT Help Desk service project.

The project was created to simulate a professional service desk environment where technical incidents are reported, assigned, investigated, resolved, and documented.

---

# 9. Jira Ticket Investigation

## Ticket Received in the Agent Queue

![Ticket Received in Agent Queue](screenshots/07-ithd-1-ticket-received-in-agent-queue.png)

The help desk ticket appeared in the agent queue as ticket `ITHD-1`.

The reported issue involved a user experiencing difficulty accessing a department network share.

At this stage, I reviewed the issue description, priority, current status, and available ticket information before beginning troubleshooting.

---

## Ticket Assigned and Investigation Started

![Ticket Assigned and Investigation Started](screenshots/08-ithd-1-assigned-and-investigation-started.png)

I assigned the ticket to myself and moved it into an active investigation status.

Assigning the ticket establishes ownership and lets other technicians know that the issue is currently being handled.

---

## Client Connectivity and SMB Diagnostics Performed

![Client Connectivity and SMB Diagnostics](screenshots/09-ithd-1-client-connectivity-and-smb-diagnostics.png)

I performed network and SMB diagnostics from the Windows client.

The troubleshooting process included:

- Confirming that the client could communicate with the domain controller
- Testing the server IP address
- Checking the shared-folder path
- Verifying SMB connectivity
- Testing TCP port 445
- Confirming that Windows Firewall was not blocking required traffic
- Reviewing the signed-in user's permissions and group membership

SMB uses TCP port 445 for Windows file and folder sharing.

---

## HR User Access Verified

![HR User Access Verified](screenshots/11-ithd-1-hr-user-access-verified.png)

I signed in using an authorized HR domain account and successfully accessed the HR network share.

This verified that the following components were functioning correctly:

- Domain authentication
- HR security-group membership
- Share permissions
- NTFS permissions
- SMB communication
- Server connectivity

---

## HR Network Drive Mapped

![HR Network Drive Mapped](screenshots/12-ithd-1-hr-drive-mapped.png)

I successfully mapped the HR network share as a drive on the Windows client.

Mapping a drive provides users with a consistent drive letter and allows them to access a shared resource without manually entering the full UNC path each time.

Example UNC path:

```text
\\SERVER\HR
````

Example drive-mapping command:

```powershell
net use H: \\SERVER\HR
```

---

## Sales User Denied Access to HR Share

![Sales User Denied HR Share](screenshots/13-ithd-1-sales-user-denied-hr-share.png)

I tested the HR share using a Sales domain account.

The Sales user was denied access because the account was not a member of the authorized HR security group.

This successful denial confirmed that department-based access restrictions were working correctly and that unauthorized users could not access HR resources.

---

## Jira Ticket Resolved

![Jira Ticket Resolved](screenshots/15-jira-ticket-resolved.png)

After confirming that the HR user could access the share and that the Sales user was correctly denied access, I documented the resolution and marked the ticket as resolved.

The resolution included:

* The reported problem
* Initial investigation
* Connectivity testing
* SMB and port 445 testing
* User group verification
* Share and NTFS permission verification
* Successful HR access
* Successful HR drive mapping
* Unauthorized Sales access denial
* Final ticket closure

This completed the full ticket lifecycle from intake through resolution.

---

# 10. Active Directory Password Reset

## User Password Reset Performed

![User Password Reset](screenshots/ad-password-reset-change-required.png)

I reset a domain user's password through Active Directory Users and Computers.

Password resets are a common help desk responsibility when a user forgets a password, becomes locked out, or requires a temporary credential.

During the reset, I assigned a temporary password and prepared the account so the user could create a private password at the next sign-in.

---

## Password Change Required at Next Logon

![Password Change Required at Next Logon](screenshots/ad-password-reset-must-change-next-logon.png.png)

I enabled the option requiring the user to change the temporary password at the next logon.

This improves security because the temporary password created by the administrator is used only once. After signing in, the user must create a password known only to them.

---

# 11. Department Network Drive Mapping

## Sales Drive Mapped on Client

![Sales Drive Mapped on Client](screenshots/client-mapped-sales-drive.png)

I mapped the Sales network share as a drive on the domain-joined Windows client.

This confirmed that:

* The client could communicate with the file server
* The Sales shared folder was available
* The Sales user had the required permissions
* SMB traffic was functioning
* The drive-mapping process worked correctly

Example command:

```powershell
net use S: \\SERVER\Sales
```

---

# 12. Department Folder Access Testing

## Authorized Sales User Access Confirmed

![Authorized Sales User Access](screenshots/sales-user-authorized-folder-access.png)

I signed in using an authorized Sales account and confirmed that the user could open the Sales shared folder.

This proved that the Sales security group had the correct share and NTFS permissions.

The test confirmed that legitimate users could access the department resource as intended.

---

## HR User Denied Access to Sales Folder

![HR User Denied Sales Folder](screenshots/hr-user-denied-sales-folder.png)

I signed in using an HR account and attempted to access the Sales shared folder.

The HR user received an access-denied message because the account was not a member of the Sales security group.

This demonstrated the principle of least privilege, which means users receive access only to the resources required for their responsibilities.

---

# 13. Sales Group Policy Configuration

## Control Panel Restriction GPO Configured

![Control Panel Restriction GPO Configured](screenshots/gpo-sales-block-control-panel-configured.png)

I created and configured a Group Policy Object that prevents Sales users from opening Control Panel and Windows Settings.

The policy was linked to the appropriate Organizational Unit so it would target only the intended department users.

This demonstrated centralized user configuration through Active Directory Group Policy.

---

## Sales GPO Verified with GPResult

![Sales GPO Verified with GPResult](screenshots/gpo-sales-applied-gpresult.png)

I used the `gpresult` command to confirm that the Group Policy Object was applied to the Sales user.

```powershell
gpresult /r
```

The command displays information about the policies applied to the current user and computer.

This verification helped confirm that:

* The user was located in the correct OU
* The GPO was linked correctly
* Group Policy processing completed
* The restriction was applied to the intended account

---

## Control Panel Successfully Blocked

![Control Panel Successfully Blocked](screenshots/gpo-sales-control-panel-blocked.png)

I attempted to open Control Panel while signed in as the Sales user.

Windows displayed a restriction message, confirming that the Group Policy setting worked correctly.

This completed the GPO testing process from policy creation through end-user verification.

---

# 14. Updated Skills Demonstrated

The additional lab work demonstrates experience with:

* Jira Service Management
* IT service desk ticket queues
* Ticket assignment
* Incident investigation
* Troubleshooting notes
* Resolution documentation
* Ticket closure
* Active Directory password resets
* Temporary password administration
* Password change at next logon
* Department security groups
* Network share access
* Unauthorized-access testing
* Share permissions
* NTFS permissions
* Network drive mapping
* UNC paths
* Group Policy creation
* Group Policy linking
* Organizational Unit targeting
* `gpupdate`
* `gpresult`
* Control Panel restrictions
* Windows Settings restrictions
* SMB troubleshooting
* TCP port 445 testing
* Principle of least privilege
* Access-control verification

---

# 15. Additional Commands Used

```powershell
whoami
whoami /groups
ipconfig /all
ping 192.168.56.10
Test-NetConnection 192.168.56.10 -Port 445
gpupdate /force
gpresult /r
net use
net use H: \\SERVER\HR
net use S: \\SERVER\Sales
```

---

# 16. Updated Project Summary

The newer portion of this lab expanded the environment beyond basic Active Directory configuration.

I practiced resetting a domain user's password, requiring a password change at the next sign-in, mapping department network drives, confirming authorized folder access, and verifying that unauthorized department users were denied access.

I also created a Sales Group Policy that blocked Control Panel and Windows Settings. I verified the policy using `gpresult` and tested the restriction from the user account.

Finally, I documented a shared-folder issue inside Jira Service Management. I received the ticket, assigned it, investigated connectivity and SMB access, verified user permissions, mapped the network drive, tested authorized and unauthorized access, documented the resolution, and closed the ticket.

These tasks reflect common responsibilities performed by help desk technicians, service desk analysts, desktop support technicians, and junior Windows administrators.

```
```
