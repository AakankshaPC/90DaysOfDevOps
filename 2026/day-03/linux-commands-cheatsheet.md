# Linux Commands Cheat Sheet

## File System Commands

| Command                   | Description                                |
| --------------------------| ------------------------------------------ |
| pwd                       | Display current working directory          |
| ls                        | List files and directories                 |
| ls -la                    | List all files including hidden files      |
| cd <directory>            | Change directory                           |
| mkdir <directory>         | Create a new directory                     |
| touch <file>              | Create an empty file                       |
| cp <source> <destination> | Copy files or directories                  |
| mv <source> <destination> | Move or rename files/directories           |
| rm <file>                 | Remove a file                              |
| rm -r <directory>         | Remove a directory recursively             |
| find . -name <filename>   | Search for files                           |
| cat <file>                | Display file contents                      |
| head -n 10 <file>         | Show first 10 lines of a file              |
| tail -n 10 <file>         | Show last 10 lines of a file               |
| tree                      | Display directory structure in tree format |
| df -h                     | Show disk space usage                      |
| du -sh <directory>        | Show directory size                        |



## Process Management Commands

| Command             | Description                                  |
| ------------------- | -------------------------------------------- |
| `ps`                | Show processes in current terminal           |
| `ps -e`             | Show all running processes                   |
| `ps -ef`            | Show all processes with detailed information |
| `ps aux`            | Show all processes with CPU and memory usage |
| `pgrep <process>`   | Find process IDs by name                     |
| `pidof <process>`   | Display PID of a process                     |
| `top`               | Monitor running processes in real time       |
| `kill <PID>`        | Terminate a process                          |
| `kill -9 <PID>`     | Forcefully terminate a process               |
| `killall <process>` | Kill all instances of a process              |
| `jobs`              | Display background jobs                      |
| `bg`                | Resume a job in the background               |
| `fg`                | Bring a background job to the foreground     |

---

## Logs & Service Management

| Command                   | Description                      |
| ------------------------- | -------------------------------- |
| `journalctl`              | View system logs                 |
| `journalctl -u nginx`     | View logs for a specific service |
| `journalctl -f`           | Follow logs in real time         |
| `tail -f /var/log/syslog` | Monitor log file continuously    |
| `systemctl status nginx`  | Check service status             |
| `systemctl start nginx`   | Start a service                  |
| `systemctl stop nginx`    | Stop a service                   |
| `systemctl restart nginx` | Restart a service                |
| `systemctl enable nginx`  | Enable service at boot           |
| `systemctl disable nginx` | Disable service at boot          |

---

## Networking Commands

| Command                    | Description                                    |
| -------------------------- | ---------------------------------------------- |
| `ping google.com`          | Test network connectivity                      |
| `ip addr`                  | Display IP addresses and network interfaces    |
| `hostname -I`              | Show system IP address                         |
| `curl https://example.com` | Send HTTP request to a website or API          |
| `wget <url>`               | Download files from the internet               |
| `dig google.com`           | Query DNS records                              |
| `nslookup google.com`      | Resolve domain names                           |
| `ss -tulpn`                | Display listening ports and active connections |
| `netstat -tulpn`           | Show network connections and ports             |
| `traceroute google.com`    | Trace network path to destination              |

---

## Frequently Used Commands During Troubleshooting

```bash
ps aux
top
df -h
du -sh 
tail -f app.log
journalctl -u nginx
systemctl status nginx
ip addr
curl https://example.com
ss -tulpn
```

## Key Takeaways

* Use File System commands to navigate and manage files.
* Use Process commands to inspect and control running applications.
* Use Logs & Service Management commands to troubleshoot services.
* Use Networking commands to diagnose connectivity and DNS issues.

These commands form the foundation of Linux administration and DevOps troubleshooting.


