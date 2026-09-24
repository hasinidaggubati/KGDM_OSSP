Multithreaded Linux Application Using POSIX Threads and Mutexes

Operating Systems and Systems Programming Project

A practical Linux application demonstrating multithreading, concurrent execution, synchronization, critical sections, race conditions, and mutual exclusion using POSIX Threads and mutexes.

---

## 📌 Project Overview

This project implements a **Multithreaded Linux Application** using the **C programming language** and **POSIX Threads (pthreads)**.

The application creates multiple threads that perform tasks concurrently. Some threads access a common shared resource, creating a critical section that requires synchronization.

To prevent multiple threads from accessing the shared resource simultaneously, **POSIX mutex locks** are used. A thread acquires the mutex before entering the critical section and releases it after completing the required operation.

The project demonstrates important Operating System concepts including:

* POSIX Threads
* Multithreading
* Concurrent execution
* Mutex synchronization
* Mutual exclusion
* Critical sections
* Race conditions
* Shared resources
* Thread creation
* Thread joining
* Thread termination
* Linux programming

---

# 🎯 Problem Statement

In a multithreaded application, multiple threads may access and modify a shared resource at the same time.

Without proper synchronization, simultaneous access can cause:

* Race conditions
* Data inconsistency
* Unexpected program output
* Incorrect shared-resource values
* Unpredictable program behavior

The objective of this project is to design a Linux-based application where multiple threads can execute concurrently while safely accessing shared resources.

The project uses **POSIX threads** for concurrent execution and **mutexes** for mutual exclusion and synchronization.

---

# 🎯 Objectives

1. Implement a multithreaded Linux application using POSIX Threads.
2. Create and manage multiple threads.
3. Demonstrate concurrent execution of multiple threads.
4. Identify and demonstrate race conditions.
5. Implement mutex-based synchronization.
6. Protect shared resources using mutex locks.
7. Demonstrate critical sections and mutual exclusion.
8. Ensure consistent access to shared data.
9. Compile and execute the application in a Linux environment.
10. Gain practical understanding of Linux thread programming.

---

# 🛠️ Technologies Used

| **Technology**               | **Purpose**                                  |
| ---------------------------- | -------------------------------------------- |
| **C**                        | Programming language used for implementation |
| **Linux / Ubuntu**           | Operating environment                        |
| **POSIX Threads (pthreads)** | Thread creation and management               |
| **POSIX Mutex**              | Synchronization and mutual exclusion         |
| **GCC Compiler**             | Compiling the C program                      |
| **Linux Terminal**           | Compilation, execution, and testing          |
| **VS Code**                  | Source-code development and editing          |
| **GitHub**                   | Version control and project repository       |

---

# 📁 Project Structure

```text
Multithreaded_Linux_Application/
│
├── src/
│   └── main.c
│
├── screenshots/
│   ├── compilation.png
│   └── output.png
│
├── presentation/
│   └── OS_Project_Presentation.pptx
│
├── documentation/
│   └── Project_Abstract.pdf
│
└── README.md
```

> The exact file names and folders can be changed according to the files present in your GitHub repository.

---

# 🏗️ System Architecture

```text
                         START
                           │
                           ▼
                  ┌─────────────────┐
                  │  Initialize     │
                  │ Shared Resource │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Initialize      │
                  │     Mutex       │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Create Multiple │
                  │     Threads     │
                  └────────┬────────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
         ┌─────────┐  ┌─────────┐  ┌─────────┐
         │ Thread 1│  │ Thread 2│  │ Thread 3│
         └────┬────┘  └────┬────┘  └────┬────┘
              │            │            │
              └────────────┼────────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Acquire Mutex   │
                  │     Lock        │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Critical        │
                  │ Section         │
                  │ Shared Resource │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Release Mutex   │
                  │     Lock        │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ pthread_join()  │
                  │ Wait for Threads│
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Destroy Mutex   │
                  └────────┬────────┘
                           │
                           ▼
                          END
```

---

# ⚙️ Working Principle

## 1. Application Initialization

The application starts by initializing the required shared resource and synchronization mechanism.

A POSIX mutex is initialized before the worker threads begin accessing the shared resource.

---

## 2. Thread Creation

Multiple threads are created using the POSIX Threads API.

The following function is used:

```c
pthread_create()
```

Each thread receives a specific task and executes independently.

The threads can execute concurrently depending on the Linux scheduler.

