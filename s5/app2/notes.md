# Concurrent Programming
## Threads
### Thread Types
* Standard Threads
    * Use a priority system
    * Timers are standard threads
* Interrupts
    * Tickers use interrupts and that's what makes them a lot more accurate
    * Interrupts use a priority level higher than the highest priority of standard threads
    * You never want to put code that could cause blocks in an interrupt

### Thread States
1. Ready
    * Waiting to be executed
2. Blocked
    * Currently blocked by a third party (Mutex / Semaphore)
    * Thread::wait() causing them to liberate the CPU
3. Running
    * Only one thread is running at once

### Thread Ordering
Generally speaking, threads are cycled in Round Robin fashion when they're all at the same priority level. If there are thread priorities, those are used to determine which thread will be executed next.

This varies between OS, but each thread has to operate during a minimal time frame (time slice). In the case of the LPC1768, this time slice is 5ms

## Operating Systems
### RTOS (Real Time Operating System)
* Faster
* Smaller memory usage
* Portable (Easy to port between architectures / systems)
* Modular (Can easily add more of whatever you need (flash / memory / cpu / etc...))
* Better uptime (rule of 9s)
* Predictable

### GPOS (General Purpose Operating System)
* Standard PC OS (Windows, OS X, Linux)
* Resource Intensive

### Common Characteristics
* Multitasking
* Resource Management (time, interrupts, ram, peripherals, synchronisation methods)

### Soft vs Hard Real-Time
The main different between hard and soft real-time is the consequences behind the responsiveness of the system. A hard real-time system will have real and possibly dangerous consequences.

RTOS are better suited for hard real-time, but technically, both types of operating systems can do both.

## Synchronisation Tools
### Mutex
* Lock / unlock
* Binary
* Used to manage critical sections
* Only the thread that locked the mutex can unlock it
* VERY dangerous to use in interrupts

### Semaphore
* Wait / release
* Can be binary or have multiple credits
* Used for sharing resources
* Used to sync rendezvous
* Any thread can lock or release the semaphore
* Releases can be queued up by the OS causing waits to be skipped immediately

### Signals
* Wait / set
* You can specify which thread receives the signal
* Waits can expect to receive certain values as a signal;therefore, guaranteeing the origin of the signal

## Communication Between Threads
### Queue
* Requires the management of a MemoryPool
* Can allow the transfer of various types / sizes of data

### Mailbox
* MemoryPool is automatically managed
* Everything put inside the mailbox uses the same amount of memory and that could waste some memory