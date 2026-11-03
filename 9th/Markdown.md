# Practical 09: Page Replacement Algorithms (FIFO and LRU)

## 🎯 Objective

To simulate and analyze virtual memory management page replacement algorithms—specifically First-In-First-Out (FIFO) and Least Recently Used (LRU)—in C to evaluate page faults and hit ratios.

## 🛠️ Tools & Environment

* **Operating System:** Ubuntu Linux (VirtualBox / Native)
* **Compiler:** GCC (GNU Compiler Collection)
* **Text Editor:** `nano` / VS Code

---

## 💻 Code Implementation

### `page_replacement.c`

```c
#include <stdio.h>

#define MAX 100

void fifo(int p[], int n, int f) {
    int a[MAX], next = 0, faults = 0, hit;
    for (int i = 0; i < f; i++) a[i] = -1;

    printf("\nFIFO Page Replacement:\n");
    for (int i = 0; i < n; i++) {
        hit = 0;
        for (int j = 0; j < f; j++) {
            if (a[j] == p[i]) {
                hit = 1;
                break;
            }
        }
        if (!hit) {
            a[next] = p[i];
            next = (next + 1) % f;
            faults++;
            printf("Page %d: ", p[i]);
            for (int j = 0; j < f; j++) {
                if (a[j] != -1) printf("%d ", a[j]);
            }
            printf("(Fault)\n");
        } else {
            printf("Page %d: ", p[i]);
            for (int j = 0; j < f; j++) {
                if (a[j] != -1) printf("%d ", a[j]);
            }
            printf("(Hit)\n");
        }
    }
    printf("Total FIFO page faults: %d\n", faults);
}

void lru(int p[], int n, int f) {
    int a[MAX], used[MAX], time = 0, faults = 0, hit, victim;
    for (int i = 0; i < f; i++) {
        a[i] = -1;
        used[i] = -1;
    }

    printf("\nLRU Page Replacement:\n");
    for (int i = 0; i < n; i++) {
        time++;
        hit = 0;
        for (int j = 0; j < f; j++) {
            if (a[j] == p[i]) {
                hit = 1;
                used[j] = time;
                break;
            }
        }
        if (!hit) {
            victim = 0;
            for (int j = 0; j < f; j++) {
                if (a[j] == -1) {
                    victim = j;
                    break;
                }
                if (used[j] < used[victim]) {
                    victim = j;
                }
            }
            a[victim] = p[i];
            used[victim] = time;
            faults++;
            printf("Page %d: ", p[i]);
            for (int j = 0; j < f; j++) {
                if (a[j] != -1) printf("%d ", a[j]);
            }
            printf("(Fault)\n");
        } else {
            printf("Page %d: ", p[i]);
            for (int j = 0; j < f; j++) {
                if (a[j] != -1) printf("%d ", a[j]);
            }
            printf("(Hit)\n");
        }
    }
    printf("Total LRU page faults: %d\n", faults);
}

int main() {
    int n, f, p[MAX];

    printf("Enter number of page references (1-100): ");
    scanf("%d", &n);

    printf("Enter page reference string: ");
    for (int i = 0; i < n; i++) {
        scanf("%d", &p[i]);
    }

    printf("Enter number of frames (1-100): ");
    scanf("%d", &f);

    fifo(p, n, f);
    lru(p, n, f);

    return 0;
}
```

---

## ⚙️ Steps and Terminal Execution

### Step 1: Write and Save Source Code
Create the source file using `nano`:
```bash
nano page_replacement.c
```

> 📸 **Screenshot :**
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/ded3c474-7bcc-4f64-974b-6aefc25f4b42" />
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/f3c19429-f76d-4752-969a-accd23d4c92e" />



---

### Step 2: Compile Program
Compile using GCC compiler:
```bash
gcc page_replacement.c -o page_replacement
```

---

### Step 3: Run the Executable
Run the program with test inputs:
```bash
./page_replacement
```

**Input Parameters:**
- **Number of page references:** `7`
- **Page reference string:** `1 2 3 1 4 2 5`
- **Number of frames:** `3`

---

## 🖥️ Terminal Execution Output Log

```text
Enter number of page references (1-100): 7
Enter page reference string: 1 2 3 1 4 2 5
Enter number of frames (1-100): 3

FIFO Page Replacement:
Page 1: 1 (Fault)
Page 2: 1 2 (Fault)
Page 3: 1 2 3 (Fault)
Page 1: 1 2 3 (Hit)
Page 4: 4 2 3 (Fault)
Page 2: 4 2 3 (Hit)
Page 5: 4 5 3 (Fault)
Total FIFO page faults: 5

LRU Page Replacement:
Page 1: 1 (Fault)
Page 2: 1 2 (Fault)
Page 3: 1 2 3 (Fault)
Page 1: 1 2 3 (Hit)
Page 4: 1 4 3 (Fault)
Page 2: 1 4 2 (Fault)
Page 5: 5 4 2 (Fault)
Total LRU page faults: 6
```

> 📸 **Screenshot :**
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/ca55f234-96bb-4c67-9764-e80c91b9abfc" />


---

## 📊 Observation and Result Table

| Algorithm | Number of Page Faults | Number of Hits | Total References | Hit Ratio |
| :--- | :---: | :---: | :---: | :---: |
| **FIFO (First-In-First-Out)** | **5** | **2** | 7 | $2 / 7 \approx 28.57\%$ |
| **LRU (Least Recently Used)** | **6** | **1** | 7 | $1 / 7 \approx 14.28\%$ |

---

## 🏁 Conclusion

The simulation of FIFO and LRU page replacement algorithms was successfully executed. The results illustrate how page fault counts vary depending on page access patterns and replacement strategy for a given frame allocation size ($f = 3$).
