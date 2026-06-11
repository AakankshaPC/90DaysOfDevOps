# Day 13 – LVM (Logical Volume Manager)

## Objective

Learn how to create and manage storage using LVM by creating:

* Physical Volumes (PV)
* Volume Groups (VG)
* Logical Volumes (LV)
* Filesystems and Mount Points
* Extended Logical Volumes

---

## Task 1: Check Current Storage

### Commands Used

```bash
lsblk
pvs
vgs
lvs
df -h
```

## Task 2: Create Physical Volume

Initially, a loop device was used for LVM practice.

### Commands Used

```bash
pvcreate /dev/loop4
pvs
```

### Output

```text
Physical volume "/dev/loop4" successfully created.
```
---

## Task 3: Create Volume Group

### Commands Used

```bash
vgcreate devops-vg /dev/loop4
vgs
```

### Output

```text
Volume group "devops-vg" successfully created.
```

---

## Task 4: Add EBS Volume to LVM

A new 5 GiB EBS volume was created and attached to the EC2 instance.

### Verify New Disk

```bash
lsblk
```

**Example:**

```text
nvme1n1    5G disk
```

### Create Physical Volume on EBS

```bash
pvcreate /dev/nvme1n1
```

### Extend Existing Volume Group

```bash
vgextend devops-vg /dev/nvme1n1
```

### Verify

```bash
vgs
pvs
```

---

## Task 5: Create Logical Volume

### Commands Used

```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```

### Output

```text
Logical volume "app-data" created.
```

---

## Task 6: Format and Mount Logical Volume

### Format Filesystem

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

### Create Mount Point

```bash
mkdir -p /mnt/app-data
```

### Mount Logical Volume

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

### Verify

```bash
df -h /mnt/app-data
```

---

## Task 7: Extend the Logical Volume

### Extend LV

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

### Resize Filesystem

```bash
resize2fs /dev/devops-vg/app-data
```

### Verify

```bash
df -h /mnt/app-data
``


---

## Quick Reference: All Commands Used

```bash
# Storage inspection
lsblk
pvs
vgs
lvs
df -h

# Physical Volume creation
pvcreate /dev/loop4
pvcreate /dev/nvme1n1

# Volume Group operations
vgcreate devops-vg /dev/loop4
vgextend devops-vg /dev/nvme1n1

# Logical Volume operations
lvcreate -L 500M -n app-data devops-vg
lvextend -L +200M /dev/devops-vg/app-data

# Filesystem operations
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
resize2fs /dev/devops-vg/app-data
```

---

## What I Learned

What I Learned


1. *LVM Architecture*: LVM provides flexible storage management through Physical Volumes (PV), Volume Groups (VG), and Logical Volumes (LV).
2. *Volume Group Expansion*: A Volume Group can be expanded by adding new disks without affecting existing data, making storage scaling easier.
3. *Dynamic Extension*: Logical Volumes can be extended dynamically, and the filesystem can be resized without recreating partitions.
4. *Solving Storage Issues with EBS*: When facing insufficient storage issues, I was able to attach a new EBS volume to the EC2 instance and integrate it into the existing LVM Volume Group without any downtime, demonstrating the power of LVM for scalable infrastructure management.
---

## LVM Architecture Diagram

```text
EBS Volume (/dev/nvme1n1)
          ↓
Physical Volume (PV)
          ↓
Volume Group (devops-vg)
          ↓
Logical Volume (app-data)
          ↓
ext4 Filesystem
          ↓
Mounted at /mnt/app-data
```

---

## Why This Matters for DevOps

* **Flexible storage management** - Allocate and manage storage dynamically
* **Easy disk expansion** - Add new disks to existing volume groups
* **Better utilization of storage resources** - No need for partition resizing
* **Commonly used in Linux servers and cloud environments** - Industry standard practice
* **Useful for databases, logs, and application storage** - Critical for production systems
