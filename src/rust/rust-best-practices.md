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






