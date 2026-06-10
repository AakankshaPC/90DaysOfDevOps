# Scenario based learning
## Scenario 1: Service Not Starting

```
A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.
```
Step 1: 
Command

```bash
systemctl status myapp
```
    systemctl status is used to view the current status and health of a systemd service on a Linux system.
    It shows whether the service is running, stopped, failed, its recent logs, and other useful details for troubleshooting.

Step 2 : 
Command
```bash
systemctl is-enabled myapp
```
    This command checks whether the myapp service is configured to start automatically when the system boots.

Step 3 : 
Command
```bash
journalctl -u myapp -n 50
```
    journalctl is used to view and analyze logs collected by systemd's journal on Linux systems.
    The -u option in journalctl stands for unit and is used to filter logs for a specific systemd service.
    The -n option specifies how many recent log entries to display.

## Scenario 2: High CPU Usage
```
Your manager reports that the application server is slow. You SSH into the server.
What commands would you run to identify which process is using high CPU?
```

Step 1 : 
Command
```bash
top
```
      This is the most commonly used command to view live CPU usage.
      The top command displays real-time information about CPU, memory, and running processes. 
      It is commonly used to monitor system performance and identify resource-intensive processes.

Step 2 : 
Command
```bash
htop
```
      htop is an interactive process monitoring tool. 
      It that provides a real-time view of CPU usage, memory usage, and running processes.
      
Step 3: 
Command

```bash
ps aux --sort=%cpu | head -10
```
    * "ps" Stands for Process Status.
    Used to display information about running processes.
    * a - Shows processes for all users on the system.
    * u - Displays the output in a user-oriented format, including: User, CPU usage, Memory usage, Start time, Command, x.
    Shows processes that are not attached to a terminal (background services, daemons, etc.).

    * Without x, you might miss important services like Nginx or Docker.

    * --sort=-%cpu
      --sort tells ps to sort the output.

      
    * %cpu means sort by CPU utilization.
    * The minus sign (-) means descending order (highest first).

    | passes the output to another command.
    head -10 shows only the first 10 lines.


## Scenario 3: Finding Service Logs

```
A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?
```

Step 1 : 

Command

```bash
systemctl status ssh
```
    systemctl status is used to view the current status and health of a systemd service on a Linux system.
    This command will show the current status and health of ssh.
    
Step 2 : 
       
Command

```bash
journalctl -u ssh -n 50
```

    journalctl is used to view and analyze logs collected by systemd.
    -u displayes in user oriented format
    - n 50 shows only the first 50 lines.

Step 3 : 

 Command

```bash
journalctl -u ssh -f
```


* `-f` → Follow the logs in real time (similar to `tail -f`).

### What it does

This command continuously displays new SSH service logs as they are generated, allowing you to monitor SSH login attempts, connections, and errors in real time.

### 2-line explanation for notes

**`journalctl -u ssh -f` displays SSH service logs in real time. It is useful for monitoring SSH connections and troubleshooting authentication or service issues as they occur.**




## Scenario 4: File Permissions Issue
```
A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?

```

Step 1 : 

Command

```bash
ls -l /home/user/backup.sh
```

    We have to look for file permissions if we notice no 'x' that means the file is not executable.

Step 2 :
Command

```bash
chmod +x /home/user/backup.sh
```

    Since we dont have execute permission, now we are adding execute permission.

Step 3 : 
Command

```bash
ls -l /home/user/backup.sh
```
    Verify if its working or not. Look for x in the permissions.

Step 4 : 
Command

```bash
./backup.sh
```

Try running the script again. 


    







      
