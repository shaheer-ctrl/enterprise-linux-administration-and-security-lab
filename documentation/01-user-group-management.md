# User & Group Management

## Objective

Implement department-based user and group management
for the TechNova Systems Linux environment.

## Departments

| Department | Linux Group |
|---|---|
| Developers | technova_developers |
| Operations | technova_operations |
| Security | technova_security |
| Support | technova_support |

## Users

| User | Department |
|---|---|
| alice | Developers |
| peter | Developers |
| james | Operations |
| samuel | Operations |
| charlie | Security |
| david | Security |
| anthony | Support |
| julia | Support |

## Tasks Performed

- Inspected `/etc/passwd`
- Inspected `/etc/group`
- Created department groups
- Created users
- Assigned primary groups
- Assigned secondary groups
- Verified UID/GID assignments
- Verified group membership

## Verification

User and group configuration was verified using:


id alice
id james
getent group technova_security

# User & Group Management

## Objective

Implement department-based user and group management for the TechNova Systems Linux environment to establish a foundational Role-Based Access Control (RBAC) architecture.

## Departments & Groups

Four enterprise-style groups were provisioned to represent the organizational structure:

| Department | Linux Group | GID |
|---|---|---|
| Developers | `technova_developers` | 1001 |
| Operations | `technova_operations` | 1002 |
| Security | `technova_security` | 1003 |
| Support | `technova_support` | 1004 |

## Users & Cross-Department Access

Eight standard employee accounts were provisioned within the `1001–1008` UID range. To simulate real-world cross-functional requirements, specific users were granted supplementary group access.

| User | Primary Department | Secondary Access |
|---|---|---|
| alice | Developers | Security |
| peter | Developers | *None* |
| james | Operations | Security |
| samuel | Operations | *None* |
| charlie | Security | Operations |
| david | Security | *None* |
| anthony | Support | Operations |
| julia | Support | *None* |

## Tasks Performed

- Inspected standard local account databases (`/etc/passwd`, `/etc/shadow`, `/etc/group`) to establish a baseline understanding of Linux identity management.
- Provisioned four dedicated departmental groups with custom GIDs.
- Provisioned eight user accounts with customized primary group assignments and home directories.
- Configured supplementary group memberships to allow cross-departmental resource access without modifying primary roles.
- Verified identity mappings and primary versus supplementary group visibility.

## Commands Used

### Group Creation

**sudo groupadd -g 1001 technova_developers
sudo groupadd -g 1002 technova_operations
sudo groupadd -g 1003 technova_security
sudo groupadd -g 1004 technova_support**

### User Provisioning

**sudo useradd -m -g technova_developers alice
sudo useradd -m -g technova_operations james**
****(Repeated for all 8 employees)
********
### Supplementary Group Assignment

**sudo usermod -aG technova_security alice
sudo usermod -aG technova_security james
sudo usermod -aG technova_operations charlie
sudo usermod -aG technova_operations anthony**

### Verification
User and group configurations were verified by querying the system's identity databases:

Verify user identity, UID, primary GID, and supplementary groups

**id alice
id james**

Verify department group configurations and supplementary members

**getent group technova_security
getent group technova_operations**

Result & Summary
The TechNova Systems organizational structure was successfully mapped to the Linux environment using native user and group management utilities. By explicitly defining primary groups based on departments and carefully assigning secondary groups for cross-functional tasks, a strict Role-Based Access Control (RBAC) foundation was established.

During verification, it was observed that users who belong to a group as their primary group do not populate in the supplementary member list of /etc/group for that specific group. This validated a core mechanical understanding of how Linux processes group ownership versus supplementary membership. This identity framework now provides the necessary structure to enforce least-privilege sudo policies and file permissions in subsequent configuration phases.
