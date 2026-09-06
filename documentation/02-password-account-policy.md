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

# Password & Account Policy

## Objective

Implement password lifecycle and account management policies for TechNova Systems users.

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

## Commands Used
### Password Aging Setup

sudo chage -M 90 -W 7 alice
sudo chage -I 30 alice
sudo chage -l alice

### Account Lock & Unlock
Account locking was tested using:

sudo passwd -l alice

sudo passwd -S alice

The account was then restored:

sudo passwd -u alice
sudo passwd -S alice

### Account Expiration Testing

Account expiration was temporarily configured for testing:

sudo chage -E 2026-12-31 julia
sudo chage -l julia

The expiration was then removed:

sudo chage -E -1 julia
### Verification
Password and account policies were verified using:

chage -l alice
chage -l julia

### Result

Password aging, account inactivity, locking, unlocking, and expiration controls were successfully implemented and validated. The successful application of these policies ensures that TechNova Systems adheres to standard identity and access management (IAM) best practices. By enforcing a 90-day password rotation and a 30-day inactivity lock, the system's attack surface regarding dormant accounts is significantly reduced. Furthermore, demonstrating the ability to manually lock and expire accounts proves readiness for routine administrative workflows such as employee offboarding and temporary contractor provisioning.
