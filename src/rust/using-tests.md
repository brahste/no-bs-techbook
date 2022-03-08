# Using Tests

> Links:
> - [Rust Book Chapter 11](https://doc.rust-lang.org/book/ch11-00-testing.html)
> - [Rust By Example Chapter 21](https://doc.rust-lang.org/stable/rust-by-example/testing.html)

## Unit Tests

Place unit tests in the files with the code they're testing. Create a module (with the `mod`) keyword at the bottom of each file, and give it the `#[cfg(test)]` annotation. Under that give each unit test a `#test` annotation.
For example, the snippet below shows three different ways you can write and control unit tests.

```rust-lang
mod tests {
    use super::*  // <- May no be necessary
    
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
