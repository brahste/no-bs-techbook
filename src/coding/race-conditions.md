# Race Conditions

When writing multithreaded applications, a race condition is a common problem.

> A race condition occurs when two or more threads are attempting to access shared data. Since the thread scheduler can swap between threads at any time, the order that each thread with access the data is unknown.

Since the changed data is dependent on the scheduler, one can interpret the threads as "racing" to access/change the data.

An example of where issues arise is when one thread checks the value of the shared data (e.g. with a conditional) before using it in it's operations. During the very small amount of time between when the data is checked and operated on, it is possible for another thread to alter the shared data, thus retroactively invalidating the check after it has already passed.

To prevent race conditions you can put a lock around the shared data to enforce access from only one thread at a time.

In C++ this functionality can be implemented with a `lock_guard`.

...incomplete... Give links to address this issue in various languages...
