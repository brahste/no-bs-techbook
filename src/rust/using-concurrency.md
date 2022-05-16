# Using Concurrency
## Basics
### Creating a New Thread
To create a new thread, use the `thread::spawn` function and pass it a closure containing the code you want to run.

As is typical with threads in other languages, the thread handle (returned by the spawn statement) has a `join` method, which will wait until the thread has finished execution to continue. By default, all spawned threads run as 'detached'.

**Example**
```rust
use std::thread;    
use std::time::Duration;    
    
fn main() {    
    let handle = thread::spawn(|| {    
        for i in 1..10 { => i32    
            println!("This is thread number {}", i);    
            thread::sleep(Duration::from_millis(1)); <- (dur)     
        }    
    });    

	handle.join().unwrap();                                                               
}  
```

### Moving Closures to a Thread
If you want the clousure to take ownership of the variable from its envrionment, use the `move` keyword.

**Example**
```rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);
    });

    handle.join().unwrap();
}

```
In this example, the code wouldn't compile without the `move` operator since the compiler wouldn't know whether the vector `v` would outlive the thread; moving it into the thread solves this problem.

## Passing Data Between Threads
Using the module  `std::sync::mpsc` (multiple produce, single consumer), data can be sent and received between threads.

**Example**
This example shows how one can use `mpsc` to send message from multiple transmitters to a single receiever.
```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {


    let (tx, rx) = mpsc::channel();
    let tx1 = tx.clone();

	thread::spawn(move || {
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];

        for val in vals {
            tx1.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    thread::spawn(move || {
        let vals = vec![
            String::from("more"),
            String::from("messages"),
            String::from("for"),
            String::from("you"),
        ];

        for val in vals {
            tx.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    for received in rx {
        println!("Got: {}", received);
    }
 }
```

## Shared-State Concurrency
Rust allows shared state concurrency and implements the common concept of a *mutex* (mutual exclusion) to guard shared memory.

In Rust, the `Mutex<T>` type holds a value. Use the `lock()` method on a mutex to acquire its value. This operation will block execution of the thread until the mutex is obtained. When the object returned by calling `lock()` on a mutex goes out of scope, the lock is released and another thread can acquire it. But there's at trick: we can't obtain the mutex's inner value unless we have ownership of it, but in order to have ownership in a thread we have to move it. This is resolved by wraping the mutex in an atomically reference counted smart pointer `Arc<T>`.

> Note: `Rc<T>` is not safe to share between threads, but otherwise acts very similar to `Arc<T>`. Since `Rc<T>` doesn't implement the thread safety of atomics it doesn't suffer from the performance penalty imposed on atomics.

**Example**

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();

            *num += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *counter.lock().unwrap());
}
```