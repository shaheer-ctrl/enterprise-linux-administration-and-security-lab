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


ps -eo pid,ppid,user,stat,%cpu,%mem,comm --sort=-%cpu | head -15

## Real-Time Monitoring

The top command was used to monitor processes and system
resources in real time:

top

The baseline system showed:

Very low CPU utilization
Low system load
No zombie processes
No stopped processes
Low memory utilization

## Process Signals
### SIGTERM
A background process was created:
sleep 300 &

The process was identified using:
pgrep -a sleep

It was then gracefully terminated:
kill <PID>

This demonstrated the use of SIGTERM for normal process
termination.
### SIGKILL

A second process was created:
sleep 300 &

The process was forcefully terminated using:
kill -9 <PID>

SIGKILL was used to demonstrate forceful process termination
when a normal termination is not sufficient.
Job Control

Foreground and background job control was demonstrated using:

sleep 300

The process was suspended using:
Ctrl + Z

The suspended job was moved to the background:
bg

The job was brought back to the foreground:
fg

It was then terminated using:
Ctrl + C

Job status was checked using:
jobs

## Persistent Background Jobs

The nohup command was tested to demonstrate running a process
without depending on the terminal session:

nohup sleep 300 > nohup-test.log 2>&1 &

The running process was verified using:

**pgrep -a sleep**

The process relationship was inspected using:

**ps -p <PID> -o pid,ppid,sid,stat,cmd**

The output file was checked using:
**ls -l nohup-test.log
cat nohup-test.log**

The empty log file was expected because the sleep command
does not generate output.
