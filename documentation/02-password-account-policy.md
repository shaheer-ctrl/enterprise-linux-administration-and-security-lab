# Password & Account Policy

## Objective

Implement password lifecycle and account management policies
for TechNova Systems users.

## Password Policy

The following password aging controls were configured:

| Policy | Value |
|---|---:|
| Maximum password age | 90 days |
| Warning period | 7 days |
| Inactive period | 30 days |
| Minimum password age | 0 days |
| Account expiration | Never |

## Tasks Performed

- Configured password expiration
- Configured password warning period
- Configured account inactivity period
- Tested account locking
- Tested account unlocking
- Tested account expiration
- Restored accounts to the required final state

Configuration Validation

The sudo configuration was validated using:
**sudo visudo -cf /etc/sudoers.d/technova
**
Result:
/etc/sudoers.d/technova: parsed OK

The main sudo configuration was also checked:
sudo visudo -c

### Access Verification

Effective privileges were reviewed for all TechNova users:
**sudo -l -U alice
sudo -l -U james
sudo -l -U peter**

### Least-Privilege Testing

Operations user james was able to manage the cron service:
**sudo -u james sudo /usr/bin/systemctl status cron.service
**
An unauthorized service-management attempt was denied:
**sudo -u james sudo /usr/bin/systemctl status ssh.service
**
The system returned a sudo permission-denied message.

### Security Result

Role-based sudo access was successfully implemented.

Users received only the administrative privileges required
for their assigned responsibilities, reducing unnecessary
root-level access.
