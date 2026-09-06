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

```bash
id alice
id james
getent group technova_security
