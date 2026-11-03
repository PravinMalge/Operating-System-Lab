# Practical 05: Automated Archival Backup Scripting in Linux

## 🎯 Objective

To write, execute, and verify a Bash shell script that automates directory backups by creating compressed `.tar.gz` archive files with dynamic timestamps, verifying file contents, and conducting a restoration test.

## 🛠️ Tools & Environment

* **Operating System:** Ubuntu Linux (VirtualBox)
* **Shell:** Bash Terminal
* **Utilities Used:** `bash`, `nano`, `chmod`, `tar`, `ls`, `mkdir`, `find`

---

## ⚙️ Step-by-Step Practical Tasks

### Step 1: Create a Test Directory and Files

Set up a test directory structure with sample files to back up:

```bash
mkdir -p "$HOME/backup_lab/source"
echo "Operating Systems lab backup test" > "$HOME/backup_lab/source/notes.txt"
mkdir -p "$HOME/backup_lab/source/docs"
echo "Sample document" > "$HOME/backup_lab/source/docs/sample.txt"
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/703a0f2b-f697-48e4-bb6a-88f06ea096cf" />


---

### Step 2: Create the Backup Script

Create and edit the shell script `backup.sh`:

```bash
touch backup.sh
nano backup.sh
```

#### 📜 Script Content (`backup.sh`):

```bash
#!/bin/bash

# Assign source and destination directories from arguments
SOURCE_DIR="$1"
BACKUP_DIR="$2"

# Check if arguments are provided
if [ -z "$SOURCE_DIR" ] || [ -z "$BACKUP_DIR" ]; then
    echo "Usage: $0 <source_directory> <backup_destination>"
    exit 1
fi

# Verify if source directory exists
if [ ! -d "$SOURCE_DIR" ]; then
    echo "Error: Source directory does not exist: $SOURCE_DIR"
    exit 1
fi

# Create backup destination directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Check if backup destination directory is writable
if [ ! -w "$BACKUP_DIR" ]; then
    echo "Error: Backup destination is not writable: $BACKUP_DIR"
    exit 1
fi

# Extract source folder name and generate timestamped archive filename
SOURCE_NAME="$(basename "$SOURCE_DIR")"
TIMESTAMP="$(date +%Y%m%d_%H%M%S)"
ARCHIVE="$BACKUP_DIR/${SOURCE_NAME}_backup_${TIMESTAMP}.tar.gz"

# Create the compressed tar archive
tar -czf "$ARCHIVE" -C "$(dirname "$SOURCE_DIR")" "$SOURCE_NAME"

# Verify archive creation success
if [ $? -eq 0 ]; then
    echo "Backup completed successfully."
    echo "Source: $SOURCE_DIR"
    echo "Backup file: $ARCHIVE"
else
    echo "Error: Backup failed."
    exit 1
fi
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/ddbaea8f-fd6e-4a5e-9190-a3c2ee175b51" />
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/b1274493-a804-4c12-902d-3da5c2ed943a" />


---

### Step 3: Make the Script Executable

Grant execution permissions to the script:

```bash
chmod +x backup.sh
```

---

### Step 4: Run the Backup Script

Execute the script by passing the source and destination paths:

```bash
./backup.sh "$HOME/backup_lab/source" "$HOME/backup_lab/backups"
```

**Output / Observation:**
```text
Backup completed successfully.
Source: /home/pravin-malge/backup_lab/source
Backup file: /home/pravin-malge/backup_lab/backups/source_backup_20261023_151713.tar.gz
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="4" src="https://github.com/user-attachments/assets/52cc6cc3-40bd-4839-bfe0-8df896bdfa9a" />


---

### Step 5: Verify the Backup Archive

Check the created archive file and list its contents without extracting:

1. **Check archive details:**
   ```bash
   ls -lh "$HOME/backup_lab/backups"
   ```

2. **Inspect contents inside the compressed archive:**
   ```bash
   tar -tzf "$HOME/backup_lab/backups/source_backup_20261023_151713.tar.gz"
   ```

**Output / Observation:**
```text
source/
source/docs/
source/docs/sample.txt
source/notes.txt
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="5" src="https://github.com/user-attachments/assets/c71eb79f-9931-431f-8dff-84acb44ea04b" />


---

### Step 6: Restoration Test

Test restoring files from the `.tar.gz` archive into a separate restore directory:

1. **Create restore target folder:**
   ```bash
   mkdir -p "$HOME/backup_lab/restore_test"
   ```

2. **Extract archive:**
   ```bash
   tar -xzf "$HOME/backup_lab/backups/source_backup_20261023_151713.tar.gz" -C "$HOME/backup_lab/restore_test"
   ```

3. **Verify restored files:**
   ```bash
   find "$HOME/backup_lab/restore_test" -type f
   ```

**Output / Observation:**
```text
/home/pravin-malge/backup_lab/restore_test/source/docs/sample.txt
/home/pravin-malge/backup_lab/restore_test/source/notes.txt
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="6" src="https://github.com/user-attachments/assets/aa989be4-2de3-4f40-8cff-7d552347417c" />


---

## 📊 Summary Table of Backup Script Flags & Commands

| Command / Flag | Function | Description |
| :--- | :--- | :--- |
| `tar -czf` | Create Compressed Archive | `-c` (create), `-z` (gzip compression), `-f` (filename specification). |
| `tar -tzf` | List Archive Contents | `-t` (list files inside archive without extracting). |
| `tar -xzf` | Extract Archive | `-x` (extract), `-C` (specify destination target folder). |
| `date +%Y%m%d_%H%M%S` | Dynamic Timestamp | Generates current date and time string for unique file naming. |
| `chmod +x` | Permission Change | Adds execution flags to `backup.sh`. |

---

## 🏁 Conclusion

The practical experiment successfully demonstrated shell scripting for automated system backups. The execution script verified path existence, permissions, archive creation using `tar`, contents inspection, and successful file extraction.
