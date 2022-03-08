# Using Command Line Arguments and Environments

The standard library package for working with the envrionment is `std::env`.

Access user's environment variables
```rust-lang
let env_var = env::var("VARIABLE");
```

Or check the presence of an enviornment variable
```rust-lang
let env_var_exists: bool = env::var("VARIABLE").is_err();
```

# Method 1: Manual

To read arguments from the command line using Rust's standard library use the [`std::env::args`](https://doc.rust-lang.org/std/env/fn.args.html) function. 
```rust-lang
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();
    
    let option = &args[1];
    let flag   = &args[2];
    
    // -- rest of program --
}
```

__Note__: The call to `args()` returns an iterator which can be converted into a [collection](https://doc.rust-lang.org/std/collections/index.html) using the `.collect()` method.
