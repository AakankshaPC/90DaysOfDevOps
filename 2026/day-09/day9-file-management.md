# Day 09 – Linux User & Group Management Challenge

## Objective

Today's goal was to practice Linux user and group management by creating users, assigning groups, configuring shared directories, and managing file permissions.

---

# Task 1: Create Users

## Users Created

* tokyo
* berlin
* professor

### Commands Used

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

### Verification

Check user entries:

```bash
grep -E "tokyo|berlin|professor" /etc/passwd
```

Check home directories:

```bash
ls -l /home
```
### Screenshot

<img width="1440" height="900" alt="Task 1" src="https://github.com/user-attachments/assets/c31751a4-2603-43ed-ac59-0abcb89d6f63" />

# Task 2: Create Groups

## Groups Created

* developers
* admins

### Commands Used

```bash
sudo groupadd developers
sudo groupadd admins
```

### Verification

```bash
grep -E "developers|admins" /etc/group
```

### Screenshot

<img width="1440" height="900" alt="task 2" src="https://github.com/user-attachments/assets/a19c1350-660c-4aa7-a8f0-bda77e1bc9cc" />

# Task 3: Assign Users to Groups

## Group Assignments

| User      | Groups             |
| --------- | ------------------ |
| tokyo     | developers         |
| berlin    | developers, admins |
| professor | admins             |

### Commands Used

```bash
sudo usermod -aG developers tokyo

sudo usermod -aG developers berlin
sudo usermod -aG admins berlin

sudo usermod -aG admins professor
```

### Verification

```bash
groups tokyo
groups berlin
groups professor
```

### Screenshot

<img width="698" height="900" alt="Task 3" src="https://github.com/user-attachments/assets/8cd676e7-bef7-4870-8a6a-269ef875abe1" />


---

# Task 4: Shared Directory

## Directory Created

```text
/opt/dev-project
```

### Commands Used

```bash
sudo mkdir /opt/dev-project

sudo chown root:developers /opt/dev-project

sudo chmod 775 /opt/dev-project
```

### Verification

Check permissions:

```bash
ls -ld /opt/dev-project
```

Test file creation:

```bash
su - tokyo
touch /opt/dev-project/tokyo.txt
exit

su - berlin
touch /opt/dev-project/berlin.txt
exit
```

Verify files:

```bash
ls -l /opt/dev-project
```

### Screenshot

<img width="698" height="900" alt="task 4" src="https://github.com/user-attachments/assets/f8ce710a-8f63-47a4-8f54-85ba3f77c849" />


---

# Task 5: Team Workspace

## User and Group Setup

### Commands Used

Create user:

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

Create group:

```bash
sudo groupadd project-team
```

Add users:

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

Create workspace:

```bash
sudo mkdir /opt/team-workspace

sudo chown root:project-team /opt/team-workspace

sudo chmod 775 /opt/team-workspace
```

### Verification

Check permissions:

```bash
ls -ld /opt/team-workspace
```

Test file creation:

```bash
su - nairobi
touch /opt/team-workspace/nairobi.txt
exit
```

Verify:

```bash
ls -l /opt/team-workspace
```

### Screenshot


<img width="1440" height="900" alt="task 5" src="https://github.com/user-attachments/assets/c48b8d90-650f-46a8-93f4-4754ca5d5013" />
<img width="1440" height="444" alt="task 5 1" src="https://github.com/user-attachments/assets/85722d4d-bea6-4eb2-bfa3-fb37573bbe5b" />



---

# Commands Used

```bash
useradd
passwd
groupadd
usermod
groups
grep
ls
mkdir
chown
chmod
su
touch
```

---

# Challenges Faced

### Challenge 1: User Created Without Home Directory

**Issue:** User was created using `useradd` without the `-m` option, resulting in a missing home directory.

**Solution:** Recreated the user or manually created the home directory and assigned ownership.

---

### Challenge 2: Permission Denied While Creating Shared Directories

**Issue:** Could not create directories under `/opt` as a regular user.

**Solution:** Used `sudo` because `/opt` is owned by the root user.

---

### Challenge 3: Group Changes Not Reflecting Immediately

**Issue:** Newly assigned groups were not visible in the current session.

**Solution:** Logged out and back in (or used `su - username`) to refresh group membership.

---

# What I Learned

* Linux users and groups are managed using `useradd`, `groupadd`, and `usermod`.
* The `-m` option with `useradd` automatically creates a user's home directory.
* Shared directories can be managed through group ownership and permissions.
* The `775` permission allows owners and group members to read, write, and execute files.
* Group membership is an effective way to provide controlled access to shared resources.
* Proper ownership and permissions are essential for collaboration and system security.

---

# Outcome

Successfully created users and groups, configured shared project directories, managed permissions, and verified access using multiple user accounts.
