# Professional Strategies for Rust Development

1. You can alter the value behind a reference by using the `*` dereference operator. ?? Should this be used? Example?

### Trade-Offs of Using `clone`

Using `clone` has runtime costs. For this reason the Rust community disfavours the its use to satisfy the borrow checker. However, it isn't _always_ a bad idea to use `clone`. When the data being cloned is very small and when prototyping code it is acceptable to use `clone` to help address ownership problems. With more experience, better ways of satifying the borrow checker will become clear, at which point you can hyperoptimize the code if you please.
