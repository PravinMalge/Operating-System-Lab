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
> ![Create User](assets/1.png)

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
> ![View User Information](assets/2.png)

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
> ![Create Group](assets/3.png)

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
> ![Add User to Group](assets/4.png)

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

---

### Experiment 7: Delete User Account
Remove user `student1` from the system:

```bash
sudo userdel student1
```

---

### Experiment 8: Delete Group
Delete group `labgroup` from the system:

```bash
sudo groupdel labgroup
```

> 📸 **Screenshot Placeholder:**
> ![Delete User and Group](assets/5.png)

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