# Using Threads
Thread objects that are joinable must either by *joined* or *detached* before they are destroyed.

**detach**
This method can be used on a thread object to *detach* the thread from the calling thread. Thus the spawned thread and the calling thread execute asynchronously and non-blocking. When either thread ends execution, its resources are released, thereby making a call to *detach* make the thread *non-joinable*.

## Passing Variables
The basic usage of `std::thread` is to pass a function pointer as the first parameter. Any any arguments needed for the function as the remaining arguments.

If the first parameter is a *member function pointer*, then the second parameter should be a pointer the concrete object upon which the member function is called, followed by any parameters to it.
```C++
foo::Bar bar();
std::thread th(&foo::Bar::m_function, &bar, 1, 2, 3).detach();
```

If the parameters of the function being called by the thread are references then you need to pass them in by wrapping them in the `std::ref`. This avoids the thread's attempt to copy-construct the supplied parameters.

Similarly, you will have to use `std::move` if you plan on passing a unique pointer to a thread.

