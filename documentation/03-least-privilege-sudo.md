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

/etc/sudoers.d/technova

# TechNova Systems - Least Privilege Sudo Policy

%technova_security ALL=(root) /usr/bin/journalctl

%technova_operations ALL=(root) /usr/bin/systemctl status cron.service
%technova_operations ALL=(root) /usr/bin/systemctl start cron.service
%technova_operations ALL=(root) /usr/bin/systemctl stop cron.service
%technova_operations ALL=(root) /usr/bin/systemctl restart cron.service

### Configuration Validation

The sudo configuration was validated using:

**sudo visudo -cf /etc/sudoers.d/technova**

Validation result:
/etc/sudoers.d/technova: parsed OK

The main sudo configuration was also checked:

**sudo visudo -c**
### Access Verification

Effective sudo privileges were reviewed for TechNova users:

**sudo -l -U alice
sudo -l -U james
sudo -l -U peter**

### Least-Privilege Testing

Operations user james was able to manage the cron service:
**sudo -u james sudo /usr/bin/systemctl status cron.service**

An unauthorized service-management attempt was denied:
**sudo -u james sudo /usr/bin/systemctl status ssh.service**

The unauthorized request was denied by sudo.

### Result

Least-privilege access was successfully implemented using
department-based sudo rules.

Security users were given controlled log access, while
Operations users received controlled permissions to manage
the cron service.

Users outside the authorized groups were prevented from
performing these administrative actions.

The final sudo configuration was validated successfully
using visudo.

