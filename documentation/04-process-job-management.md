# Process & Job Management

## Objective

The objective of this phase was to understand, monitor, and
manage Linux processes and shell jobs. The lab focused on
process identification, parent-child relationships, resource
usage, signal handling, foreground/background job control,
and persistent background execution.

---

## 1. Process Inspection

Linux processes were inspected using standard process-management
utilities.

### Process Listing

The following command was used to display processes sorted by
CPU utilization:

```bash
ps -eo pid,ppid,user,stat,%cpu,%mem,comm --sort=-%cpu | head -15
