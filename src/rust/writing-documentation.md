# Writing Documentation

> Links:
> 
> - [Guide on how to write documentation for a Rust crate](https://blog.guillaume-gomez.fr/articles/2020-03-12+Guide+on+how+to+write+documentation+for+a+Rust+crate)

Generate Rust documentation using *rustdoc* which is provided with *cargo*.

```bash
$ cargo doc
```

This will create the docmentation for your crate. Open the documentation by adding the `--open` flag

```bash
$ cargo doc --open
```

## Documentation Comments

Use either `///` or `//!` to specify that the comments are meant for documentation. The former comment style should be used before the item being commented, while the latter should be used after the item being commented.

The best documentation blocks should be formatted to have three components:

1.  Brief explanation of what the item does

2. Example of how to use the function

3. Additional explanations and examples

... incomplete!...






