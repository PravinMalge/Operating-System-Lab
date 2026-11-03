# Practical 07: Process Synchronization using Semaphores (Producer-Consumer Problem)

## 🎯 Objective

To implement and demonstrate thread synchronization and solve the classic Producer-Consumer critical section problem using POSIX semaphores (`sem_t`) and POSIX threads (`pthread`).

---

## 🛠️ Tools & Environment

* **Operating System:** Ubuntu Linux (VirtualBox)
* **Compiler:** GCC with POSIX Threads library (`-pthread`)
* **Core Concepts:** Semaphores (`sem_wait`, `sem_post`), Bounded Buffer, Mutex, Multi-threading (`pthread_create`, `pthread_join`)

---

## 💻 Code Implementation

### `producer_consumer.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define SIZE 5

int buffer[SIZE];
int in = 0;
int out = 0;

sem_t empty;
sem_t full;
sem_t mutex;

void *producer(void *arg) {
    int item;
    for (item = 1; item <= 10; item++) {
        sem_wait(&empty);
        sem_wait(&mutex);

        buffer[in] = item;
        printf("Producer produced: %d\n", item);
        in = (in + 1) % SIZE;

        sem_post(&mutex);
        sem_post(&full);
        sleep(1);
    }
    return NULL;
}

void *consumer(void *arg) {
    int item;
    for (int i = 1; i <= 10; i++) {
        sem_wait(&full);
        sem_wait(&mutex);

        item = buffer[out];
        printf("Consumer consumed: %d\n", item);
        out = (out + 1) % SIZE;

        sem_post(&mutex);
        sem_post(&empty);
        sleep(1);
    }
    return NULL;
}

int main() {
    pthread_t prod_thread, cons_thread;

    // Initialize semaphores
    sem_init(&empty, 0, SIZE); // Initially, buffer has SIZE empty slots
    sem_init(&full, 0, 0);     // Initially, 0 slots are filled
    sem_init(&mutex, 0, 1);    // Binary semaphore for mutual exclusion

    // Create threads
    pthread_create(&prod_thread, NULL, producer, NULL);
    pthread_create(&cons_thread, NULL, consumer, NULL);

    // Wait for threads to complete execution
    pthread_join(prod_thread, NULL);
    pthread_join(cons_thread, NULL);

    // Destroy semaphores
    sem_destroy(&empty);
    sem_destroy(&full);
    sem_destroy(&mutex);

    return 0;
}
```

---

## ⚙️ Steps and Terminal Execution

### Step 1: Write the Source Code
Create and edit the C file using `nano`:
```bash
nano producer_consumer.c
```

> 📸 **Screenshot:**
> ![Nano Editor](assets/nano_producer_consumer.png)

---

### Step 2: Compile the Program
Compile the C program linking the POSIX threads library:
```bash
gcc producer_consumer.c -o producer_consumer -pthread
```

---

### Step 3: Run the Executable
Execute the compiled binary:
```bash
./producer_consumer
```

**Terminal Output / Execution Log:**
```text
Producer produced: 1
Consumer consumed: 1
Producer produced: 2
Consumer consumed: 2
Producer produced: 3
Producer produced: 4
Consumer consumed: 3
Producer produced: 5
Producer produced: 6
Consumer consumed: 4
Producer produced: 7
Producer produced: 8
Consumer consumed: 5
Producer produced: 9
Producer produced: 10
Consumer consumed: 6
Consumer consumed: 7
Consumer consumed: 8
Consumer consumed: 9
Consumer consumed: 10
```

> 📸 **Screenshot:**
> ![Terminal Output](assets/execution_output.png)

---

## 📊 Semaphore Functionality Summary

| Semaphore Variable | Initial Value | Purpose / Function |
| :--- | :--- | :--- |
| `empty` | `SIZE` (`5`) | Counts empty slots available in the buffer. Decremented by Producer, incremented by Consumer. |
| `full` | `0` | Counts filled slots available in the buffer. Incremented by Producer, decremented by Consumer. |
| `mutex` | `1` | Binary semaphore ensuring mutual exclusion when accessing the shared buffer. |

---

## 🏁 Conclusion

The Producer-Consumer practical was successfully implemented and verified using POSIX semaphores and threads. The output confirms proper synchronization without race conditions or buffer overflow/underflow.