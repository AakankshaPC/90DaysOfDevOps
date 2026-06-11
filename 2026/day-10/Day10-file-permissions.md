# Day 10 – File Permissions & Basic File Operations

## Objective

Today's goal was to practice creating, reading, and managing files in Linux while understanding and modifying file permissions using the `chmod` command.

---

# Task 1: Create Files

## Files Created

### Create an Empty File

```bash
touch devops.txt
```

### Create a File with Content

```bash
echo "These are my DevOps notes." > notes.txt
```

### Create a Shell Script

```bash
vim script.sh
```

Contents:

```bash
echo "Hello DevOps"
```

### Verify File Creation

```bash
ls -l
```

### Screenshot

<img width="1288" height="242" alt="Screenshot 2026-06-11 at 9 40 49 PM" src="https://github.com/user-attachments/assets/511367d9-e460-42b4-bfd5-4b4f29a2ee82" />


---

# Task 2: Read Files

## View File Content

### Read notes.txt

```bash
cat notes.txt
```

### Open script.sh in Read-Only Mode

```bash
vim -R script.sh
```

### Display First 5 Lines of /etc/passwd

```bash
head -n 5 /etc/passwd
```

### Display Last 5 Lines of /etc/passwd

```bash
tail -n 5 /etc/passwd
```

### Screenshot

<img width="695" height="294" alt="task 2" src="https://github.com/user-attachments/assets/d4b0ed12-4aef-4b4d-bdea-b184e427a57b" />

---

# Task 3: Understand Permissions

## Permission Format

```text
rwxrwxrwx
│  │  │
│  │  └── Others
│  └───── Group
└──────── Owner
```

### Permission Values

| Permission  | Value |
| ----------- | ----- |
| Read (r)    | 4     |
| Write (w)   | 2     |
| Execute (x) | 1     |

### Check Current Permissions

```bash
ls -l devops.txt notes.txt script.sh
```

### Example Analysis

| File       | Permissions | Description                           |
| ---------- | ----------- | ------------------------------------- |
| devops.txt | rw-r--r--   | Owner can read/write, others can read |
| notes.txt  | rw-r--r--   | Owner can read/write, others can read |
| script.sh  | rw-r--r--   | Not executable yet                    |

### Screenshot

<img width="695" height="294" alt="task 3" src="https://github.com/user-attachments/assets/e4f62121-41aa-4b7c-8714-12036a5d7cef" />

---

# Task 4: Modify Permissions

## Make script.sh Executable

```bash
chmod +x script.sh
```

Run the script:

```bash
./script.sh
```

Output:

```text
Hello DevOps
```

---

## Make devops.txt Read-Only

```bash
chmod a-w devops.txt
```

Verify:

```bash
ls -l devops.txt
```

---

## Set notes.txt Permission to 640

```bash
chmod 640 notes.txt
```

Verify:

```bash
ls -l notes.txt
```

Expected:

```text
-rw-r----- notes.txt
```

---

## Create Directory with 755 Permissions

```bash
<img width="695" height="407" alt="Screenshot 2026-06-11 at 9 52 26 PM" src="https://github.com/user-attachments/assets/87e5c3dc-7e7a-44aa-8bfa-ffc0571164da" />
```

Verify:

```bash
ls -ld project
```

Expected:

```text
drwxr-xr-x
```

### Screenshot

<img width="695" height="407" alt="Screenshot 2026-06-11 at 9 52 26 PM" src="https://github.com/user-attachments/assets/5d9ec5ce-6429-44c3-b101-2467fcc38a4f" />


---

# Task 5: Test Permissions

## Attempt to Write to Read-Only File

```bash
echo "Testing" >> devops.txt
```

Observed Result:

```text
Permission denied
```

---

## Remove Execute Permission from Script

```bash
chmod -x script.sh
```

Attempt to Execute:

```bash
<img width="695" height="407" alt="task 5" src="https://github.com/user-attachments/assets/ed744ef7-f6f4-4949-8dd8-a337a35fbb4d" />
```

Observed Result:

```text
Permission denied
```

### Error Messages Observed

* Permission denied while modifying a read-only file.
* Permission denied while executing a file without execute permission.

### Screenshot

<img width="695" height="407" alt="task 5" src="https://github.com/user-attachments/assets/2d282838-96ca-4247-831d-7f36c07bef92" />


---

# Files Created

* devops.txt
* notes.txt
* script.sh
* project/

---

# Permission Changes

| File/Directory | Before    | After     |
| -------------- | --------- | --------- |
| script.sh      | rw-r--r-- | rwxr-xr-x |
| devops.txt     | rw-r--r-- | r--r--r-- |
| notes.txt      | rw-r--r-- | rw-r----- |
| project        | default   | rwxr-xr-x |

---

# Commands Used

```bash
touch
echo
cat
vim
vim -R
head
tail
ls -l
ls -ld
chmod +x
chmod -x
chmod a-w
chmod 640
chmod 755
mkdir
./script.sh
```

---

# What I Learned

* Linux permissions are divided into owner, group, and others.
* Read (r), write (w), and execute (x) permissions control file access and execution.
* The `chmod` command can modify permissions using symbolic or numeric notation.
* A script must have execute permission before it can be run.
* Directories require execute permission to allow users to access their contents.

---

# Outcome

Successfully created files and directories, viewed file contents, modified permissions using `chmod`, and tested how permissions affect file access and execution.
