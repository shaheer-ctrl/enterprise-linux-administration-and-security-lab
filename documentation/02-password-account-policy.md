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

## Commands Used

```bash
sudo chage -M 90 -W 7 alice
sudo chage -I 30 alice
sudo chage -l alice
