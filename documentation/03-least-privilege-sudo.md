# Least-Privilege Sudo

## Objective

Implement role-based administrative access using sudo
while following the principle of least privilege.

## Security Design

TechNova users were divided into department-based groups.
Administrative permissions were assigned according to job
responsibilities rather than granting full root access.

## Sudo Policy

| Department | Administrative Access |
|---|---|
| Security | Read system logs using journalctl |
| Operations | Manage the cron service |
| Developers | No sudo access |
| Support | No sudo access |
| Standard users | No sudo access |

## Configuration

Sudo policies were configured using:

```text
/etc/sudoers.d/technova

# TechNova Systems - Least Privilege Sudo Policy

%technova_security ALL=(root) /usr/bin/journalctl

%technova_operations ALL=(root) /usr/bin/systemctl status cron.service
%technova_operations ALL=(root) /usr/bin/systemctl start cron.service
%technova_operations ALL=(root) /usr/bin/systemctl stop cron.service
%technova_operations ALL=(root) /usr/bin/systemctl restart cron.service
