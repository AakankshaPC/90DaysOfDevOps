# day-12-revision.md (Mini Self-Check Answers)

## 1. Which 3 commands save you the most time right now, and why?

1. ls -l → Quickly shows file details, permissions, owner, and group in one command.

2. systemctl status <service> → Instantly checks whether a service is running, failed, or inactive.

3. tail -f <file> → Helps monitor logs in real time for troubleshooting applications and services.

## 2. How do you check if a service is healthy? List the exact 2–3 commands you’d run first.

For example, to check the nginx service:

1. systemctl status → Shows detailed service status.

2. systemctl is-active → Quickly confirms if the service is active.

3. journalctl -u → Displays recent logs to check for errors or warnings.

## 3. How do you safely change ownership and permissions without breaking access? Give one example command.

First, check current permissions with ls -l. Then change ownership or permissions carefully using sudo and avoid giving unnecessary 777 permissions.

### Example command

> ls -l app-config.yaml

> sudo chown ubuntu:developers app-config.yaml

> chmod 640 app-config.yaml


Why this is safe:

* Changes only the owner and group of app-config.yaml.

* Does not modify file permissions unexpectedly.

* Keeps access controlled for the developers group.

### 4. What will you focus on improving in the next 3 days?

I will focus on:

1. Practicing Linux permissions and ownership until the commands become natural.

2. Improving troubleshooting skills using systemctl, journalctl, and log analysis.

3. Building confidence with Git and DevOps workflows by doing small daily hands-on tasks.
