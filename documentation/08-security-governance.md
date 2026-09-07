# Security Governance

## 1. Objective

The objective of this phase was to establish and demonstrate basic security governance for the TechNova Systems Linux environment.

The governance process focuses on ensuring that user accounts, groups, administrative privileges, services, processes, system resources, and security logs are regularly reviewed and managed according to defined security requirements.

The goal is not only to configure the system securely, but also to establish a repeatable process for reviewing and maintaining that security posture.

---

## 2. Account Lifecycle Governance

TechNova requires a controlled lifecycle for all user accounts.

The account lifecycle consists of:

- Account creation
- Role and department assignment
- Authentication and password policy assignment
- Privilege assignment
- Periodic review
- Account locking when necessary
- Account expiration when appropriate
- Removal of inactive or unnecessary accounts

Each account should have a defined business purpose and should belong to the appropriate department or role.

When an employee changes department or responsibility, their group memberships and privileges should also be reviewed.

When an employee leaves the organization, the account should be disabled or removed according to the organization's account termination procedure.

---

## 3. User Account Audit

An account audit was performed to identify the users present on the system and verify their roles.

The environment contains the main administrative account together with eight TechNova employee accounts.

The employee accounts are distributed across four departments:

- Developers
- Operations
- Security
- Support

The audit confirmed that the TechNova accounts use dedicated user IDs and department-specific primary groups.

This provides a structured identity model instead of placing every employee into a single shared group.

### Observation

The account structure is suitable for demonstrating enterprise-style role separation in the lab environment.

---

## 4. Password and Account Expiration Governance

A password policy was applied to the TechNova employee accounts.

The implemented policy includes:

- Maximum password lifetime of 90 days
- Seven-day expiration warning period
- 30-day inactive period after password expiration
- No automatic account expiration unless specifically required

The policy encourages regular credential changes while preventing accounts from remaining indefinitely usable after becoming inactive.

### Observation

All eight TechNova employee accounts were reviewed and confirmed to have the expected password-aging configuration.

---

## 5. Account Locking and Inactive Accounts

Account locking is an important control when an account is suspected of compromise or temporarily needs to be disabled.

The lab included testing of account locking and unlocking to verify that account status can be controlled administratively.

Inactive accounts should be reviewed periodically.

Accounts that no longer have a legitimate business purpose should be disabled and eventually removed according to the organization's retention requirements.

### Security Benefit

This reduces the number of unnecessary active identities that could potentially be abused.

---

## 6. Group and Role Governance

Department-based groups were established for TechNova:

- `technova_developers`
- `technova_operations`
- `technova_security`
- `technova_support`

Primary group membership represents the employee's main department.

Secondary group membership provides additional role-based access where required.

For example, selected employees from Development and Operations were given secondary Security membership, while selected Security and Support personnel received additional Operations membership.

### Governance Principle

Group membership should be based on job responsibilities rather than convenience.

Additional group membership should be reviewed whenever an employee's responsibilities change.

---

## 7. Least-Privilege Governance

Administrative privileges were reviewed to ensure that TechNova users receive only the permissions required for their responsibilities.

The Security department was given controlled access to system journal information.

The Operations department was given controlled access to manage the Cron service.

Other users were not automatically granted administrative privileges.

### Observation

The final privilege model demonstrates role-based access control.

For example:

- Security personnel can perform approved log-review activities.
- Operations personnel can perform approved Cron service management.
- Users without an approved administrative requirement do not receive those privileges.

This is significantly safer than providing every employee with unrestricted administrative access.

---

## 8. Sudo Access Review

Administrative privilege assignments should be reviewed periodically.

The review should answer:

1. Who has administrative privileges?
2. Why do they need them?
3. What commands can they execute?
4. Are the privileges still required?
5. Can the permissions be reduced further?

The TechNova sudo policy was validated after implementation.

The configuration was also tested against users with different roles to verify that permitted actions were available while unauthorized actions were rejected.

### Result

The testing demonstrated that privilege boundaries were functioning as intended.

---

## 9. Service Governance

System services should be managed according to operational requirements.

For this lab, the Cron service was used as the primary example.

Its operational state was reviewed to confirm:

- The service is active
- The service starts automatically
- Administrative users can manage it according to their assigned permissions
- Unauthorized users cannot perform restricted service-management actions

The service was stopped, started, restarted, and its startup configuration was tested during the lab.

### Governance Principle

Production services should have defined owners, startup requirements, monitoring requirements, and change procedures.

---

## 10. Process and Resource Governance

Running processes and system resources should be periodically monitored to identify abnormal activity.

The lab reviewed:

