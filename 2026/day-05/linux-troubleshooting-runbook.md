# Linux Fundamentals Runbook

## Target Service: SSH (sshd)

### Objective
Perform basic Linux system inspection and troubleshooting using common administrative commands. Use SSH (`sshd`) as the target service.

---

# 1. Environment Basics

## Command

```bash
uname -a
```

### Purpose
Displays kernel version, architecture, hostname, and operating system details.

### Example Output

```text
Linux ip-172-31-42-169 6.8.0-1029-aws #31-Ubuntu SMP x86_64 GNU/Linux
```

### Observation
System is running Ubuntu on an AWS EC2 instance using the AWS Linux kernel.

---

## Command

```bash
lsb_release -a
```

### Purpose
Displays Linux distribution information.

### Example Output

```text
No LSB modules are available.
Distributor ID: Ubuntu
Description: Ubuntu 24.04 LTS
Release: 24.04
Codename: noble
```

### Observation
LBS stands for Linux Standard Base

 ```text 
|Note| modules are optional packages that provides information about which part of LBS installed on system. So its common to get above error after executing the command.
```

---

# 2. Filesystem Sanity

## Command

```bash
mkdir /tmp/runbook-demo
```

### Purpose
Creates a temporary directory for testing filesystem operations.

### Result

```text
(no output)
```

### Observation
Directory created successfully.

---

## Command

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

### Purpose
source = /etc/hosts
Destination = /tmp/runbook-demo/hosts-copy
Copies a system file and verifies the copied file.

### Example Output

```text
total 4
-rw-r--r-- 1 ubuntu ubuntu 222 Jun 3 10:20 hosts-copy
```

### Observation
The file was copied successfully.

---

# 3. CPU and Memory

## Command

```bash
free -h
```

### Purpose
Displays memory and swap usage in human-readable format.

### Example Output

```text
               total        used        free      shared  buff/cache   available
Mem:           911Mi       250Mi       200Mi        10Mi       460Mi       540Mi
Swap:             0B          0B          0B
```

### Observation
Memory usage is healthy with sufficient available RAM.

---

## Command

```bash
ps aux | grep sshd
```

### Purpose
Find the SSH daemon process.

### Example Output

```text
root       845  0.0  0.1 sshd: /usr/sbin/sshd
```

---

## Command

```bash
ps -o pid,pcpu,pmem,comm -p 845
```

### Purpose
View CPU and memory usage for the SSH process.

### Example Output

```text
PID %CPU %MEM COMMAND
845  0.0  0.1 sshd
```

### Observation
SSH daemon is running and consuming minimal resources.

---

# 4. Disk and Storage

## Command

```bash
df -h
```

### Purpose
Displays mounted filesystems and disk usage.

### Example Output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.7G  2.1G  4.6G  32% /
```

### Observation
Root filesystem is only 32% utilized.

---

## Command

```bash
du -sh /var/log
```

### Purpose
Checks the size of the log directory.

### Example Output

```text
28M /var/log
```

### Observation
Log files are consuming a reasonable amount of space.

---

# 5. Network

## Command

```bash
ss -tulpn | grep ssh
```

### Purpose
Checks whether SSH is listening on a network port.

### Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=845,fd=3))
```

### Observation
SSH service is actively listening on port 22.

---

## Command

```bash
ping -c 4 google.com
```

### Purpose
Tests network connectivity.

### Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

### Observation
Internet connectivity is working correctly.

---

# 6. Logs

## Command

```bash
journalctl -u ssh -n 20
```

### Purpose
Displays recent SSH service logs.

### Example Output

```text
Jun 03 10:00:15 ip-172-31-42-169 sshd[2105]: Accepted publickey for ubuntu
Jun 03 10:00:15 ip-172-31-42-169 sshd[2105]: Session opened for user ubuntu
```

### Observation
Recent SSH login activity is visible.

---

## Command

```bash
tail -n 20 /var/log/auth.log
```

### Purpose
Displays recent authentication log entries.

### Example Output

```text
Jun 03 10:00:15 ip-172-31-42-169 sshd[2105]: Accepted publickey for ubuntu
```

### Observation
Authentication logs confirm successful SSH access.

---

# SSH Service Summary

| Check | Status |
|---------|---------|
| SSH Process Running | Yes |
| SSH Listening Port | 22 |
| CPU Usage | Low |
| Memory Usage | Low |
| Disk Health | Healthy |
| Network Connectivity | Working |
| SSH Logs Available | Yes |

## Conclusion

The SSH service (`sshd`) is running correctly and listening on port 22. System resources are healthy, disk usage is low, network connectivity is functional, and authentication logs confirm successful user logins.
