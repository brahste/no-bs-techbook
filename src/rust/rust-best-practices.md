# Best Practices for Rust Programs

# Keep Things Modular

Modularity improves the code's readability, testability, and simplifies error handling. Keep the following points in mind when developing a program.
- Each function should deal with a single task. If a function is handling multiple responsibilities then it should likely be refactored.
- Use configuration variables to reduce the number of variables that need to be in scope.
- Handle error messages correctly the first time. Using `expect` statements is fine for prototyping, but once an implementation is chosen, handle errors explicitly so that large code overhauls are avoided.
- Place error-handling code in one place (as much as possible).

## Seperation of Concerns for Binary Projects

The Rust community has developed standards relating to what should be included in _main.rs_ and what should be included in _lib.rs_. Primarily, only command line parsing, configuration setup, and a call to a `run` function in _lib.rs_ (with associated error handling) should ever be inside the `main` function. Prototype code is the obvious exception to this rule, yet, it's always a good idea to keep these practices in mind as the code is developed.

It is also best practice to group related program configuration variables into a `struct Config` which is parsed in `main` by calling its constructor (e.g. `new`).

__Note__: Since the `main` function isn't testable directly, removing as much logic from `main` as possible improves the overall testability of the program.

## Handle Potential Errors with a `Result`

Returning a `Result` ensures that any errors possible in a function are handled when the function is called.
TODO: Expand on this section

## Split Code into a Library Crate

Move everything that isn't in the `main` function into _src/lib.rs_. This includes:
- All functions called in `main`
- Relevant `use` statements
- Configuration structs and method definitions

To make objects available in _src/main.rs_, first use the `pub` keyword to make them public. Next, since anything in the _src/lib.rs_ file will be available under the crate's name (from _Cargo.toml_) any of the objects can be used by prefixing the crate's name, or by including a `use <crate_name>::<object>;` call to bring the `<object>` into scope.

## Use Test Driven Development

Test driven development is a software development technique where you follow these steps:
1. Write a test that reflects how the code is intended to be run.
2. Write code that allows the test to compile, and run it to make sure it fails for the reason you expect.
3. Write code to make the test pass.
4. Refactor the code ensuring the tests still pass.
5. Repeat from step 1.

Rust's testing framework makes TDD much easier than other system level programming languages (such as C++).
TODO: Re-formulate this so it's more different than the Rust book
TODO: Add link to a better document on testing in Rust


