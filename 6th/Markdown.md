# Practical 06: Linux File Permissions and Ownership Management

## 🎯 Objective

To understand and manage Linux file permissions, numeric and symbolic permission modification (`chmod`), file ownership assignment (`chown`), user/group identity (`id`, `whoami`), and default file creation masks (`umask`).

## 🛠️ Tools & Environment

* **Operating System:** Ubuntu Linux (VirtualBox)
* **Shell:** Bash Terminal
* **Utilities Used:** `mkdir`, `touch`, `ls`, `chmod`, `chown`, `whoami`, `id`, `umask`, `sudo`

---

## ⚙️ Step-by-Step Experiments

### Experiment 1: Create a Test File & Inspect Initial Permissions

Set up a test directory, navigate into it, and inspect the default permission layout:

```bash
mkdir permission_lab
cd permission_lab
touch file.txt
ls -l file.txt
```

**Observation:** Displays default permissions assigned upon creation (e.g., `-rw-rw-r--`).

> 📸 **Screenshot:**
> 

---

### Experiment 2: Change Permissions Using Octal / Numeric Notation (`chmod`)

Modify file permissions using 3-digit octal codes representing User, Group, and Others:

1. **Set permissions to Read-Write for Owner, Read-Only for Group & Others (`644`):**
   ```bash
   chmod 644 file.txt
   ls -l file.txt
   ```

2. **Set executable permissions for Owner, Group, and Others (`755`):**
   ```bash
   chmod 755 file.txt
   ls -l file.txt
   ```

3. **Restrict all access to Owner only (`700`):**
   ```bash
   chmod 700 file.txt
   ls -l file.txt
   ```

> 📸 **Screenshot:**
> 

---

### Experiment 3: Change Permissions Symbolically

Modify permissions using user categories (`u`, `g`, `o`, `a`) and operators (`+`, `-`, `=`):

1. **Reset permission to `644`:**
   ```bash
   chmod 644 file.txt
   ```

2. **Add execute permission (`+x`) to User (`u`):**
   ```bash
   chmod u+x file.txt
   ls -l file.txt
   ```

3. **Remove execute permission (`-x`) from User:**
   ```bash
   chmod u-x file.txt
   ls -l file.txt
   ```

> 📸 **Screenshot:**
> 

---

### Experiment 4: Change File Ownership Using `chown`

Inspect user identities and transfer file ownership attributes to root using superuser privileges:

1. **Check current logged-in user and ID details:**
   ```bash
   whoami
   id
   ```

2. **Change file user owner to `root`:**
   ```bash
   sudo chown root file.txt
   ls -l file.txt
   ```

3. **Change both user owner and group owner to `root`:**
   ```bash
   sudo chown root:root file.txt
   ls -l file.txt
   ```

> 📸 **Screenshot:**
> 

---

### Experiment 5: Explore Default File Creation Mask (`umask`)

View and modify the system `umask` to control default permissions for newly created files and directories:

1. **View default `umask`:**
   ```bash
   umask
   ```

2. **Set `umask` to `022` and create test entries:**
   ```bash
   umask 022
   touch newfile.txt
   mkdir newdir
   ls -ld newfile.txt newdir
   ```

3. **Set restrictive `umask` to `027` and create private entries:**
   ```bash
   umask 027
   touch private.txt
   mkdir private_dir
   ls -ld private.txt private_dir
   ```

> 📸 **Screenshot:**
> 

---

## 📊 Experiment Observation Table

| Sr. No | Command / Test | Observed Permissions / Result | Description |
| :---: | :--- | :--- | :--- |
| **1** | `ls -l file.txt` | `-rw-rw-r--` | Initial default file permissions |
| **2** | `chmod 644 file.txt` | `-rw-r--r--` | Owner: `rw-`, Group: `r--`, Others: `r--` |
| **3** | `chmod 755 file.txt` | `-rwxr-xr-x` | Read, Write, Execute for Owner; Read & Execute for Group/Others |
| **4** | `chmod 700 file.txt` | `-rwx------` | Full control to Owner only; No access for Group/Others |
| **5** | `chmod u+x file.txt` | `-rwxr--r--` | Added execution bit (`+x`) for owner (`u`) |
| **6** | `sudo chown root file.txt` | `-rw-r--r-- 1 root pravin-malge` | User owner changed to `root` |
| **7** | `sudo chown root:root file.txt` | `-rw-r--r-- 1 root root` | User and group owner changed to `root` |
| **8** | `umask 022` | File: `-rw-r--r--`<br>Dir: `drwxr-xr-x` | Default mask granting read/execute to group and others |
| **9** | `umask 027` | File: `-rw-r-----`<br>Dir: `drwxr-x---` | Restrictive mask revoking all permissions for others |

---

## 🏁 Conclusion

The practical successfully demonstrated file access control mechanisms in Linux. We verified how octal and symbolic modes alter access levels, how ownership transfers via `chown`, and how `umask` dynamically controls default permissions for newly created files and folders.