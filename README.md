# Linux User Management & File Permissions Lab
This README walks you through a hands-on Linux lab simulating a real-world 
system administration scenario at a growing technology
company. In this lab, we set up 
user accounts, groups, and file permissions for two departments **(Marketing 
and IT)** using a Kali Linux virtual machine. The obective of the lab was to
understand how to manage users and groups, control file ownership, and apply 
the correct permissions to keep files secure.

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
**What I learned here:** `usermod -aG` appends the user to the specified group without removing them from other groups.

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
**What I learned here:** `chown` changes the owner of the file to the respective user.

#### 7: Set File Permissions (700)
```bash
sudo chmod 700 /home/shared/marketing/alice_report.txt
sudo chmod 700 /home/shared/marketing/bob_report.txt
sudo chmod 700 /home/shared/marketing/carol_report.txt
sudo chmod 700 /home/shared/marketing/david_report.txt
sudo chmod 700 /home/shared/marketing/emma_report.txt
```
**Notes:**`chmod 700` gives the owner full permissions (rwx) while the group and others have no access (---).

**In Summary:(r-4, w-2, x-1)** 

| Number | Who | Permissions |
|--------|-----|-------------|
| 7 | Owner | rwx |
| 0 | Group | --- |
| 0 | Others | --- |

---


### Part 2: The IT Department

#### 1: Created the IT Group
```bash
sudo groupadd itdept
```

#### 2: Created 5 IT Users for the IT Department (frank_it, grace_it, henry_it, iris_it, and jack_it)
```bash
sudo useradd -m frank_it
sudo useradd -m grace_it
sudo useradd -m henry_it
sudo useradd -m iris_it
sudo useradd -m jack_it
```

#### 3: Added the Users to the IT Group
```bash
sudo usermod -aG itdept frank_it
sudo usermod -aG itdept grace_it
sudo usermod -aG itdept henry_it
sudo usermod -aG itdept iris_it
sudo usermod -aG itdept jack_it
```

#### 4: Created the Shared IT Directory
```bash
sudo mkdir -p /home/shared/itdept
```

#### 5: Created the Shared Project File (project_specs.txt)
```bash
sudo touch /home/shared/itdept/project_specs.txt
```

#### 6: Set Group Ownership
```bash
sudo chown :itdept /home/shared/itdept/project_specs.txt
```
**What I learned here:** Using `:itdept` (with no user before the colon) changes only the **group owner** of the file without modifying the user owner.


#### 7: Set File Permissions (770)
```bash
sudo chmod 770 /home/shared/itdept/project_specs.txt
```
**Notes:**`chmod 770` gives the owner and group full permissions (rwx) while others have no access (---).

| Number | Who | Permissions |
|--------|-----|-------------|
| 7 | Owner | rwx |
| 7 | Group | rwx |
| 0 | Others | --- |

**Verified My Results:** to see the groups, their users, the files and permissions
```bash
ls -l /home/shared/marketing
ls -l /home/shared/itdept
getent group marketing
getent group itdept
```


## Screenshots of Results
![linux User Management   File Permissions Lab](https://github.com/user-attachments/assets/26d5ca83-ca59-40e3-a981-ffc33122e533)

All files created

![groups](https://github.com/user-attachments/assets/1934fe4f-f9e0-4f23-ad1f-5846db11ac99)

The two groups and their users

![files](https://github.com/user-attachments/assets/c0523472-7c15-4ed8-9050-12cf810f2f73)

All files in their respective directories and their permissions


## Key Observations / Lessons Learned

- **The `-aG` flag matters:** When adding a user to a group, leaving out `-a` 
would remove them from all their existing groups

- **Permission numbers are logical:** Once I understood that read=4, write=2, 
execute=1, the numbers made sense. 7 means full access, 0 means none, no memorization needed 😂

- **Real-World Application:** I now understand why companies have strict file 
permissions, one wrong setting could expose private files to everyone on the network
