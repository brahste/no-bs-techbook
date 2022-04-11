# Using Cargo and Crates

## Release Profiles

*Release profiles* allow a developer to use different configurations when compiling their code.

There are two main release profiles, *dev* and *release*. By default the *dev* profile is used (e.g. with `cargo build`) and the *release* profile can be toggled with `--release` (e.g. `cargo build --release`). 

You can override default options and add custom profiles to your *Cargo.toml* by adding a `[profile.*]` field. For example,

```toml
[profile.dev]
opt-level = 1
```

will change the amount of compile-time optimizations to 1 instead of the default 0 (though this change is not advised, you get the point). A full list of profile options can be found in [The Cargo Book](https://doc.rust-lang.org/cargo/reference/profiles.html).

## Published a Crate to Crates.io
