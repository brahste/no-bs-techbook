# Using Smart Pointers
Put simply, a pointer is a variable that holds a memory address. In Rust the most common use of a pointer is when you prepend a variable with `&` to access it as a reference. Using this notation, you borrow the value the reference points to. These are effectively for performance because there's no cost to accessing that data (e.g. no copies).

A smart pointer is the same as a normal pointer, but is equipped with additional functionality. For example, both the `String` and `Vec<T>` types are smart pointer. These include:
- Reference counting

References are pointers that only borrow data. Often smart pointers own the data they point to.

Typically smart pointers are structs that implement the `Deref` and `Drop` traits.

## Using a Box to Point to Data on the Heap
The most basic smart pointer is the `Box<T>` type. They're handy in the follow situations:
- When you have a type whose size can’t be known at compile time and you want to use a value of that type in a context that requires an exact size
- When you have a large amount of data and you want to transfer ownership but ensure the data won’t be copied when you do so
- When you want to own a value and you care only that it’s a type that implements a particular trait rather than being of a specific type

> At compile time, Rust needs to know how much space a type takes up.

To resolve this, when Rust doesn't know how large a type may be (potentially because the type is recursive), you can declare a pointer to that type such that it's allocated on the heap. This way, all that's on the stack is a pointer to a specific type. In Rust this is called indirection.

Indirection means that instead of storing a value directly you store a pointer to the value, thereby storing it *indirectly*.

Boxes provide only indirection and heap allocation.

## The Deref Trait

... Stopped at beginning of 15.2 ... 