# Understanding RAII

> Links:
> - https://www.youtube.com/watch?v=q6dVKMgeEkk

Resource Acquisition is Instantiation (RAII)

When you acquire some resource (memory on the heap e.g. dynamically allocated), or a mutex lock, or a thread. When resources are acquired, if they're not cleaned up when they go out of scope then you'll get memory leaks.

RAII is used to make code that acuqires a resource safer and easier to write.

> RAII is when you acquire resouces in a constructor and release (or delete) the resource in the corresponding destructor.

### What is a Resource

- something that must be acquired before use
- In limited supply
- Examples: heap memory, files, sockets, mutexes

A program has to acquire memory from the OS (for heap allocation), and the program must eventually give them back to the OS.

Benefits of RAII
- Dont have to worrya bout the resource lifetime
- Instead, think about object lifetime.

Consequences:
- Never write:
  - `new`
  - `free`
  - `delete`
  - explicitly lock/unlock a `mutex`


Examples of RAII classes:
- `std::vector`
- `std::string`
- `std::unique_ptr`
- std::shared_ptr
- `std::lock_guard` or `std::scoped_lock`


