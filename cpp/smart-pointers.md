# Smart Pointers

You can you `new` to create a new instance of a type and allocate that memory on the heap. You then need to use `delete` to deallocate that memory and guarentee that you won't have a memory leak. In C++, smart pointers can be used to manage the calls to `new` and `delete` without using them directly.

To get access to smart pointers `#include <memory>`

- `std::unique_ptr<T>`: This is a scoped pointer so when it goes out of scope it's memory is deleted. You may pass the type of the pointer as a template argument `T`. You can't copy a `unique_ptr`. The preferred way to create a `unique_ptr` is to use `std::make_unique`
- `std::shared_ptr<T>`: This is a pointer that remains active until the number of references to that pointer becomes zero. You may pass the type of the pointer as a template argument `T`. The preferred way to create a `shared_ptr` is to use `std::make_shared`. When you assign a `shared_ptr` to another `shared_ptr` it increases the reference count.
- `std::weak_ptr<T>`: Can be used in conjuction with a `shared_ptr` but doesn't increase the reference count so doesn't affect the lifetime of the pointer's underlying entity.
