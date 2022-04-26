# Using Cargo and Crates

> Links:
> - [Rust Book: Chp. 14](https://doc.rust-lang.org/book/ch14-02-publishing-to-crates-io.html)

## Release Profiles

*Release profiles* allow a developer to use different configurations when compiling their code.

There are two main release profiles, *dev* and *release*. By default the *dev* profile is used (e.g. with `cargo build`) and the *release* profile can be toggled with `--release` (e.g. `cargo build --release`). 

You can override default options and add custom profiles to your *Cargo.toml* by adding a `[profile.*]` field. For example,

```toml
[profile.dev]
opt-level = 1
```

will change the amount of compile-time optimizations to 1 instead of the default 0 (though this change is not advised, you get the point). A full list of profile options can be found in [The Cargo Book](https://doc.rust-lang.org/cargo/reference/profiles.html).

## Publishing a Crate to Crates.io

## Documentation Comments

To make documentation comments use three slashes `///`. This notation provides markdown support. Docmentaion comments that use `///` are compiled into HTML using `cargo doc`. The generated HTML can be found in the *target/doc* directory. A handy tool is `cargo doc --open` try it out. Another type of documentation comment that should be placed at the top of crates or modules to introduce them use `//!`.

Common Documentation Sections:

- Examples
- Panics
- Errors
- Safety

One of the coolest features in rust is that any code blocks will be run **as tests** so that you know if a code change has broken an example in your documentation. Issuing `cargo test`, there will be a section at the bottom that looks as follows.
```
   Doc-tests my_crate

running 1 test
test src/lib.rs - your_test (line 5) ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.27s
```
Just make sure that your doc-test has an assert.

