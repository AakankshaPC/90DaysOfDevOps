# Day 08 - Cloud Deployment with AWS EC2

## Overview

In this lab, I launched an AWS EC2 instance, connected to it using SSH, installed and managed Nginx, configured network access through Security Groups, and extracted Nginx logs from the server to my local machine using SCP.

---

## Commands Used

### Connect to EC2 Instance

```bash
ssh -i ubuntu.pem ubuntu@<public-ip>
```

### Update the System

```bash
sudo apt update
sudo apt upgrade -y
```

### Install Nginx

```bash
sudo apt install nginx -y
```

### Check Nginx Status

```bash
sudo systemctl status nginx
```

### Start Nginx

```bash
sudo systemctl start nginx
```

### Check if Nginx Starts on Boot

```bash
systemctl is-enabled nginx
```

### View Nginx Logs

```bash
sudo tail -20 /var/log/nginx/access.log
```

### Copy Logs to a File

```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

### Check File Permissions

```bash
ls -l ~/nginx-logs.txt
```

### Change File Ownership

```bash
sudo chown ubuntu:ubuntu ~/nginx-logs.txt
```

### Download File to Local Machine

```bash
scp -i ubuntu.pem ubuntu@<public-ip>:~/nginx-logs.txt .
```

---

## Challenges Faced

### 1. Unable to Access Nginx from Browser

**Issue:**
I could successfully SSH into the EC2 instance, but opening the public IP in the browser did not work.

**Cause:**
The Security Group only allowed inbound traffic on port 22 (SSH). HTTP traffic on port 80 was blocked.

**Solution:**
Added an inbound rule to allow HTTP traffic on port 80 from anywhere (0.0.0.0/0).

---

### 2. SCP Authentication Failed

**Issue:**

```text
Permission denied (publickey)
```

**Cause:**
I attempted to run the SCP command from inside the EC2 instance, but the private key file (`ubuntu.pem`) existed only on my local machine.

**Solution:**
Exited the EC2 session and ran the SCP command from my MacBook, where the PEM file was available.

---

### 3. SCP Permission Denied While Downloading Logs

**Issue:**

```text
scp: remote open "nginx-logs.txt": Permission denied
```

**Cause:**
The log file was created using `sudo`, making the owner of the file `root`.

**Solution:**

```bash
sudo chown ubuntu:ubuntu ~/nginx-logs.txt
```

After changing ownership, the file could be downloaded successfully using SCP.

---

## What I Learned

* AWS Security Groups act as virtual firewalls and control inbound and outbound traffic.
* Port 22 is used for SSH access, while port 80 is used for HTTP web traffic.
* Nginx can be managed using `systemctl` commands such as start, stop, restart, and status.
* Linux file ownership and permissions directly affect file accessibility.
* SCP can be used to securely transfer files between a remote server and a local machine.
* Running commands with `sudo` may create files owned by the root user, requiring ownership changes before access by regular users.

---

## Outcome

Successfully deployed and accessed an Nginx web server on AWS EC2, viewed and extracted server logs, and securely downloaded the log file to my local machine.
