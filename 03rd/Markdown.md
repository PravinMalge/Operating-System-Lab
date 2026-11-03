# Practical 03: Tracing System Calls using `strace`

## 🎯 Objective
To understand how user-space applications interact with the Linux kernel by tracing system calls using the `strace` utility on a simple C program.

---

## 💻 Code Implementation

### `hello.c`
```c
#include <stdio.h>

int main() {
    printf("Hello Duniya\n");
    return 0;
}
```

---

## ⚙️ Steps and Terminal Execution

### Step 1: Check `strace` Installation and Version
```bash
strace --version
```
**Output / Observation:**
```text
strace -- version 6.19
Copyright (c) 1991-2026 The strace developers https://strace.io.
This is free software; see the source for copying conditions.
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/e5febeff-f646-47a1-99db-7ee624c9341a" />


---

### Step 2: Write, Compile, and Execute C Program
1. Create and edit source file:
   ```bash
   nano hello.c
   ```
2. Compile using GCC:
   ```bash
   gcc hello.c -o hello
   ```
3. Run executable:
   ```bash
   ./hello
   ```
**Output:**
```text
Hello Duniya
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/9de3f20c-fa55-4e69-bf94-388ecd7e0ca6" />


---

### Step 3: Trace System Calls during Execution
Trace system call invocations for the binary:
```bash
strace ./hello
```
**Key System Calls Observed:**
- `execve()` - Program execution initialization.
- `openat()`, `read()`, `fstat()`, `close()` - Dynamic linking and shared library operations (`libc.so.6`).
- `mmap()`, `mprotect()`, `brk()` - Memory allocation and protection setup.
- `write(1, "Hello Duniya\n", 13)` - Output operation to stdout.
- `exit_group(0)` - Process termination.

> 📸 **Screenshot:**
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/3fc3d837-fc32-45e7-9d8c-80e607b81c9b" />


---

### Step 4: Display Summary of System Calls
Generate a comparative performance profile and call counts:
```bash
strace -c ./hello
```
**Output Summary Table:**
```text
% time     seconds  usecs/call      calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 39.46    0.000103          25         4           mprotect
 21.67    0.000053           7         7           mmap
  6.51    0.000017           5         3           brk
  6.13    0.000016           5         5           munmap
  5.75    0.000015           5         3           fstat
  5.30    0.000014           1        14           close
  3.07    0.000008           8         1           write
  3.07    0.000008           8         1           set_tid_address
  2.68    0.000007           7         1           prlimit64
  2.30    0.000006           6         1           getrandom
  2.30    0.000006           6         1           rseq
  1.92    0.000005           2         2           set_robust_list
  0.00    0.000000           0         1        1 faccessat
  0.00    0.000000           0         2           openat
  0.00    0.000000           0         1           read
  0.00    0.000000           0         1           execve
------ ----------- ----------- --------- --------- ----------------
100.00    0.000261                    56        1 total
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/491100e5-9530-4708-9003-85ab24ffa689" />


---

### Step 5: Redirect `strace` Output to File
Save system call details for analysis:
```bash
strace -o trace.txt ./hello
cat trace.txt
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="5" src="https://github.com/user-attachments/assets/c28eff2c-5445-4a8b-9f31-0aafec5d5219" />


---

## 📊 Key System Calls Summary Table

| System Call | Purpose / Description |
| :--- | :--- |
| `execve` | Executes the specified program binary (`./hello`). |
| `openat` / `read` / `close` | Opens, reads library header metadata (`libc.so.6`), and closes descriptor. |
| `mmap` / `munmap` | Maps files or devices into process memory space. |
| `mprotect` | Controls access permissions for mapped memory regions. |
| `brk` | Allocates virtual memory dynamically on the heap. |
| `write` | Writes data (`Hello Duniya\n`) to standard output file descriptor `1`. |
| `exit_group` | Exits all threads in the process group smoothly. |

---

## 🏁 Conclusion
The experiment successfully demonstrates system call execution and tracing using `strace`. It verifies how user-level program instructions trigger lower-level kernel operations to perform execution, memory allocation, and I/O tasks.
