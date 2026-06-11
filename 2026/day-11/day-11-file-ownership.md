# Day 11 – File Ownership Challenge (chown & chgrp)

## Objective

Learn how Linux file ownership works and practice changing file owners and groups using `chown` and `chgrp`.

---

# Task 1: Understanding Ownership

## Commands Used

```bash
cd ~
ls -l
```

## Sample Output

```bash
-rw-r--r-- 1 ubuntu ubuntu   0 Jun 11 10:00 devops-file.txt
drwxr-xr-x 2 ubuntu ubuntu 4096 Jun 11 10:05 projects
```

### Ownership Format

```text
-rw-r--r-- 1 owner group size date filename
```

### Difference Between Owner and Group

* **Owner**: The user who owns and controls the file.
* **Group**: A collection of users who can be granted shared access to the file.
* Ownership determines who can read, write, or execute files and directories.

---

### Screenshot
<img width="695" height="367" alt="Screenshot 2026-06-11 at 10 09 09 PM" src="https://github.com/user-attachments/assets/e9f3c96f-2a29-41de-ad14-03efaffdcac4" />


# Task 2: Basic chown Operations

## Commands Used

```bash
touch devops-file.txt

ls -l devops-file.txt

sudo useradd tokyotown
sudo useradd berlintown

sudo chown tokyotown devops-file.txt
ls -l devops-file.txt

sudo chown berlintown devops-file.txt
ls -l devops-file.txt
```

## Ownership Changes

| File            | Before        | After         |
| --------------- | ------------- | ------------- |
| devops-file.txt | ubuntu:ubuntu | tokyotown:ubuntu  |
| devops-file.txt | tokyo:ubuntu  | berlintown:ubuntu |

### Screenshot

<img width="695" height="245" alt="Screenshot 2026-06-11 at 10 13 18 PM" src="https://github.com/user-attachments/assets/bb0d2aab-d25a-47e7-a6a1-3f119c8c4ab9" />


---

# Task 3: Basic chgrp Operations

## Commands Used

```bash
touch team-notes.txt

ls -l team-notes.txt

sudo groupadd heist-team

sudo chgrp heist-team team-notes.txt

<img width="695" height="245" alt="Screenshot 2026-06-11 at 10 26 43 PM" src="https://github.com/user-attachments/assets/9993cec9-5f22-4cb6-9f02-f32aca92f944" />
```

## Ownership Changes

| File           | Before Group | After Group |
| -------------- | ------------ | ----------- |
| team-notes.txt | ubuntu       | heist-team  |

### Screenshot

<img width="695" height="245" alt="Screenshot 2026-06-11 at 10 26 43 PM" src="https://github.com/user-attachments/assets/ee727718-b719-4795-aaae-ddc5e522124a" />


---

# Task 4: Combined Owner & Group Change

## Commands Used

```bash
touch project-config.yaml

sudo useradd professor1

sudo chown professor:heist-team project-config.yaml

ls -l project-config.yaml

mkdir app-logs

sudo chown berlin:heist-team app-logs

ls -ld app-logs
```

## Ownership Changes

| File/Directory      | Before        | After                |
| ------------------- | ------------- | -------------------- |
| project-config.yaml | ubuntu:ubuntu | professor:heist-team |
| app-logs            | ubuntu:ubuntu | berlin:heist-team    |

### Screenshot

<img width="695" height="278" alt="Screenshot 2026-06-11 at 10 28 21 PM" src="https://github.com/user-attachments/assets/7ed2afcb-70d8-4484-afbc-8fc6f10ac524" />

---

# Task 5: Recursive Ownership

## Commands Used

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf

sudo groupadd planners

sudo chown -R professor:planners heist-project/

ls -lR heist-project/
```

## Verification

```bash
heist-project/
├── plans/
│   └── strategy.conf
└── vault/
    └── gold.txt
```

All files and directories were changed to:

```text
Owner: professor
Group: planners
```

### Screenshot

<img width="695" height="865" alt="Screenshot 2026-06-11 at 10 31 59 PM" src="https://github.com/user-attachments/assets/e6690b7d-49e7-46de-905a-f08d171fd5de" />


---

# Task 6: Practice Challenge

## Commands Used

```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi

sudo groupadd vault-team
sudo groupadd tech-team

mkdir bank-heist

touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt

sudo chown tokyo:vault-team bank-heist/access-codes.txt

sudo chown berlin:tech-team bank-heist/blueprints.pdf

sudo chown nairobi:vault-team bank-heist/escape-plan.txt

ls -l bank-heist/
```

## Final Ownership

| File             | Owner   | Group      |
| ---------------- | ------- | ---------- |
| access-codes.txt | tokyo   | vault-team |
| blueprints.pdf   | berlin  | tech-team  |
| escape-plan.txt  | nairobi | vault-team |

### Screenshot

<img width="695" height="411" alt="Screenshot 2026-06-11 at 10 34 47 PM" src="https://github.com/user-attachments/assets/c6786941-36ef-4973-a890-e0696a0bdbba" />


---

# Files & Directories Created

## Files

```text
devops-file.txt
team-notes.txt
project-config.yaml

heist-project/vault/gold.txt
heist-project/plans/strategy.conf

bank-heist/access-codes.txt
bank-heist/blueprints.pdf
bank-heist/escape-plan.txt
```

## Directories

```text
app-logs/
heist-project/
heist-project/vault/
heist-project/plans/
bank-heist/
```

---

# Commands Reference

```bash
# View ownership
ls -l filename

# Change owner
sudo chown newowner filename

# Change group
sudo chgrp newgroup filename

# Change owner and group
sudo chown owner:group filename

# Recursive ownership change
sudo chown -R owner:group directory/

# Change only group using chown
sudo chown :groupname filename
```

---

# What I Learned

1. Every Linux file has an owner and a group associated with it.
2. The `chown` command changes file ownership, while `chgrp` changes group ownership.
3. Recursive ownership changes using `-R` are useful when managing application directories, logs, and deployment files.

---

# Troubleshooting

## Permission Denied

```bash
sudo chown username filename
```

Use `sudo` for ownership-related operations.

## Group Does Not Exist

```bash
sudo groupadd groupname
```

Create the group before assigning it.

## User Does Not Exist

```bash
sudo useradd username
```

Create the user before changing ownership.

---

# Why This Matters for DevOps

Proper file ownership is essential for:

* Application deployments
* Shared team directories
* Container file permissions
* CI/CD pipeline artifacts
* Log file management
* Security and access control