---

## 3. Concurrent Execution

After creation, multiple threads execute their assigned operations concurrently.

```text
             Main Thread
                  │
          Create Threads
                  │
       ┌──────────┼──────────┐
       ▼          ▼          ▼
   Thread 1   Thread 2   Thread 3
       │          │          │
       ▼          ▼          ▼
     Task       Task       Task
```

Concurrent execution allows multiple threads to make progress during the same period.

---

## 4. Shared Resource

Some operations performed by the threads involve accessing a common shared resource.

For example:

```text
Thread 1 ──────┐
               │
Thread 2 ──────┼──► Shared Resource
               │
Thread 3 ──────┘
```

Since multiple threads may access the resource, synchronization is required.

---

## 5. Critical Section

The portion of the program where the shared resource is accessed or modified is called the **critical section**.

Only one thread should access the protected critical section at a time.

```text
Thread
   │
   ▼
Acquire Mutex
   │
   ▼
Critical Section
   │
   ▼
Access Shared Resource
   │
   ▼
Release Mutex
```

---

## 6. Mutex Synchronization

A mutex provides **mutual exclusion**.

Before entering the critical section, the thread locks the mutex:

```c
pthread_mutex_lock(&mutex);
```

The thread then performs the operation on the shared resource.

After completing the operation, the mutex is released:

```c
pthread_mutex_unlock(&mutex);
```

This ensures that another thread can access the protected resource only after the current thread has finished.

---

## 7. Race Condition

A race condition can occur when multiple threads access or modify shared data at the same time without synchronization.

### Without Mutex

```text
Thread 1 ───────► Shared Data
                     ▲
                     │
Thread 2 ───────► Shared Data

        ↓

   Race Condition
        ↓
Inconsistent Result
```

### With Mutex

```text
Thread 1 ──► LOCK ──► Critical Section ──► UNLOCK
                                           │
Thread 2 ──────────────────────────────────►
                       waits
```

The mutex prevents simultaneous access to the protected critical section.

---

## 8. Thread Completion

After the threads complete their execution, the main thread waits for them using:

```c
pthread_join()
```

This ensures that the main program does not terminate before the created threads finish their execution.

---

## 9. Mutex Destruction

After all threads have completed and the mutex is no longer required, it is destroyed using:

```c
pthread_mutex_destroy()
```

This releases the resources associated with the mutex.

---

# 🔄 Thread Synchronization Flow

```text
                Thread Created
                     │
                     ▼
              Perform Task
                     │
                     ▼
             Shared Resource?
                /          \
              Yes           No
               │             │
               ▼             ▼
          Lock Mutex      Continue
               │
               ▼
        Critical Section
               │
               ▼
         Modify / Access
         Shared Resource
               │
               ▼
         Unlock Mutex
               │
               ▼
          Continue Task
               │
               ▼
          Thread Ends
```

---

# 🔑 POSIX APIs Used

| **API**                   | **Purpose**                                                  |
| ------------------------- | ------------------------------------------------------------ |
| `pthread_create()`        | Creates a new thread                                         |
| `pthread_join()`          | Waits for a thread to complete                               |
| `pthread_mutex_init()`    | Initializes a mutex                                          |
| `pthread_mutex_lock()`    | Locks the shared resource before entering a critical section |
| `pthread_mutex_unlock()`  | Releases the mutex after accessing the shared resource       |
| `pthread_mutex_destroy()` | Destroys the mutex after use                                 |

---

# 💻 Basic Mutex Implementation

A simplified implementation of the synchronization mechanism is:

```c
pthread_mutex_lock(&mutex);

/* Critical Section */
/* Access or modify shared resource */

pthread_mutex_unlock(&mutex);
```

The mutex ensures that only one thread can execute the protected section at a time.

---

# 🧠 Key Operating System Concepts

## POSIX Threads

POSIX Threads, commonly called **pthreads**, provide an API for creating and managing threads in Linux.

---

## Multithreading

Multithreading allows multiple threads within the same application to execute concurrently.

---

## Concurrency

Concurrency allows multiple threads to make progress during the same period of execution.

---

## Mutex

A mutex is a synchronization mechanism used to provide mutual exclusion when multiple threads access shared resources.

---

## Critical Section

A critical section is a portion of code where shared data or resources are accessed or modified.

---

## Race Condition

A race condition occurs when the result of a program depends on the timing or order in which multiple threads access shared data.

