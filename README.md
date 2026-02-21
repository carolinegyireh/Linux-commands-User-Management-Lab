# Linux User Management & File Permissions Lab
This readme walks you through 

## Objective
The objective of this lab is to set up user accounts, groups, and file permissions for two departments (Marketing and IT) on a Linux system, simulating a real-world sysadmin scenario for a growing Tech Company.

## Tools Used
- Kali Linux (Virtual Machine)

## Step-by-Step Process

### Part 1: The Marketing Department

#### 1: Create the Marketing Group using
```bash
sudo groupadd marketing
```

#### 2: Created 5 Marketing Users (alice_m, bob_m, carol_m, david_m, and emma_m)
```bash
sudo useradd -m alice_m
sudo useradd -m bob_m
sudo useradd -m carol_m
sudo useradd -m david_m
sudo useradd -m emma_m
```
**Notes:** Run code for one user at a time

#### 3: Added All Users to the Marketing Group
```bash
sudo usermod -aG marketing alice_m
sudo usermod -aG marketing bob_m
sudo usermod -aG marketing carol_m
sudo usermod -aG marketing david_m
sudo usermod -aG marketing emma_m
```
**What I lerned here:** `usermod -aG` appends the user to the specified group without removing them from other groups.

#### 4: Created the Shared Marketing Directory
```bash
sudo mkdir -p /home/shared/marketing
```
**What I lerned here:** `mkdir -p` creates the directory and any missing parent directories in the path and when run without it caused errors

#### 5: Created Personal Files for Each User
```bash
sudo touch /home/shared/marketing/alice_report.txt
sudo touch /home/shared/marketing/bob_report.txt
sudo touch /home/shared/marketing/carol_report.txt
sudo touch /home/shared/marketing/david_report.txt
sudo touch /home/shared/marketing/emma_report.txt
```

#### 6: Set File Ownership for each user to be the owner of their respective files
```bash
sudo chown alice_m /home/shared/marketing/alice_report.txt
sudo chown bob_m /home/shared/marketing/bob_report.txt
sudo chown carol_m /home/shared/marketing/carol_report.txt
sudo chown david_m /home/shared/marketing/david_report.txt
sudo chown emma_m /home/shared/marketing/emma_report.txt
```
**What I lerned here:** `chown` changes the owner of the file to the respective user.

#### 7: Set File Permissions (700)
```bash
sudo chmod 700 /home/shared/marketing/alice_report.txt
sudo chmod 700 /home/shared/marketing/bob_report.txt
sudo chmod 700 /home/shared/marketing/carol_report.txt
sudo chmod 700 /home/shared/marketing/david_report.txt
sudo chmod 700 /home/shared/marketing/emma_report.txt
```
**Notes: **`chmod 700` gives the owner full permissions (rwx) while the group and others have no access (---).

**In Summary:(r-4, w-2, x-1)** 

| Number | Who | Permissions |
|--------|-----|-------------|
| 7 | Owner | rwx |
| 0 | Group | --- |
| 0 | Others | --- |

---
