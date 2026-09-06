# systemd Service Management

## Objective

The objective of this phase was to understand and manage Linux
services using `systemd` and `systemctl`.

The lab focused on checking service status, starting and stopping
services, restarting services, enabling and disabling services at
boot, and reviewing service behavior through system logs.

---

## 1. Understanding systemd

`systemd` is the service and system manager responsible for
starting and managing services and other system components.

The systemd process was verified using:

```bash
ps -p 1 -o pid,comm,args

2. Checking Service Status

The cron service was selected as the example service for
testing.

Its status was checked using:

systemctl status cron

The service was found to be:

Active: active (running)

The service was also shown as enabled:

Loaded: loaded (...; enabled; ...)

Important information displayed by systemctl status included:

Service description
Loaded state
Active state
Main PID
Memory usage
CPU usage
Control group
Recent service logs
Observation

The cron service was running normally and was configured to
start automatically

