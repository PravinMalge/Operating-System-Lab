# Practical 08: Memory and Swap Usage Monitoring (`free`, `vmstat`)

## 🎯 Objective

To observe, monitor, and analyze system memory (RAM) and swap space utilization in Linux using the `free` and `vmstat` command-line utilities.

---

## 🛠️ Tools & Environment

- **Operating System:** Ubuntu Linux (VirtualBox / Native)
- **Shell:** Bash Terminal
- **Core Commands:** `free`, `vmstat`

---

## ⚙️ Step-by-Step Practical Execution

### Experiment 1: Observe Memory Usage using `free`

The `free` command displays the total amount of free and used physical memory and swap memory in the system, as well as the buffers and caches used by the kernel.

#### Step 1: Open Terminal & Display Default Memory Usage
Execute the basic `free` command to display memory values in kilobytes (KB):
```bash
free
```

**Observed Output:**
```text
              total        used        free      shared  buff/cache   available
Mem:        7576224     3672436      714976      128120     3221660     3903700
Swap:       4194300           0     4194300
```

#### Step 2: Display Values in Human-Readable Format
Use the `-h` flag to convert byte counts into human-readable units (GiB, MiB):
```bash
free -h
```

**Observed Output:**
```text
              total        used        free      shared  buff/cache   available
Mem:          7.2Gi       3.4Gi       816Mi       123Mi       3.1Gi       3.8Gi
Swap:         4.0Gi          0B       4.0Gi
```

#### Step 3: Continuously Refresh Memory Statistics
Use the `-s` flag to refresh statistics continuously at a specified interval (e.g., every 2 seconds). Press `Ctrl + C` to stop execution:
```bash
free -h -s 2
```

**Observed Output (Streaming Snapshot):**
```text
              total        used        free      shared  buff/cache   available
Mem:          7.2Gi       3.4Gi       754Mi       121Mi       3.1Gi       3.8Gi
Swap:         4.0Gi          0B       4.0Gi

              total        used        free      shared  buff/cache   available
Mem:          7.2Gi       3.4Gi       753Mi       121Mi       3.1Gi       3.8Gi
Swap:         4.0Gi          0B       4.0Gi
```

#### Step 4: Display Memory Statistics in Megabytes
Use the `-m` flag to output memory metrics in megabytes (MB):
```bash
free -m
```

**Observed Output:**
```text
              total        used        free      shared  buff/cache   available
Mem:           7390        3467         804         121        3136        3930
Swap:          4095           0        4095
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/a802cfa7-c991-45d0-a2f4-8f9234995e49" />


---

### Experiment 2: Observe Memory and Swap Activity using `vmstat`

The `vmstat` (Virtual Memory Statistics) tool reports information about processes, memory, paging, block I/O, traps, and CPU activity.

#### Step 1: Display Virtual Memory Summary
Run `vmstat` without arguments to get a cumulative summary of system activity since the last system boot:
```bash
vmstat
```

**Observed Output:**
```text
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 2  1      0 778328  46240 3165168   0    0    51    72  755 5090 21 14  5 61  0  0
```

#### Step 2: Refresh Statistics at Intervals
Display updated virtual memory reports every 2 seconds:
```bash
vmstat 2
```

#### Step 3: Display Fixed Number of Reports
Limit the report to a fixed count (e.g., 5 reports at 2-second intervals):
```bash
vmstat 2 5
```

**Observed Output:**
```text
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0 709844  46304 3165380   0    0  4923     6  252 2424 26 92 11 38  6  0
 0  0      0 779804  46328 3165296   0    0     0    58 3317 4183 10 38  0  0  0  0
 1  0      0 795352  46344 3165244   0    0     0  4767 6487 16  5 79  8  0  0  0  0
 0  0      0 611272  46344 3265212   0    0     0  3078 3475  7 39  0 60  0  0  0  0
 0  0      0 771292  46296 3171440   0    0    54 22233 40385 17 10 73  8  0  0
```

#### Step 4: Display Memory Statistics in Megabytes
Use the `-S M` flag to format the `vmstat` output fields in megabytes:
```bash
vmstat -S M
```

**Observed Output:**
```text
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0    798     45   3091    0    0    48    70  738 5037 21 13  5 62  0  0
```

> 📸 **Screenshot:**
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/2221f47f-3ac0-4b0f-8f0b-7e008d7af723" />


---

## 📊 Observation Table

| Sr. No. | Command | RAM Observed | Swap Observed | Key Insights |
| :---: | :--- | :--- | :--- | :--- |
| **1** | `free -h` | **Total:** 7.2Gi<br>**Used:** 3.4Gi<br>**Free:** 816Mi | **Total:** 4.0Gi<br>**Used:** 0B<br>**Free:** 4.0Gi | Shows overall memory distribution in human-readable units. |
| **2** | `free -m` | **Total:** 7390 MB<br>**Used:** 3467 MB<br>**Free:** 804 MB | **Total:** 4095 MB<br>**Used:** 0 MB<br>**Free:** 4095 MB | Provides exact memory allocations in megabytes. |
| **3** | `vmstat` | **Free:** 778328 KB<br>**Cache:** 3165168 KB | **swpd:** 0 KB<br>**si:** 0, **so:** 0 | Summarizes system memory, swap paging, and CPU utilization. |
| **4** | `vmstat 2 5` | **Free:** 771292 KB (final reading) | **swpd:** 0 KB | Real-time monitoring of memory paging and CPU state. |

---

## 🏁 Conclusion

Memory and swap space monitoring commands (`free` and `vmstat`) were successfully executed. The observations confirm that the Linux kernel actively uses idle RAM for filesystem buffering and caching (`buff/cache`), while maintaining zero swap space utilization (`swpd: 0`).
