# Reading From Files

# Text Files to String

Reading contents from a text file into Rust is a fundamental operation. To do this, using the standard library use the [`std::fs::read_to_string`](https://doc.rust-lang.org/std/fs/fn.read_to_string.html) function.
```rust-lang
use std::fs;

fn main() {
    let contents = fs::read_to_string("file.txt");
    // -- rest of program -- 
}
```
