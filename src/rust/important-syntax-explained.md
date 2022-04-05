# Important Syntax Explained

# if let

When extracting inner content from an enum, such as a `Result` or `Option`, if you're only interested in one of the variants then it's cleaner to use an `if let` statement.

For example:
```rust-lang
let result = function_that_returns_result();  // <- this function returns Result<(), Error>

if let Err(e) = result {
    process::exit(1);                         // <- only considers the Error variant
}
```

Resd the statement `if let Err(e) = result` as: If `result` is an `Err` variant, pass the error contained within `Err(e)` to the block, otherwise pass.
