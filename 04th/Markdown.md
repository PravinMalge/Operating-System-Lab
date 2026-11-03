# Practical 04: Process Management & Monitoring in Linux

## 🎯 Objective

To understand and execute Linux process management and monitoring utilities, including displaying process details (`ps`), interactive system monitoring (`top`), inspecting background tasks, and terminating processes (`kill`).

---

## 🛠️ Tools & Environment

- **Operating System:** Ubuntu Linux
- **Shell:** Bash Terminal
- **Commands Covered:** `ps`, `top`, `sleep`, `pgrep`, `kill`

---

## ⚙️ Step-by-Step Practical Tasks

### Task A: Display Processes using `ps`

1. **Display processes linked to the current terminal:**
   ```bash
   ps
   ```
   **Observation:** Shows the PID, TTY, time, and command name for processes running in the current terminal session (e.g., `bash`, `ps`).

2. **Display all processes in full format:**
   ```bash
   ps -ef
   ```
   **Observation:** Lists all system processes with details such as UID, PID, PPID, execution start time, TTY, CPU time, and command parameters.

   > 📸 **Screenshot:**
   > ![ps and ps -ef execution](assets/1.png)

3. **Display process owner, PID, CPU, and memory information:**
   ```bash
   ps aux
   ```
   **Observation:** Displays detailed resource consumption (percentage of CPU `%CPU` and memory `%MEM`, virtual size `VSZ`, resident set size `RSS`, and process state `STAT`) for all processes.

4. **Display only processes owned by the logged-in user:**
   ```bash
   ps -u "$USER"
   ```
   **Observation:** Filters and lists processes owned by the currently active user account.

   > 📸 **Screenshot:**
   > ![ps aux and ps -u USER execution](assets/2.png)

---

### Task B: Monitor Processes using `top`

1. **Run the dynamic real-time system monitor:**
   ```bash
   top
   ```

2. **Observe system summary and process list:**
   - Monitor total CPU usage, memory usage, swap memory status, process states (running, sleeping, zombie), and process IDs.

3. **Interactive Keyboard Shortcuts in `top`:**
   - `q` — Quit `top`.
   - `P` — Sort processes by CPU usage.
   - `M` — Sort processes by memory usage.
   - `1` — Toggle display of individual CPU cores.

   > 📸 **Screenshot:**
   > ![top system monitor](assets/3.png)

---

### Task C: Create a Test Process and Inspect It

1. **Start a 10-minute sleep process in the background:**
   ```bash
   sleep 600 &
   ```
   *Note the returned Job ID and Process ID (PID) from the terminal prompt (e.g., `[1] 5002`).*

2. **Verify the process status:**
   ```bash
   ps -p <PID> -o pid,ppid,stat,%cpu,%mem,cmd
   ```

3. **Locate the process by command name:**
   ```bash
   pgrep -a sleep
   ```

---

### Task D: Terminate the Test Process using `kill`

1. **Send a graceful termination request (SIGTERM):**
   ```bash
   kill -TERM <PID>
   ```

2. **Check whether the process has exited:**
   ```bash
   ps -p <PID> -o pid,stat,cmd
   ```

3. **Force termination (SIGKILL) if the process remains active:**
   ```bash
   kill -KILL <PID>
   ```

   > 📸 **Screenshot:**
   > ![Process creation, inspection, and termination](assets/4.png)

---

## 📊 Summary Table of Process Commands

| Command | Usage / Purpose | Key Options |
| :--- | :--- | :--- |
| **`ps`** | Displays a snapshot of current processes | `-ef`, `aux`, `-u $USER` |
| **`top`** | Dynamic real-time process & resource monitoring | `P` (CPU), `M` (Memory), `q` (Quit) |
| **`sleep`** | Suspends execution for a specified duration | `sleep 600 &` (Runs in background) |
| **`pgrep`** | Looks up processes by name/pattern | `-a` (Displays full command) |
| **`kill`** | Sends signals to terminate processes | `-TERM` (Graceful), `-KILL` (Forceful) |

---

## 🏁 Conclusion

The practical experiment successfully covered process management and resource monitoring utilities in Linux. The lifecycle of processes—creation, state inspection, resource tracking, and termination—was demonstrated and logged.