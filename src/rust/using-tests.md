# Using Tests

> Links:
> - [Rust Book Chapter 11](https://doc.rust-lang.org/book/ch11-00-testing.html)
> - [Rust By Example Chapter 21](https://doc.rust-lang.org/stable/rust-by-example/testing.html)

## Unit Tests

Place unit tests in the files with the code they're testing. Create a module (with the `mod`) keyword at the bottom of each file, and give it the `#[cfg(test)]` annotation. Under that give each unit test a `#test` annotation.
For example, the snippet below shows three different ways you can write and control unit tests.

```rust-lang
#[cfg(test)]
mod tests {
    use super::* 
    
    #[test]
    fn test_one() {
        assert_eq!(2 + 2, 4);
    }
    
    #[test]
    #[should_panic]  // <- Accepts optional (expected = "Panic type") parameter
    fb test_two() {
        let b = True;
        let x = "string cannot add to" + b;
    }
    
    #[test]
    #[ignored]  // <- Can be ignored with $ cargo test -- --ignored
    fn test_three() {
        assert("Hello world".contains("ello"));
    }
    
}
```

Note the call to `use super::*` brings objects in the parent module into the scope of the `tests` module. This allows private functions to be unit tested. While some methodologies argue that private functions shouldn't be tested, Rust remains agnostic on this matter and allows developers to test private functions in this way if they like.

## Integration Tests

Place integration tests in the _tests/_ directory.
