# Day 04 – Linux Practice: Processes and Services

## 1. Process Checks

### Command 1 — `ps aux | head`

```bash
ubuntu@ip-172-31-42-169:~$ ps aux | head
```

**Output:**
```
USER       PID %CPU %MEM    VSZ   RSS TTY   STAT START  TIME COMMAND
root         1  1.5  1.7  25224 16024 ?     Ss   14:36  0:02 /sbin/init
root         2  0.0  0.0      0     0 ?     S    14:36  0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?     S    14:36  0:00 [pool_workqueue_release]
root         4  0.0  0.0      0     0 ?     I<   14:36  0:00 [kworker/R-rcu_gp]
root         5  0.0  0.0      0     0 ?     I<   14:36  0:00 [kworker/R-sync_wq]
root         6  0.0  0.0      0     0 ?     I<   14:36  0:00 [kworker/R-kvfree_rcu_reclaim]
root         7  0.0  0.0      0     0 ?     I<   14:36  0:00 [kworker/R-slub_flushwq]
root         8  0.0  0.0      0     0 ?     I<   14:36  0:00 [kworker/R-netns]
root         9  0.0  0.0      0     0 ?     I    14:36  0:00 [kworker/0:0-cgroup_free]
```

### Command 2 — `ps aux --sort=%mem` and `ps aux --sort=%cpu`

```bash
ubuntu@ip-172-31-42-169:~$ ps aux --sort=%mem | head -5
ubuntu@ip-172-31-42-169:~$ ps aux --sort=%cpu | head -5
```

**Output (both sorted the same on this idle instance):**
```
USER   PID %CPU %MEM  VSZ  RSS TTY  STAT START  TIME COMMAND
root     2  0.0  0.0    0    0 ?    S    14:36  0:00 [kthreadd]
root     3  0.0  0.0    0    0 ?    S    14:36  0:00 [pool_workqueue_release]
root     4  0.0  0.0    0    0 ?    I<   14:36  0:00 [kworker/R-rcu_gp]
root     5  0.0  0.0    0    0 ?    I<   14:36  0:00 [kworker/R-sync_wq]
```

### Command 3 — `htop` (interactive process viewer)

```bash
ubuntu@ip-172-31-42-169:~$ htop
```
Tasks: 8 total, 0 threads, 1 running
Load average: 0.00  0.00  0.00
Uptime: 11 days, 05:59:29

  PID USER     PRI NI VIRT  RES  SHR S CPU% MEM%  TIME+   Command
    1 sandbox   20  0 4628 3612 3164 S  0.0  0.0  0:00.01  /bin/bash
   13 sandbox   20  0 4628 3692 3248 S  0.0  0.0  0:00.01  /bin/bash
   99 sandbox   20  0 3176 2316 2036 T  0.0  0.0  0:00.02  less sample.log
  116 sandbox   20  0 7312 3280 2732 T  0.0  0.0  0:00.00  top
  117 sandbox   20  0 5004 3664 3020 R  0.0  0.0  0:00.00  htop
```

### 2. Service Checks
### Command 4 — `systemctl status ssh`

```bash
ubuntu@ip-172-31-42-169:~$ systemctl status ssh
```

**Output:**
```
● ssh.service – OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: ena)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Tue 2026-06-02 14:36:41 UTC; 2min 35s ago
  Invocation: caacfb57505343c5b5cfa2c19149e6f5
 TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1012 (sshd)
      Tasks: 1 (limit: 627)
     Memory: 6.8M (peak: 8M)
        CPU: 72ms
     CGroup: /system.slice/ssh.service
             └─1012 "sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand ..."