---

## Mutual Exclusion

Mutual exclusion ensures that only one thread accesses a protected critical section at a time.

---

## Thread Joining

`pthread_join()` allows the main thread to wait until a created thread finishes execution.

---

# 🧪 Testing

The application can be tested by observing the execution of multiple threads and the access to the shared resource.

Testing focuses on:

* Multiple thread creation
* Concurrent execution
* Shared-resource access
* Mutex locking
* Mutex unlocking
* Critical-section protection
* Race-condition prevention
* Thread completion
* Final consistent output

---

# 📊 Expected Behavior

When synchronization is correctly implemented:

```text
Thread 1 → Lock → Access Shared Resource → Unlock
                                              │
Thread 2 → Wait ─────────────────────────────┘
                                              │
                                              ▼
                              Thread 2 → Lock → Access
```

Only one thread enters the protected critical section at a time.

This helps maintain consistent shared data.

---

# 🖥️ Compilation

Navigate to the project directory:

```bash
cd ~/path/to/Multithreaded_Linux_Application
```

Compile the C program using GCC:

```bash
gcc main.c -o app -pthread
```

The `-pthread` option enables POSIX thread support.

---

# ▶️ Running the Application

Run the compiled application using:

```bash
./app
```

The program creates multiple threads and executes the assigned tasks concurrently.

---

# 📌 Sample Output

The exact output depends on the implementation and thread scheduling.

A typical execution may look like:

```text
Multithreaded Linux Application

Thread 1 created
Thread 2 created
Thread 3 created

Thread 1 accessing shared resource
Thread 1 completed critical section

Thread 2 accessing shared resource
Thread 2 completed critical section

Thread 3 accessing shared resource
Thread 3 completed critical section

All threads completed successfully.
Final shared resource value: <value>
```

> Thread execution order may change between different runs because thread scheduling is handled by the Linux operating system.

---

# 📂 Files Description

| **File / Folder** | **Purpose**                                             |
| ----------------- | ------------------------------------------------------- |
| `main.c`          | Contains the main application and thread implementation |
| `README.md`       | Project documentation                                   |
| `screenshots/`    | Stores project execution screenshots                    |
| `presentation/`   | Contains project presentation files                     |
| `documentation/`  | Contains project documentation and abstract             |

> Update this table if your actual repository contains additional source files.

---

# 👥 Team

**Course:** Operating Systems and Systems Programming (25CS2104E)

**Academic Year:** 2026–27
**Term:** I
**Section:** 08
**Team:** 06

### Team Members

| **Roll Number** | **Student Name** | **Individual Responsibility**                           |
| --------------- | ---------------- | ------------------------------------------------------- |
| 2520030079      | M. Keerthi Sri   | Application design and multithreading implementation    |
| 2520030080      | N. Greeshma      | Critical-section design and mutex-based synchronization |
| 2520030289      | D. Darahasini    | Race-condition testing and performance evaluation       |
| 2520030296      | R. Mythri        | Linux environment setup, debugging and documentation    |

---

# 🎓 Learning Outcomes

Through this project, we gain practical understanding of:

1. POSIX thread programming.
2. Thread creation and management.
3. Concurrent execution.
4. Shared-resource management.
5. Mutex-based synchronization.
6. Critical sections.
7. Race conditions.
8. Mutual exclusion.
9. Thread joining and termination.
10. Linux-based C programming.

---

# ✅ Expected Outcome

The project produces a functional multithreaded Linux application in which multiple threads execute concurrently while safely accessing shared resources.

The use of mutex locks prevents simultaneous access to protected critical sections and helps maintain consistent results.

The project demonstrates practical Operating Systems concepts including:

* Multithreading
* Concurrency
* Synchronization
* Mutual exclusion
* Critical sections
* Race conditions
* POSIX APIs
* Linux programming

---

# 🏁 Conclusion

This project demonstrates the implementation of a **Multithreaded Linux Application using POSIX Threads and Mutexes**.

Multiple threads are created to perform concurrent tasks, while mutex synchronization is used to protect shared resources and critical sections.

The project provides practical experience in **thread management, concurrency, synchronization, mutual exclusion, race-condition prevention, and Linux system programming**.

---

## 📌 Project Status

**Status:** Completed / Under Development

**Platform:** Linux / Ubuntu

**Language:** C

**Threading:** POSIX Threads

**Synchronization:** POSIX Mutex
