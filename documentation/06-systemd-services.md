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

ps -p 1 -o pid,comm,args

## 2. Checking Service Status
The cron service was selected as the example service for
testing.

**Its status was checked using:
**
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
## Observation

The cron service was running normally and was configured to
start automatically

## 3. Checking Service State
The following commands were used to check the current state:

systemctl is-active cron

Result: **active**

The startup configuration was checked using:
systemctl is-enabled cron

Result: **enabled**

| Command                | Purpose                                                         |
| ---------------------- | --------------------------------------------------------------- |
| `systemctl is-active`  | Checks whether the service is currently running                 |
| `systemctl is-enabled` | Checks whether the service is configured to start automatically |

## 4. Stopping a Service
The cron service was stopped using:

**sudo systemctl stop cron
**
Its state was then verified:
**systemctl is-active cron
**
The service returned:
inactive
The status was also checked:

systemctl status cron

The service showed:
Active: inactive (dead)
## Observation

The service stopped successfully.

The systemd logs showed that the service received a termination
request and was deactivated successfully

## 5. Starting a Service
The stopped service was started again:
**sudo systemctl start cron
**
Its state was verified:

**systemctl is-active cron
**
Result: **active**

The complete status was reviewed:
systemctl status cron

The service was again shown as:
Active: active (running)
## Observation

The service successfully returned to its running state.

A new Main PID was assigned after the service was started,
which is normal because the previous process had already
terminated.

## 6. Restarting a Service

The service was restarted using:
****sudo systemctl restart cron
****
Its status was then checked:
systemctl status cron --no-pager

The service returned to:
Active: active (running)
## Observation

Restarting a service stops and starts the service again.

The Main PID changed after the restart, demonstrating that a
new service process was created.

## 7. Reloading a Service

A reload operation was tested:
**sudo systemctl reload cron
**
The command returned:

Failed to reload cron.service:
Job type reload is not applicable for unit cron.service.
## Observation

This was an expected result for the selected cron unit.

The service does not provide a systemd reload operation, so
systemd correctly rejected the request.

This demonstrates an important administration concept:

Not every systemd service supports reload.

A reload should only be used when the service supports
reloading its configuration without completely restarting

## 8. Enable and Disable Services

The startup configuration of cron was tested.

First, the service was checked:

systemctl is-enabled cron

Result: **enabled**

The service was then disabled:
**sudo systemctl disable cron
**
The configuration was verified:
**systemctl is-enabled cron
Result: **disabled**

The service was then enabled again:
**sudo systemctl enable cron
**
Final verification:
**systemctl is-enabled cron
**
Result: **enabled**

The final runtime state was also checked:

systemctl is-active cron

Result: **active**
## Observation

The service was successfully restored to its original
configuration.

The final state was:

Service: cron
Runtime: active
Startup: enabled

## 9. Service Logs

Service-specific logs were reviewed using journalctl.

The recent cron logs were displayed using:
**sudo journalctl -u cron --no-pager -n 30
**
Logs from the current day were reviewed using:
**sudo journalctl -u cron --since today --no-pager**

These logs showed service lifecycle events including:

Stopping cron.service...
cron.service: Deactivated successfully.
Stopped cron.service...
Started cron.service...
## Observation

The journal provided a timeline of service activity and was
useful for verifying whether start, stop, and restart operations
were successful.

## 10. Service Configuration Warning

During service startup, the journal contained the following
warning:

cron.service: Referenced but unset environment variable
evaluates to an empty string: EXTRA_OPTS

Despite this warning, the service successfully started and
remained active.

The cron process also reported:

**(CRON) INFO (pidfile fd = 3)
(CRON) INFO (Skipping @reboot jobs -- not system startup)******
## Observation

The EXTRA_OPTS message was identified as a configuration
warning rather than a service failure.

The service remained operational after startup.

This demonstrates why administrators should review logs instead
of assuming that every warning means a service has failed.
