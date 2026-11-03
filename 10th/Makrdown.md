# Practical 10: User and Group Administration in Linux

## 🎯 Objective

To learn and execute administrative operations for user and group management in Linux, including creating user accounts, configuring passwords, managing groups, modifying memberships, and removing accounts/groups using superuser privileges.

## 🛠️ Tools & Environment

* **Operating System:** Ubuntu Linux (VirtualBox / Native)
* **Shell:** Bash Terminal
* **Core Commands:** `useradd`, `passwd`, `id`, `getent`, `groupadd`, `usermod`, `gpasswd`, `userdel`, `groupdel`

---

## ⚙️ Step-by-Step Experiments

### Experiment 1: Create a New User
Create a new user named `student1` with a default home directory, and assign an authentication password:

```bash
sudo useradd -m student1
sudo passwd student1
```

**Output / Observation:**
```text
New password:
Retype new password:
passwd: password updated successfully
```

> 📸 **Screenshot Placeholder:**
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/f5366e3b-5b62-47ff-a638-de47cb0cd542" />


---

### Experiment 2: View User Information
Inspect identity metrics, UID, GID, group associations, and system account records for `student1`:

1. **Check user identity and numerical IDs:**
   ```bash
   id student1
   ```
   **Output:**
   ```text
   uid=1001(student1) gid=1001(student1) groups=1001(student1)
   ```

2. **Retrieve account configuration entry from `/etc/passwd`:**
   ```bash
   getent passwd student1
   ```
   **Output:**
   ```text
   student1:x:1001:1001::/home/student1:/bin/sh
   ```

> 📸 **Screenshot Placeholder:**
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/33d31dd9-5ea8-4d60-af84-2478cc2e9f32" />


---

### Experiment 3: Create a System Group
Create a new supplementary group named `labgroup` and verify its existence:

1. **Create group:**
   ```bash
   sudo groupadd labgroup
   ```

2. **Verify group creation entry from `/etc/group`:**
   ```bash
   getent group labgroup
   ```
   **Output:**
   ```text
   labgroup:x:1002:
   ```

> 📸 **Screenshot Placeholder:**
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/50c35ea8-13cb-4657-b847-f28b77480f27" />


---

### Experiment 4: Add User to a Supplementary Group
Append user `student1` to the newly created `labgroup` without removing existing group associations:

```bash
sudo usermod -aG labgroup student1
groups student1
id student1
```

**Output / Observation:**
```text
student1 : student1 labgroup
uid=1001(student1) gid=1001(student1) groups=1001(student1),1002(labgroup)
```

> 📸 **Screenshot Placeholder:**
<img width="1440" height="900" alt="4" src="https://github.com/user-attachments/assets/db954cc6-fe7d-48ac-8493-d69906b5a2d4" />


---

### Experiment 5: Remove User from a Supplementary Group
Remove `student1` from the supplementary group `labgroup`:

```bash
sudo gpasswd -d student1 labgroup
```

**Output / Observation:**
```text
Removing user student1 from group labgroup
```
<img width="1440" height="900" alt="5" src="https://github.com/user-attachments/assets/7f7020e4-d25e-45fb-8ac6-6a8f0c46f4a6" />

---

### Experiment 6: Change User Password
Update or reset the password for account `student1`:

```bash
sudo passwd student1
```

**Output / Observation:**
```text
New password:
Retype new password:
passwd: password updated successfully
```
<img width="1440" height="900" alt="6" src="https://github.com/user-attachments/assets/7eb3c469-bf0f-4682-9b08-686c078be7e5" />

---


## 📊 Observation and Result Table

| Sr. No. | Task | Command Executed | Status / Observation |
| :---: | :--- | :--- | :--- |
| **1** | Create User `student1` | `sudo useradd -m student1` | User created successfully (`uid=1001`, home directory `/home/student1`). |
| **2** | Set Password | `sudo passwd student1` | Password updated successfully. |
| **3** | Create Group `labgroup` | `sudo groupadd labgroup` | Group created successfully (`gid=1002`). |
| **4** | Add User to Group | `sudo usermod -aG labgroup student1` | User added successfully (`groups=1001(student1),1002(labgroup)`). |
| **5** | Remove from Group | `sudo gpasswd -d student1 labgroup` | Removed `student1` from `labgroup`. |
| **6** | Delete User & Group | `sudo userdel student1`<br>`sudo groupdel labgroup` | User (`student1`) and group (`labgroup`) removed successfully. |

---

## 🏁 Conclusion

The user and group administration practical was successfully executed on Ubuntu Linux. The experiment verified account creation, group allocation, permission inheritance via supplementary groups, password administration, and resource cleanup.
