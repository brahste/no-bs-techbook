# Error Handling in Rust

look into `std::error::Error`?

`Box<dyn Error>` means that the function given this will return a type that implements the `Error` trait, but the specific type of the return value doesn't have to be known.

The `?` operator will return the error value from the current function. In this way it can be used to propgate errors through functions themselves.
