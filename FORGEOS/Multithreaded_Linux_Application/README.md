Multithreaded Linux Application Using POSIX Threads and Mutexes
Project Overview

This project is a Multithreaded Linux Application developed to demonstrate important Operating Systems and Systems Programming concepts such as POSIX threads, thread synchronization, mutex locks, condition variables, producer-consumer architecture, shared data, signal handling, and graceful shutdown.

The application is designed to process multiple tasks concurrently using three worker threads. The main thread acts as a producer by reading integer values from an input file and adding them to a shared circular task queue. The worker threads act as consumers, retrieving tasks from the queue and processing them simultaneously.

Each worker calculates the square of the assigned value and writes the result to an output file. For example, an input value of 10 produces 100, while 20 produces 400.

How the Project Works

The application follows a Producer–Consumer model:

The main thread reads task values from data/tasks.txt.
Each value is converted into a task object.
The task is added to a shared circular FIFO queue.
If a worker is waiting because the queue is empty, a condition variable signals it.
One of the three worker threads retrieves the task.
The worker calculates value × value.
The result is written to output/results.txt.
This process continues until all tasks are completed.
The workers are then stopped safely.
Synchronization

Since multiple worker threads access the same task queue and output file, synchronization is required to prevent unsafe simultaneous access.

A mutex is used to protect the shared resources. Only one thread can access the protected resource at a time, helping prevent race conditions.

A condition variable is used to coordinate the workers. When the queue is empty, workers wait instead of continuously checking the queue and wasting CPU resources. When the producer adds a new task, it signals a waiting worker.

Circular Task Queue

The project uses a bounded circular FIFO queue with a size of 10.

The queue uses:

front – identifies the next task to remove
rear – identifies where the next task is inserted
count – tracks the number of pending tasks
tasks[] – stores the task objects

The circular structure allows the queue positions to be reused after reaching the end.

Graceful Shutdown

The application supports safe termination using SIGINT (Ctrl+C).

When the user presses Ctrl+C:

The SIGINT handler is triggered.
A shutdown request is recorded.
Workers detect the shutdown request and stop safely.
pthread_join() waits for the worker threads to finish.
The output file is closed.
Synchronization resources are cleaned up.
The application exits without abrupt termination.
Project Structure
Multithreaded-Linux-Application/
│
├── src/
│   ├── main.c
│   ├── task_queue.c
│   └── task_queue.h
│
├── data/
│   └── tasks.txt
│
├── output/
│   └── results.txt
│
└── README.md
File Description
main.c – Handles thread creation, producer logic, signal handling, and worker management.
task_queue.c – Contains queue initialization, task insertion, and task retrieval functions.
task_queue.h – Defines the task and queue structures and function declarations.
tasks.txt – Contains the input values to be processed.
results.txt – Stores the processed results.
Example
Input
10
20
30
40
50
Processing
Worker 1 → 10² = 100
Worker 2 → 20² = 400
Worker 3 → 30² = 900
Output
Worker 1 processed Task 1: 10 -> 100
Worker 2 processed Task 2: 20 -> 400
Worker 3 processed Task 3: 30 -> 900

The complete results are saved in output/results.txt.

Operating System Concepts Demonstrated

This project demonstrates:

POSIX Threads (pthread)
Thread Creation
Thread Synchronization
Mutex Locks
Condition Variables
Producer–Consumer Model
Shared Data Management
Circular Queue
Signal Handling
Graceful Shutdown
Thread Joining
File I/O
Learning Outcomes

Through this project, we demonstrate how multiple threads can execute tasks concurrently while safely accessing shared resources. The project also provides practical understanding of race-condition prevention, thread coordination, synchronization, Linux/POSIX APIs, and safe process termination.

Future Scope

The project can be extended with:

Dynamic number of worker threads
Larger task queues
Priority-based task scheduling
Task statistics and monitoring
More complex task processing
Performance benchmarking
Improved logging
Conclusion

The project successfully demonstrates a practical multithreaded Linux application using POSIX threads, mutexes, condition variables, signal handling, and a producer-consumer architecture. It shows how multiple workers can process shared tasks concurrently while maintaining synchronization and ensuring safe application termination.
