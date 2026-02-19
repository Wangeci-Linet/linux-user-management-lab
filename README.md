# :penguin: Linux User Management Lab - TechCorp Solutions

## :pushpin: User Management and File Permissions Lab

---

## :dart: Objective
This lab demonstrates practical Linux system administration by creating users, managing groups and assigning file permisssions for two departments: Marketing and IT.
It ensures secure file access, privacy of individual users and collaborative group work using Linux permission structures.

---

## :hammer_and_wrench: Tools Used

- Kali Linux
- Linux Terminal (Bash)
- GitHub
- Screenshot tool

---

# :desktop_computer: PART 1: Marketing Department (Private Files)

### Scenario
The Marketing department has five new employees. Each employee requires a personal workspace file that only they can access.

---

## Step 1: Create Marketing Group
```bash
sudo groupadd marketing
```
![Marketing Group](screenshots/01-marketing-group.png)

## Step 2: Create Marketing Users
```bash
sudo useradd -m -G marketing -s /bin/bash alice_m
sudo useradd -m -G marketing -s /bin/bash bob_m
sudo useradd -m -G marketing -s /bin/bash carol_m
sudo useradd -m -G marketing -s /bin/bash david_m
sudo useradd -m -G marketing -s /bin/bash emma_m
```
![Marketing Users](screenshots/02-marketing-users.png)

## Step 3: Create Marketing Shared Directory
```bash
sudo mkdir -p /home/shared/marketing
sudo chown root:marketing /home/shared/marketing
sudo chown 770 /home/shared/marketing
```
![Marketing Directory](screenshots/03-marketing-directory.png)

## Step 4: Create Individual User Files
```bash
sudo touch /home/shared/marketing/alice_report.txt 
sudo touch /home/shared/marketing/bob_report.txt
sudo touch /home/shared/marketing/carol_report.txt
sudo touch /home/shared/marketing/david_report.txt
sudo touch /home/shared/marketing/emma_report.txt
```


## Step 5: Assign Ownership to Users
```bash
sudo chown alice_m:marketing /home/shared/marketing/alice_report.txt
sudo chown bob_m:marketing /home/shared/marketing/bob_report.txt
sudo chown carol_m:marketing /home/shared/marketing/carol_report.txt
sudo chown david_m:marketing /home/shared/marketing/david_report.txt
sudo chown emma_m:marketing /home/shared/marketing/emma_report.txt
```


## Step 6: Set Private Permissions (700)
```bash
sudo chmod 700 /home/shared/marketing/*.txt
```


---

# :desktop_computer: PART 2: IT Department (Shared Collaborative File)

### Scenario
The IT department needs a shared project file where all team members can collaborate.

---

## Step 1: Create IT Group
```bash
sudo groupadd itdept
```


## Step 2: Create IT Users
```bash
sudo useradd -m -G itdept -s /bin/bash frank_it
sudo useradd -m -G itdept -s /bin/bash grace_it
sudo useradd -m -G itdept -s /bin/bash henry_it
sudo useradd -m -G itdept -s /bin/bash iris_it
sudo useradd -m -G itdept -s /bin/bash jack_it
```


## Step 3: Create IT Shared Directory
```bash
sudo mkdir -p /home/shared/itdept
sudo chown root:itdept /home/shared/itdept
sudo chmod 770 /home/shared/itdept
```


## Step 4: Create Shared Project File
```bash
sudo touch /home/shared/itdept/project_specs.txt
```


## Step 5: Assign Group Ownership
```bash
sudo chown :itdept /home/shared/itdept/project_specs.txt
```


## Step 6: Set Shared Permissions (770)
```bash
sudo chmod 770 /home/shared/itdept/project_specs.txt
```


---

# :camera: Verification Commands

## Verify
```bash
cat /etc/passwd
```


## Verify Groups
```bash
getent group marketing
getent group itdept
```


## Verify Marketing Files and Permissions
```bash
ls -l /home/shared/marketing/
```


## Verify IT Files and Permissions
```bash
ls -l /home/shared/itdept
```


---

# :brain: Key Observations/Lessons Learned

- **Linux user and group management is fundamental to system security.** Proper configuration ensures that only authorized users can access specific resources within an organization.
- **Group-based access control simplifies administration.** Instead of assigning permissions individually, users can be managed collectively through groups such as marketing and itdept.
- **File ownership directly determines access control.** Assigning correct ownership using chown ensures that files are controlled by the intended users or groups.
- **Permission modes enforce confidentiality and collaboration.**
  *  Permission **700** guarantees complete privacy by allowing only the file owner to read, write and execute.
  *  Permission **770** enables secure collaboration by granting full access to the owner and group while denying others.
- **Directory permissions affect file accessibility.** Even if a file has correct permissions, users cannot access it without proper directory permissions.
- **Verification commands are essential in system administration.** Commands such as ls -l, cat /etc/passwd, and getent group help confirm that configurations are correctly implemented.
- **Practical implementation improves Linux administration skills.** This lab strengthens real-world competencies in user management, permission setting, and secure system configuration used in cybersecurity.
- **Attention to detail is critical.** Small mistakes in usernames, group assignments, or permission values can lead to access failures or security vulnerabilities.

