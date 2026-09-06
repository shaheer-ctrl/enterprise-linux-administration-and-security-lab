# Enterprise Linux Administration & Security Lab

## TechNova Systems

A simulated enterprise Linux administration and security environment
designed to demonstrate practical Linux system administration,
access control, monitoring, service management, logging, and
security governance.

## Project Objectives

- Manage Linux users and groups
- Implement password and account lifecycle policies
- Apply least-privilege sudo access
- Monitor processes and system resources
- Manage systemd services
- Analyze system logs using journald
- Perform security and governance audits

## Environment

- OS: Ubuntu Linux
- Platform: WSL2
- Init System: systemd
- Shell: Bash
- Architecture: x86_64

## Project Workflow

User & Group Management
        ↓
Password & Account Policies
        ↓
Least-Privilege Sudo
        ↓
Process & Job Management
        ↓
Resource Monitoring
        ↓
Systemd Service Management
        ↓
Journald Logging
        ↓
Security Governance
        ↓
Final Security Audit

## Key Implementations

### User & Group Management

Created department-based groups:

- technova_developers
- technova_operations
- technova_security
- technova_support

Created and managed users with primary and secondary
group assignments.

### Password & Account Management

Implemented:

- Password expiration
- Password warning period
- Account inactivity policy
- Account lock/unlock
- Account expiration testing

Password policy:

- Maximum password age: 90 days
- Warning period: 7 days
- Inactive account period: 30 days

### Least-Privilege Sudo

Implemented role-based sudo permissions using:

`/etc/sudoers.d/technova`

Examples:

- Security → journal access
- Operations → controlled cron service management
- Support → restricted administrative access

Sudo configuration was validated using `visudo`.

### Process & Job Management

Demonstrated:

- ps
- top
- pgrep
- pidof
- pstree
- jobs
- fg
- bg
- nohup
- SIGTERM
- SIGKILL

### Resource Monitoring

Analyzed:

- CPU utilization
- Load average
- Memory usage
- Swap usage
- Disk utilization
- Inode usage
- Large files
- System performance using vmstat

### Systemd

Managed the cron service using:

- status
- start
- stop
- restart
- enable
- disable
- reload testing

### Logging

Analyzed system logs using:

- journalctl
- journalctl -u
- journalctl -b
- journalctl -xe

### Security Governance

Performed audits covering:

- User accounts
- Groups
- Password policies
- Sudo privileges
- Service status
- System warnings
- Active sessions
- Failed login records

## Results

The project demonstrates a structured approach to Linux
administration based on:

Access Control → Monitoring → Service Management → Logging → Auditing

## Disclaimer

This project was performed in a controlled WSL2 laboratory
environment for educational purposes.