- Running processes
- Process ownership
- CPU utilization
- Memory utilization
- Load averages
- Swap utilization
- Disk utilization
- Inode utilization
- Large files
- Resource-intensive processes

Controlled CPU activity was also generated during testing to demonstrate how resource utilization changes can be detected.

### Observation

The system returned to normal resource utilization after the test activity was terminated.

This demonstrates the importance of monitoring both normal and abnormal resource behavior.

---

## 11. Log Review Governance

System logs provide an important source of evidence for security and operational events.

The journal was reviewed for:

- Service activity
- Service failures
- Warnings
- Errors
- Administrative activity
- System startup events
- Current-boot events

The review identified several environment-specific warnings.

Some warnings were related to WSL2, virtualization, hardware emulation, time synchronization, or the lab environment rather than a direct TechNova security incident.

### Governance Principle

Log messages should be investigated based on their context and severity instead of assuming that every warning represents a security compromise.

---

## 12. Session and Authentication Review

User sessions and authentication-related information were reviewed as part of the governance process.

The review identified the currently active interactive session.

Failed-login records were also checked.

No failed-login records were returned during the review period.

This does not prove that failed authentication attempts have never occurred; it only indicates that none were present in the records examined during the audit.

---

## 13. Administrative Change Documentation

Security-sensitive administrative changes should be documented.

Examples include:

- Creating or removing accounts
- Changing group membership
- Changing password policies
- Modifying sudo permissions
- Starting or stopping important services
- Changing service startup behavior
- Investigating security-related log events

Documentation should record:

- What was changed
- Why it was changed
- Who performed the change
- When the change occurred
- What was tested afterward
- Whether the change was successful

This creates accountability and makes troubleshooting easier.

---

## 14. Periodic Security Audit Schedule

A repeatable review schedule should be established for the environment.

### Daily

Review:

- Critical system events
- Service failures
- High-severity log events
- Unexpected resource consumption

### Weekly

Review:

- User activity
- Authentication events
- Service status
- Resource utilization
- Important warnings and errors

### Monthly

Review:

- User accounts
- Group memberships
- Sudo privileges
- Password-aging policies
- Inactive accounts
- Enabled services
- Disk utilization

### Quarterly

Perform a broader security review covering:

- Account lifecycle
- Role assignments
- Least privilege
- Service configuration
- Logging
- Resource trends
- Governance procedures

---

## 15. Governance Findings

The following findings were identified during the project:

### Finding 1 — Role-Based Groups

Department-specific groups successfully separate TechNova employees according to organizational roles.

**Status:** Implemented

### Finding 2 — Password Aging

All TechNova accounts have a defined password-aging policy.

**Status:** Implemented

### Finding 3 — Least Privilege

Administrative privileges are restricted according to job responsibilities.

**Status:** Implemented

### Finding 4 — Service Governance

Cron service management was tested and restricted to authorized Operations personnel.

**Status:** Implemented

### Finding 5 — Logging

System and service logs were reviewed through journald.

**Status:** Implemented

### Finding 6 — Resource Monitoring

CPU, memory, storage, swap, inode usage, and processes were reviewed.

**Status:** Implemented

### Finding 7 — WSL2 Environment

Some warnings observed during the audit are specific to the WSL2/virtualized laboratory environment and should not automatically be treated as production Linux security findings.

**Status:** Documented

---

## 16. Governance Improvements

For a production implementation, TechNova should additionally consider:

- Centralized authentication
- Multi-factor authentication
- Centralized log collection
- Privileged access management
- Automated account deprovisioning
- Security alerting
- File-integrity monitoring
- Centralized configuration management
- Vulnerability management
- Formal change-management procedures
- Automated compliance checks
- Backup and recovery testing

These controls would extend the laboratory implementation toward a more realistic enterprise security environment.

---

## 17. Evidence

The following evidence was collected during the project:

- User and group audit results
- Password-aging configuration results
- Account lock/unlock testing
- Sudo privilege review
- Least-privilege testing
- Process inspection
- Resource monitoring results
- Service-management testing
- Journal and warning review
- Session and authentication review
- Governance audit results

Screenshots of these activities should be stored in the project's evidence directory.

---

## 18. Final Result

The TechNova Systems Linux environment now includes a basic security governance framework covering identity management, role separation, password policies, least privilege, service management, resource monitoring, logging, and periodic auditing.

The project demonstrates that Linux administration is not limited to running commands or configuring services. Effective administration also requires **controlled access, monitoring, documentation, auditing, and continuous review**.

This governance layer completes the security and administration objectives of the TechNova Systems laboratory.

**Overall Status: Successfully Implemented and Audited**
