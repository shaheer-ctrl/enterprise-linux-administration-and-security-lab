# Resource Monitoring & Performance Analysis

## Objective

The objective of this phase was to monitor and analyze the
Linux system's CPU, memory, swap, disk, and overall resource
utilization.

Resource monitoring helps administrators identify performance
issues, resource exhaustion, unusual workloads, and potential
system bottlenecks.

---

## 1. CPU Analysis

The CPU architecture and available processing resources were
identified using:


lscpu | grep -E '^(CPU\(s\)|Model name|Thread|Core|Socket)'

#Observed Configuration

| Resource         | Value                        |
| ---------------- | ---------------------------- |
| Logical CPUs     | 8                            |
| CPU Cores        | 4                            |
| Threads per Core | 2                            |
| CPU Socket       | 1                            |
| CPU Model        | Intel Core i7-4770 @ 3.40GHz |

## 2. CPU Utilization

Real-time CPU utilization was monitored using:

top

The baseline system showed approximately:

CPU Idle: 100%

during periods of minimal workload.

## Observation

The system was under very low CPU load during the baseline
measurement. No persistent CPU-intensive processes were
observed.

A controlled CPU workload was also performed to observe how
CPU utilization changes under load.

After terminating the test workload, CPU utilization returned
to normal idle levels.

## 3. Load Average

System load was checked using:

uptime

Example observation:

**load average: 0.00, 0.00, 0.01**

The load average was also inspected directly:

cat /proc/loadavg

Example:

0.00 0.00 0.01 1/197 14195
Load Average Meaning

The three load values represent approximately:

Value	Period
First	1 minute
Second	5 minutes
Third	15 minutes

The observed values were extremely low compared with the
available 8 logical CPUs.

## Observation

The system was not experiencing CPU scheduling pressure during
the baseline measurement.

## 4. Memory Monitoring

Memory utilization was checked using:

free -h

The baseline showed approximately:

Total Memory:       7.7 GiB
Used Memory:        ~531 MiB
Available Memory:   ~7.2 GiB
Swap Used:          0 B
Swap Available:     2.0 GiB

Memory usage was also checked in megabytes:
free -m

## Observation

The system had a large amount of available memory and was not
experiencing memory pressure.

## 5. Swap Monitoring

Swap configuration was inspected using:

**swapon --show**

The system showed approximately:
NAME      TYPE       SIZE   USED
/dev/sdc  partition  2G     0B

## Observation

The swap area was available but unused during the monitoring
period.

Zero swap usage indicated that the system was not actively
swapping memory pages under the observed workload.

6. Disk Space Monitoring
Filesystem utilization was checked using:
**df -h**

The main Linux filesystem showed approximately:

Total:      1007G
Used:       ~1.6G
Available:  ~955G
Usage:      1%

## Observation 
The Linux filesystem had substantial free capacity and was not
close to storage exhaustion.

Windows-mounted filesystems were also visible inside WSL2.
These were treated separately from the primary Linux filesystem
for the Linux resource analysis.

## 7. Inode Monitoring

Filesystem inode utilization was checked using:
**df -i**

The main Linux filesystem showed approximately:

Total inodes:  67,108,864
Used:          ~45,112
Usage:         1%
## Observation

The filesystem had a very large number of available inodes.

No inode exhaustion condition was observed.

Monitoring inodes is important because a filesystem can run out
of inodes even when sufficient disk space remains available.

## 9. Large File Detection

Files larger than 100 MB were identified using:

**sudo find / -xdev -type f -size +100M \
-printf '%s %p\n' 2>/dev/null | sort -nr | head -20**

The largest detected file was approximately:
138567144 /usr/lib/x86_64-linux-gnu/libLLVM.so.21.1

This file is a system library and was not removed.

**Security & Administration Note
**Large files should not automatically be deleted.

Before removing a large file, an administrator should determine:

What the file is
Which package owns it
Whether it is actively required
Whether removing it could break the system

## 10. System Performance with vmstat

System performance was monitored using:
**vmstat 1 5
**
Important observations included:

r    0-1
b    0
swpd 0
si   0
so   0
wa   0
id   99-100

## Observation

The low r value indicated minimal CPU scheduling demand.
Both si and so remained at zero, indicating no active
swap-in or swap-out activity.

CPU idle time remained around 99–100%, and I/O wait remained
at zero.

Overall, the system showed no significant resource pressure
during the baseline monitoring period.

## Security & Administration Relevance

Resource monitoring is an important Linux administration and
security capability.

Regular monitoring can help identify:

CPU exhaustion
Memory pressure
Swap activity
Disk exhaustion
Inode exhaustion
Unexpected large files
Resource-intensive processes
I/O bottlenecks
Abnormal system behavior

From a security perspective, unusual resource consumption can
also be an indicator of unauthorized processes, malicious
activity, or compromised services.
