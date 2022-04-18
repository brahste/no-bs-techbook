# Using Tests

> Links:
> 
> - [Rust Book Chapter 11](https://doc.rust-lang.org/book/ch11-00-testing.html)
> - [Rust By Example Chapter 21](https://doc.rust-lang.org/stable/rust-by-example/testing.html)

## Unit Tests

The body of a unit test function should contain three steps to be a complete test (this isn't Rust specific and is considered good practice for testing in any language):

1. Arrange: Setup the data or state required for testing

2. Act: Run the code under test

3. Assert: Ensure the result is what was expected

### Writing Unit Tests in Rust

Place unit tests in the files with the code they're testing. Create a module (with the `mod`) keyword at the bottom of each file, and annotate it with the `#[cfg(test)]` attribute. Then, before each unit test annotate it the function declaration with a `#[test]` attribute.

**Snippet**

```
#[cfg(test)]
mod tests {
    #[test]
    fn test1() {
    
    }
}
```

In Rust there are a few types of test that can be used:

1. Assert tests: These tests use one of `assert()`, `assert_eq()`, `assert_ne()` to check that the result of some code is what we expect. Note that you can pass custom failure messages after the expression or variables being asserted.

2. Panic tests: These are tests that ensure that the program will panic if it is used incorrectly. To use these type of tests add the `#[should_panic]` attribute to the test. To make these tests more precise you can also add an expected substring to the attribute such as `#[should_panic(expected = "Cannot divide")]`. In this case, if the test panics with a message of *"Cannot divide by zero"*, then this test will pass, oterhwise it will fail.

3. Result tests: These tests operate similar *assert tests*, but instead return a `Result<T, E>` type. If during the execution of the test an `Err` variant is returned, the test fails. This type of test allows you to use the `?` operator to conveniently return an error variant, thus failing the test.
   
4. Ignoreable tests: These tests can be of the same type as any of the above, but can be optionally ignored by annotating it with the `#[ignore]` tag. To run only the ignored tests use `cargo test -- --ignored`.
   
   
**Example**

For example, the snippet below shows three different ways you can write and control unit tests.

```rust-lang
#[cfg(test)]
mod tests {
    use super::*

    #[test]  // An 'assert' test
    fn test_one() {
        assert_eq!(2 + 2, 4);
    }

    #[test] 
    #[should_panic]  // A 'panic' test
    fn test_two() {
        let b = True;
        let x = "string cannot add to" + b;
    }

    #[test]  // A 'result' test
    fn test_three() -> Result<(), String> {
        if 2 + 2 == 4 {
            Ok(())
        } else {
            Err(String::from("Doesn't equal four"))
        }
    }

    #[test]
    #[ignore]  // An 'ignored' test 
    fn test_four() {
        assert("Hello world".contains("ello"));
    }

}
```

Note the call to `use super::*` brings objects in the parent module into the scope of the `tests` module. This allows private functions to be unit tested. While some methodologies argue that private functions shouldn't be tested, Rust remains agnostic on this matter and allows developers to test private functions if they like.

### Running the Unit Tests

To run your tests use

```bash
$ cargo test
```

This commands compiles your code in test mode and runs a binary that executes any functions annotated with `#[test]`. Other functions in the test module can can still be useful for shared setup logic.

There are a number of command line flags that can be set to adjust how the tests are compiled and run. Flags that are impact the testing compiler are passed directly (e.g. `cargo test --doc`) while flags that impact the resulting binary are seperated by `--` (e.g. `cargo test -- --nocapture`). Some of the most useful flags are given below.

### Framework Pattern for Unit Tests

By using non-test functions as helpers to the testable ones, a test framework pattern is easily implemented in Rust unit tests. 

**Example**

You want to use a library from logging in your unit tests. The crate's *log* and *env_logger* together with will do the trick.

```
use log;
use env_logger;

env_logger::init();

// -- snip --                    

#[cfg(test)]
mod tests {
    fn init() {
        // Enables logging in tests
        let _ = env_logger::builder().is_test(true).try_init();  
    }

    #[test]   
    fn test_1() {   
        init();   
        log::debug!("Debug message from test 1")
    }   
 
    #[test]   
    fn test_2() {   
        init();   
        log::debug!("Debug message from test 2")
    }   
```

Then make sure the `RUST_LOG` environment variable is set to debug.

```
RUST_LOG=debug cargo test -- --show-output
```

This way you can use shared setup logic in the `init()` function to setup logging capabilities directly in each test.

## Integration Tests

Put integration tests in the _tests/_ directory. Files in the *tests/ folder will only bo compiled when the `cargo test` command is issued. Test functions in integration tests still need to be annotated with `#[test]` and the code being tested has to be brought into scope, but the `#[cfg(test)]` attribute isn't required.
Each file in the *tests/* directory is compiled as a seperate crate.

### Framework Pattern for Integration Tests

By seperating utility code into another crate in the *tests/* directory, commonly used setup logic can be used across integration tests, but there's a trick. You have to setup the utility module with the structure *tests/utilities/mod.rs*, where *utilities/* can be whatever module name you prefer (e.g. *common/*). When you setup the files this way, Rusts test compiler doesn't include these files when compiling the integration tests. Of course, the module still has to be brought into scope on the integration tests themselves.

**Example**

```
use your_crate;

mod utilities;

#[test]
fn test_1() {
    utilities::init();
    assert_eq!(4, your_crate::give_four());
}
```

## Filtering Tests

You can select which tests to run by providing a test name or substring of a set of test names to run them. For example, if you have three tested named `foo`, `bar`, `baz`, then you could run only `bar`, and `baz` by issuing `cargo test ba`. Also, the module becomes part of the name so entire test modules can be run independently using this method.

## Useful Command Line Flags

- `cargo test -- --test-threads=1`: Limits the number of threads used by the test runner (by default each test uses its own thread).
- `cargo test -- --show-output`: Shows output from the tests (by defaul, any output to stdout or stderr is captured by the test runner and hidden).
- `cargo test -- --include-ignored`: Run all of the tests, including the ones tagged with `#[ignore]`.
- `cargo test --test integration_test1`: Will run only the tests contained in the *tests/integration_test1.rs* file.

