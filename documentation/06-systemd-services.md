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