Jun 02 14:36:41 systemd[1]: Starting ssh.service – OpenBSD Secure Shell server...
Jun 02 14:36:41 sshd[1012]: Server listening on 0.0.0.0 port 22.
Jun 02 14:36:41 systemd[1]: Started ssh.service – OpenBSD Secure Shell server.
Jun 02 14:36:41 sshd[1012]: Server listening on :: port 22.
Jun 02 14:37:08 sshd-session[1138]: Accepted publickey for ubuntu from 139.5.27.160 port 49398 ssh2: RSA SHA256:EY0texeKAAaN...
Jun 02 14:37:08 sshd-session[1138]: pam_unix(sshd:session): session opened for user ubuntu(uid=1000) by ubuntu(uid=0)
```

### Command 5 — `sudo ss -tulpn | grep :22`

```bash
ubuntu@ip-172-31-42-169:~$ sudo ss -tulpn | grep :22
```

**Output:**
```
tcp  LISTEN  0  4096  0.0.0.0:22  0.0.0.0:*  users:(("sshd",pid=1012,fd=3),("systemd",pid=1,fd=196))
tcp  LISTEN  0  4096     [::]:22     [::]:*  users:(("sshd",pid=1012,fd=4),("systemd",pid=1,fd=197))
```


## 3. Log Checks

### Command 6 — `journalctl -u ssh` (service logs)

```bash
ubuntu@ip-172-31-42-169:~$ journalctl -u ssh -n 20 --no-pager
```

**Output (from systemctl status output above, which includes journal tail):**
```
Jun 02 14:36:41 ip-172-31-42-169 systemd[1]: Starting ssh.service – OpenBSD Secure Shell server...
Jun 02 14:36:41 ip-172-31-42-169 sshd[1012]: Server listening on 0.0.0.0 port 22.
Jun 02 14:36:41 ip-172-31-42-169 systemd[1]: Started ssh.service – OpenBSD Secure Shell server.
Jun 02 14:36:41 ip-172-31-42-169 sshd[1012]: Server listening on :: port 22.
Jun 02 14:37:08 ip-172-31-42-169 sshd-session[1138]: Accepted publickey for ubuntu from 139.5.27.160 port 49398 ssh2: RSA SHA256:EY0texeKAAaN...
Jun 02 14:37:08 ip-172-31-42-169 sshd-session[1138]: pam_unix(sshd:session): session opened for user ubuntu(uid=1000) by ubuntu(uid=0)
```


## 4. Mini Troubleshooting Flow

**Scenario:** "I can't SSH into the server — is sshd running?"

```bash
# Step 1 – Check if the service is running
systemctl status ssh
# Look for: active (running) or  failed / inactive 

# Step 2 – Is it actually listening on port 22?
sudo ss -tulpn | grep :22
# Expect: 0.0.0.0:22 and [::]:22 with sshd pid 
# If missing: sshd is not bound → restart the service

# Step 3 – Any errors in the logs?
journalctl -u ssh -n 30 --no-pager
# Look for: "error", "failed", "refused" in recent lines

# Step 4 – If the service is failed, restart it
sudo systemctl restart ssh
journalctl -u ssh -f     # watch logs immediately after restart

# Step 5 – Confirm the process is alive with the right PID
ps aux | grep sshd
# Expect: /usr/sbin/sshd -D ... (the main daemon)
```

**On my AWS instance — all checks passed:**
- ✅ `systemctl status ssh` → `active (running)`
- ✅ `ss -tulpn | grep :22` → listening on both IPv4 and IPv6
- ✅ `journalctl` → clean startup, successful login recorded
- ✅ `ps aux | grep sshd` → PID 1012 running

---

## Key Takeaways

| Command | What it does |
|---|---|
| `ps aux \| head` | Show all processes, first 10 lines |
| `ps aux --sort=%cpu` | Sort processes by CPU usage |
| `ps aux --sort=%mem` | Sort processes by memory usage |
| `htop` | Interactive process viewer with per-CPU bars |
| `systemctl status ssh` | Full service health: state, PID, memory, recent logs |
| `sudo ss -tulpn \| grep :22` | Confirm sshd is bound and listening on port 22 |
| `journalctl -u ssh -n 20` | Last 20 log lines for the ssh service |
| `journalctl -u ssh -f` | Follow ssh logs live (like tail -f) |

---

## Why This Matters for DevOps

On AWS EC2, SSH is your lifeline — if sshd goes down you lose access to the instance entirely.
These 8 commands let you:
1. Confirm a service is running before you report an outage
2. Find the exact moment something failed in the logs
3. Check that a process is listening on the expected port
4. Restart and verify recovery — all in under 2 minutes

Muscle memory with these commands = faster incident response.
